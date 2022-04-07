# IaC Code for Social Distancing Violation Detection

## Requirements
- A Free Tier AWS account
- An EC2 instance to deploy the infrastructure

## Steps to Take Before Deploying the Project
1. Launch an EC2 instance with the shared AMI named "SWEN_TEAM8_TERM_PROJECT_AMI" and connect to it using SSH
2. Clone this repository and enter its directory `git clone https://github.com/RIT-cloud-computing/term-project-team-team-8.git && cd term-project-team-team-8`
3. Change permission of the automation bash script that will spin up all resources: `chmod u+x automate.sh`
4. Convert the line endings of the automation bash script from Windows to Unix line endings: `sed -i -e 's/\r$//' automate.sh`
5. Open sns-lambda.py using Vim: `vim sns-lambda.py`
6. On line 23, the TargetArn is given a parameter in the following format: `TargetArn='arn:aws:sns:us-east-1:AWS_ACCOUNT_ID_NUMBER:crowd_lambda'`. Replace AWS_ACCOUNT_ID_NUMBER with the ID number of your AWS account
7. Save the changes, exit vim and open lambda.tf: `vim lambda.tf`
8. Add your emails in line 4 to get SNS notifications: `emails = ["email1@email.com","email2@email.com",...]`
9. Exit vim

## Deploying and Running the Project
1. Run the automation bash script to automatically spin up resources. This will result in additional prompts: `./automate.sh`
2. Enter your AWS access key ID and AWS secret access key
3. Enter `us-east-1` as the default region
4. Enter `text` as default output format
5. Terraform needs an access token to deploy the Ampify app. To find the access token, please check the Slack channel's pinned message, as entering it in GitHub immediately revokes it
6. Enter `yes` to give permission to Terraform to create all the resources and wait for it to complete
7. You will receive an email regarding a subscription from AWS Notifications. Confirm the subscription by clicking on the link in the email
8. Navigate to the Amplify app on the AWS console and check if "amp-terr-test" has been completely deployed
9. Press Enter to run the program. This will run test.sh
10. test.sh is a script that will process the video feed used in this repository. Since it is a small video feed, the script will stop at some point. Once the script outputs `Working on frame number: n`, you can open the Amplify app link in the AWS console
11. The Amplify app will display a video feed looking for any social distancing violations. You may receive an email with a link to a frame of the video if too many social distancing violations occur in a period of time.
12. When the feed has stopped processing, a prompt will appear asking you to destroy the created resources. Press Enter to continue