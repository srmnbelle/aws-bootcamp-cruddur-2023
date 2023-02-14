# Week 0 — Billing and Architecture

## LECTURES

### Live Stream | [Free AWS Cloud Project Bootcamp - Week 0 - Billing and Architecture](https://www.youtube.com/watch?v=SG8blanhAOg&list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv&index=11)

- From Margaret, our first speaker, I learned about the project scenario from her "user persona"-way of story telling. I learned in general that we are going to work on Cruddr, a twitter-like social media platform with expiring posts. For front-end, we're using Java and React. For back-end, we're using Python using Flask. And for APIs, we're using "Object Relational Mapping (ORM)". We're also going to utilize AWS but with great consideration on budget costs.
- From Chris, I learned the importance of MEETING requirements, and ADDRESSING the risks, assumptions, and constraints to create a good architecture. To create the designs, there are high-level to low-level types of design from conceptual, logical to physical design.

### Pre-recorded | [AWS Bootcamp Week 0 - Pricing Basics and Free tier](https://www.youtube.com/watch?v=OVw3RrlP-sI&list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv&index=9)

- From Chirag, I learned about the overview of different AWS pricing modules and the features available for free tier accounts. I also learned and done setting up the billing alerts as instructed in the video.

### Pre-recorded | [Week 0 - Generate Credentials, AWS CLI, Budget and Billing Alarm via CLI](https://www.youtube.com/watch?v=OdUnNuKylHg&list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv&index=13)

- Created budget and set-up alerts based on dollar ($0.01) and credit ($1 alert at 80%) spending
- Created an IAM user credentials
- Introduced to AWS Cloudshell
  - CLI Commands Reference https://docs.aws.amazon.com/cli/latest/reference/
- Installed CLI Commands to Gitpod environment
  - Tested `aws sts get-caller-identity` and saved credentials to Gitpod
- Recreated AWS Budget using Gitpod CLI Commands
- Created SNS Topic (with pending confirmation from email) and Cloudwatch Alarm

### Pre-recorded | [Week 0 - Lucid Charts Lets Recreate the Cruddur Logical Diagram ](https://www.youtube.com/watch?v=K6FDrI_tz0k&list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv&index=18)

- Walkthrough on how to obtain AWS architecture icons and other related resources
- Recreated the sample logical diagram presented on the livestream
  - Possible use of other line weight/color/design to denote different process but make sure to include labels
- Imported SVG file to Lucid Charts; use of Adobe Illustrator to edit SVG file

### Pre-recorded | [Week 0 - Homework Idea (Well Architected Tool](https://www.youtube.com/watch?v=i-hOfAJb3cE&list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv&index=17)

- AWS Well-Architected framework is essentially a document with series of questions to determine if you follow the AWS-recommended best practices, or not.
- Ideally, for each "checkbox" in each of the questions, you provide proof or explanation on how you met the requirement.

### Pre-recorded | [AWS Organizations & AWS IAM Tutorial For Beginners - Cloud BootCamp - Week 0](https://www.youtube.com/watch?v=4EMWBYVggQI&list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv&index=13)

- TO BE WATCHED

## ASSIGNMENTS

### REQUIRED

#### Recreate Conceptual Diagram in Lucid Charts or on a Napkin

- [Conceptual Diagram in Lucid Charts](https://lucid.app/lucidchart/c88c4d16-618d-4905-9987-71cf53745b04/edit?viewport_loc=-864%2C-212%2C1853%2C923%2C0_0&invitationId=inv_18ac208a-35fa-4dc6-99bb-8a6020d22915)
![Cruddr HW Diagrams - Livestream Conceptual Diagram](https://user-images.githubusercontent.com/64080430/218744337-07452ce5-a22d-498b-840d-27ed541b4d3a.jpeg)

#### Recreate Logical Architectual Diagram in Lucid Charts

- [Logical Diagram in Lucid Charts](https://lucid.app/lucidchart/c88c4d16-618d-4905-9987-71cf53745b04/edit?viewport_loc=-669%2C-435%2C1365%2C680%2Cwt8w7ByHRSOc&invitationId=inv_18ac208a-35fa-4dc6-99bb-8a6020d22915)
![Cruddr HW Diagrams - Pre-recorded Logical Diagram](https://user-images.githubusercontent.com/64080430/218744298-fd1fd9fe-694f-422e-b548-23b39fe8aaae.jpeg)

#### Create an Admin User
<img width="960" alt="05 create user admin" src="https://user-images.githubusercontent.com/64080430/218744514-6d800f04-2671-48de-a75e-652baa1e5ad6.png">

#### Using CloudShell

<img width="960" alt="03 HW HARD - Using CloudShell alt" src="https://user-images.githubusercontent.com/64080430/218746708-106589db-b621-406e-b419-23b16d25d1a1.png">


#### Generating AWS Credentials

<img width="960" alt="02 HW HARD - Generating AWS Credentials alt" src="https://user-images.githubusercontent.com/64080430/218746669-bb124a71-9977-4a4e-80e6-3d9deee59359.png">


#### Install AWS CLI
<img width="960" alt="04 install cli" src="https://user-images.githubusercontent.com/64080430/218744631-594b3ecf-c44e-4a56-9028-4201fca032b3.png">

#### Set a Billing alarm

<img width="960" alt="00 HW HARD - Set a Billing alarm" src="https://user-images.githubusercontent.com/64080430/218322602-1f812377-ad99-49ce-a482-8796229792a5.png">

#### Set a AWS Budget

<img width="960" alt="01 HW HARD - Set a AWS Budget" src="https://user-images.githubusercontent.com/64080430/218322612-8c2aaba2-9e99-4721-bec9-b3646f9b5565.png">

### CHALLENGES

#### Destroy your root account credentials, Set MFA, IAM role

<img width="960" alt="setup iam" src="https://user-images.githubusercontent.com/64080430/218746749-ae5386e7-dfb8-4bbc-8a34-59ed149eacd5.png">


#### Use EventBridge to hookup Health Dashboard to SNS and send notification when there is a service health issue.

- PENDING

#### Review all the questions of each pillars in the Well Architected Tool (No specialized lens)

- PENDING

#### Create an architectural diagram (to the best of your ability) the CI/CD logical pipeline in Lucid Charts

- PENDING

#### Research the technical and service limits of specific services and how they could impact the technical path for technical flexibility.

- PENDING

#### Open a support ticket and request a service limit

- PENDING
