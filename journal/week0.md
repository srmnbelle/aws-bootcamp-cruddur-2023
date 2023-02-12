# Week 0 — Billing and Architecture

## Lectures

### Live Stream | [Free AWS Cloud Project Bootcamp - Week 0 - Billing and Architecture](https://www.youtube.com/watch?v=SG8blanhAOg&list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv&index=11)

- From Margaret, our first speaker, I learned about the project scenario from her "user persona"-way of story telling. I learned in general that we are going to work on Cruddr, a twitter-like social media platform with expiring posts. For front-end, we're using Java and React. For back-end, we're using Python using Flask. And for APIs, we're using "Object Relational Mapping (ORM)". We're also going to utilize AWS but with great consideration on budget costs.
- From Chris, I learned the importance of MEETING requirements, and ADDRESSING the risks, assumptions, and constraints to create a good architecture. To create the designs, there are high-level to low-level types of design from conceptual, logical to physical design.

### Pre-recorded | [AWS Bootcamp Week 0 - Pricing Basics and Free tier](https://www.youtube.com/watch?v=OVw3RrlP-sI&list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv&index=9)

- From Chirag, I learned about the overview of different AWS pricing modules and the features available for free tier accounts. I also learned and done setting up the billing alerts as instructed in the video.

### Pre-recorded | [AWS Organizations & AWS IAM Tutorial For Beginners - Cloud BootCamp - Week 0](https://www.youtube.com/watch?v=4EMWBYVggQI&list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv&index=13)

-

### Pre-recorded | [Week 0 - Generate Credentials, AWS CLI, Budget and Billing Alarm via CLI](https://www.youtube.com/watch?v=OdUnNuKylHg&list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv&index=13)

- Created budget and set-up alerts based on dollar ($0.01) and credit ($1 alert at 80%) spending
- Created an IAM user credentials
- Introduced to AWS Cloudshell
  - CLI Commands Reference https://docs.aws.amazon.com/cli/latest/reference/
- Installed CLI Commands to Gitpod environment
  - Tested `aws sts get-caller-identity` and saved credentials to Gitpod
- Recreated AWS Budget using Gitpod CLI Commands
- Created SNS Topic (with pending confirmation from email) and Cloudwatch Alarm

## Assignments

### Hard

- Set a Billing alarm
<img width="960" alt="00 HW HARD - Set a Billing alarm" src="https://user-images.githubusercontent.com/64080430/218322602-1f812377-ad99-49ce-a482-8796229792a5.png">
- Set a AWS Budget
<img width="960" alt="01 HW HARD - Set a AWS Budget" src="https://user-images.githubusercontent.com/64080430/218322612-8c2aaba2-9e99-4721-bec9-b3646f9b5565.png">
- Generating AWS Credentials
<img width="960" alt="02 HW HARD - Generating AWS Credentials" src="https://user-images.githubusercontent.com/64080430/218322618-33da8522-1414-4729-84c2-259fcc086f0e.png">
- Using CloudShell
<img width="960" alt="03 HW HARD - Using CloudShell" src="https://user-images.githubusercontent.com/64080430/218322641-194eec0d-d927-47a8-a703-3226571983a6.png">
- Conceptual Architecture Diagram or your Napkins
  * PENDING. Not sure if this should be an original diagram as I'm not well-versed in the web dev/cloud blocks and how each works/interacts

### Stretch

-
