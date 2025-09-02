# ServiceNow-Word-of-the-Day-Agent

## <ins>I. Overview</ins><br/>
The ServiceNow Word of the Day agent is a test prep tool for the ServiceNow Certified System Administrator (CSA) and Certified Application Developer (CAD) certification exams. It provides a daily keyword or phrase and its definition for review, sent to the user's email. Built using n8n and OpenAI.

### <ins>Flow Diagram</ins>
<img width="1912" height="890" alt="template" src="https://github.com/user-attachments/assets/ceae2c3f-9cc7-49d6-bd17-ff18bf115fc6" />

## <ins>II. Building the Agent</ins></br>
- In order to receive daily emails, the agent is given a scheduled trigger. In this case, the trigger has been set to execute daily at 8am. <br/>

<img width="300" height="386" alt="trigger" src="https://github.com/user-attachments/assets/5a1e0391-800d-46da-bcba-76eadabe6337" /> <br/>
- The trigger fires into the AI agent node, which uses OpenAI for its LLM. The agent is prompted:<br/>
>"You are a ServiceNow guru, helping students study for the CSA and CAD. You should return a term that is valid and relevant in the **Yokohama release** only.<br/>
>
>Make sure you format your response as:
>Term: [name]  
>Definition: [1-2 sentence max]  
>Example: [realistic one line example of how it's used in ServiceNow]
>
>DO NOT include outdated terms and prioritize from the Yokohama release.
>Focus on terms specifically from the CSA and CAD exams."
<br/>
<img width="575" height="360" alt="AI node" src="https://github.com/user-attachments/assets/5a0b66b1-3367-4699-817c-2d9f3893d20e" /> <br/>

- In addition to the prompt, a structured output parser is given an example, to ensure all following responses are returned with the correct formatting:

````
{
  "term": "CMDB",
  "definition": "A centralized database that stores configuration items (CIs) and their relationships.",
  "example": "Admins use the CMDB to assess the impact of a failed email server."
}
````
<img width="260" height="360" alt="output parser" src="https://github.com/user-attachments/assets/cb7881e3-e05c-4b2f-8565-8ca534be0af2" /><br/>
- Finally, the agent's action is routed to send a message through a Gmail node. Here, the message is configured to convert the agent's JSON output to HTML, and structure it dynamically using JavaScript to allow for dynamic returns.
<br/>
<img width="250" height="380" alt="email" src="https://github.com/user-attachments/assets/7711af80-b617-41da-bc42-90f625bd4275" /><br/>
<img width="923" height="360" alt="email1" src="https://github.com/user-attachments/assets/5ac89d5d-adbf-4079-abd5-068e36af8ca1" /><br/><br/>

- Once successfully executed, the agent sends the user an email with an appropriate phrase or term and its definition, on a daily basis.<br/>
<img width="1097" height="422" alt="output" src="https://github.com/user-attachments/assets/33c66dbe-9578-44ab-ad3e-09466c90de36" />
