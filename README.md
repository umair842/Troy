# Fetch Tool Agent Workflows - n8n Automation

## Overview

This project contains a set of n8n workflows used for automating the management of job enquiries, payroll inquiries, general inquiries, and escalation complaints for the Fetch Recruitment team. The workflows are designed to manage various incoming requests, process relevant data, and send necessary notifications to the concerned teams.

## Workflow Overview

### 1. Job Enquiry Workflow (`Fetch-Tool-Agent1_JobEnquiry-log_job_enquiry`)
This workflow handles incoming job enquiries through a webhook, processes the request, and forwards the necessary information to the appropriate recruiter team via email.

- **Steps**:
  - Receives job enquiry data from a webhook.
  - Edits the fields, including caller name, phone, email, message, recruiter group, transcription, etc.
  - Routes the data based on the recruiter group.
  - Sends confirmation emails to the recruiter team and handles any errors or fallback scenarios.

### 2. Recruiter Team Lookup Workflow (`Fetch-Tool-Agent1_JobEnquiry-lookup_recruiter_team`)
This workflow is designed to fetch relevant recruiter information based on the recruiter group from a data table and route the enquiry accordingly.

- **Steps**:
  - Retrieves recruiter team details based on the input recruiter group.
  - Sends emails to the recruiter team.
  - Sends fallback emails in case of errors.

### 3. Save Job Enquiry to Google Sheets (`Fetch-Tool-Agent1_JobEnquiry-Save-Gsheet-2-DataStore`)
This workflow is scheduled to run on a set interval and updates job enquiry data into a Google Sheets document.

- **Steps**:
  - Fetches job enquiry data.
  - Upserts the data into a Google Sheets document for storage and tracking.

### 4. Payroll Enquiry Workflow (`Fetch-Tool-Agent2_Payroll-log_payroll_enquiry`)
This workflow handles payroll-related enquiries, collects necessary data, and sends emails to the payroll team.

- **Steps**:
  - Receives payroll enquiry data through a webhook.
  - Processes and edits the data including caller details, issue summary, and transcription.
  - Sends an email to the payroll team regarding the enquiry.

### 5. General Inquiry Workflow (`Fetch-Tool-Agent4_General-Fallback-log_general_enquiry`)
This workflow deals with general inquiries and escalates them to the appropriate team.

- **Steps**:
  - Receives general enquiry data.
  - Processes and sends emails to the appropriate department or individual.
  - Handles fallback scenarios and error notifications.

### 6. Escalation/Complaint Workflow (`Fetch-Tool-Agent5_Escalation-Complaints-log_complaint_enquiry`)
This workflow is designed for handling complaint or escalation enquiries, ensuring that the issue is routed to the correct escalation team.

- **Steps**:
  - Receives complaint data.
  - Processes and sends an email to the escalation team.
  - Handles email notifications with detailed enquiry summaries and transcriptions.

## Setup and Requirements

### Prerequisites

- **n8n** instance setup for automation.
- **AWS SES** credentials configured for sending emails.
- **Google Sheets** API credentials configured for updating the Google Sheets.
- Data tables for recruiter information and job enquiries.
  
### Environment Configuration

1. **n8n Setup**:
   - Ensure n8n is installed and accessible for workflow execution.
   - Add necessary API credentials for AWS and Google Sheets in n8n's credentials manager.

2. **Google Sheets Configuration**:
   - Update the `Fetch-Tool-Agent1_JobEnquiry-Save-Gsheet-2-DataStore` workflow with your Google Sheets document ID and sheet name.

3. **Webhook URLs**:
   - Ensure the webhook URLs for each workflow are properly configured to receive incoming data.

4. **Email Configurations**:
   - Update email addresses in workflows to ensure the right teams receive notifications.

## Execution Flow

1. A **job enquiry** request is received via a webhook, and the data is processed through the `Fetch-Tool-Agent1_JobEnquiry-log_job_enquiry` workflow.
2. The request is then routed to the relevant **recruiter team**, and an email is sent with the details of the enquiry.
3. Enquiry details are optionally saved to a **Google Sheets** document for reference and tracking.
4. Similarly, **payroll**, **general**, and **complaint** workflows operate in a similar manner with emails sent to the relevant departments and fallback notifications for any errors.

## Error Handling

- Each workflow contains provisions for sending **error notifications** via email in case of issues during processing.
- **Fallback workflows** ensure that if a primary routing fails, the inquiry is forwarded to an alternative team or recipient for handling.

## Contributing

Feel free to fork the repository and contribute improvements. For any issues, raise a bug report or open a pull request with your fixes.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details.
