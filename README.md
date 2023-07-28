# README for SendEmail

## Description:

The SendEmailAction is a custom GitHub Action designed to send an email using Gmail. It allows you to send an email to a recipient with a specified subject and body. Optionally, you can also attach log files to the email.

## Inputs:

- **recipient (required):** The recipient's email address.
- **subject (required):** The subject of the email.
- **emailBody (required):** The body of the email.
- **attachments (optional):** An optional list of log file paths to attach to the email.
- **Privatekey (required):** The SMTP private key of the sender's email account. It is recommended to store this as a secret in your repository.
- **username (required):** The sender's username email.
- **senderEmail (required):** The sender's email address.

## How it Works:

1. The action starts by creating an email file (**email.txt**) containing the specified subject and email body.
2. If there are any log file attachments specified (**attachments input**), it creates a folder named logs and copies each log file to this folder.
3. Finally, it sends the email using the **curl** command with the SMTP details of the sender's Gmail account.

## Usage:

To use this action in your GitHub workflow, you can add the following snippet to your workflow YAML file (e.g., .github/workflows/send_email.yml):


    name: Send Email
    on:
      push:
        branches:
          - main
    
    jobs:
      send_email_job:
        runs-on: ubuntu-latest
        steps:
        - name: Checkout code
          uses: actions/checkout@v2
    
        
        - name: Send Email
          uses: vphanideep/GithubActions@v1
          with:
            recipient: your_recipient_email@gmail.com
            subject: 'Enter email subject'
            emailBody: 'Enter email body here'
            attachments: 'path/to/attachment1.txt,path/to/attachment2.log'
            Privatekey: ${{ secrets.SMTP_PRIVATE_KEY }}
            username: yourusername@gmail.com
            senderEmail: youremail@gmail.com

        
### Note:

Before using this action, make sure to enable access to less secure apps in your Gmail settings or use an App Password if two-factor authentication is enabled for your Gmail account.

Ensure you have the necessary permissions to access the specified attachments and read the content of the files.

### Security Note:

It is highly recommended to use GitHub secrets (secrets.SMTP_PRIVATE_KEY in this case) to store sensitive information like passwords, private keys, and tokens securely. Avoid hardcoding sensitive information directly in your workflow files.

## Disclaimer:
Please use this action responsibly and only with Gmail accounts that you own or have permission to use for sending emails. Sending emails without proper authorization may violate the terms of service of your email provider and can lead to account suspension or other consequences.
