# Week 0 — Billing and Architecture

## **LECTURES**

### Live Stream | [Free AWS Cloud Project Bootcamp - Week 0 - Billing and Architecture](https://www.youtube.com/watch?v=SG8blanhAOg&list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv&index=11)

- From Margaret, our first speaker, I learned about the project scenario from her "user persona"-way of story telling. I learned in general that we are going to work on Cruddr, a twitter-like social media platform with expiring posts. For front-end, we're using Java and React. For back-end, we're using Python using Flask. And for APIs, we're using "Object Relational Mapping (ORM)". We're also going to utilize AWS but with great consideration on budget costs.
- From Chris, I learned the importance of MEETING requirements, and ADDRESSING the risks, assumptions, and constraints to create a good architecture. To create the designs, there are high-level to low-level types of design from conceptual, logical to physical design.

### Pre-recorded | [AWS Bootcamp Week 0 - Pricing Basics and Free tier](https://www.youtube.com/watch?v=OVw3RrlP-sI&list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv&index=9)

- From Chirag, I learned about the overview of different AWS pricing modules and the features available for free tier accounts. I also learned and done setting up the billing 


s as instructed in the video.

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

### Pre-recorded | [Week 0 - Homework Idea (Well Architected Tool)](https://www.youtube.com/watch?v=i-hOfAJb3cE&list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv&index=17)

- AWS Well-Architected framework is essentially a document with series of questions to determine if you follow the AWS-recommended best practices, or not.
- Ideally, for each "checkbox" in each of the questions, you provide proof or explanation on how you met the requirement.

### Pre-recorded | [AWS Organizations & AWS IAM Tutorial For Beginners - Cloud BootCamp - Week 0](https://www.youtube.com/watch?v=4EMWBYVggQI&list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv&index=13)

- Add MFA to root user to prevent "bad hackers" accessing the most powerful user
- Create an organization unit to help manage security, cost, billing policies
  - Recommended: having Management Account (with no resources), Active Account pool, and Standby Account pool
- Enable AWS Trail to audit "most" of logs
  - Region Service (huge network) vs Availability Zone (sub network within a region)
- Create IAM Users
  - Three types of users: (1) IAM user, (2) system user, (3) federated user
- Create AWS IAM Roles
  - Roles: used to assign specific permissions
  - Policies: defines the permissions; can be applied to users, groups, or roles
  - Roles and policies go hand-in-hand
- Enable organization Service Control Policies (SCPs)
  - [SCP Best Practices](https://github.com/hashishrajan/aws-scp-best-practice-policies/tree/main/AWS%20SCP%20Policies)
    <br>
<br>

## **ASSIGNMENTS**

### Recreate Conceptual Diagram in Lucid Charts or on a Napkin

- [Conceptual Diagram in Lucid Charts](https://lucid.app/lucidchart/c88c4d16-618d-4905-9987-71cf53745b04/edit?viewport_loc=-864%2C-212%2C1853%2C923%2C0_0&invitationId=inv_18ac208a-35fa-4dc6-99bb-8a6020d22915)

![Cruddr HW Diagrams - Livestream Conceptual Diagram](https://user-images.githubusercontent.com/64080430/218748367-0ad7b761-8f7b-4a8c-aa64-c079f848d99d.png)<br>

### Recreate Logical Architectual Diagram in Lucid Charts

- [Logical Diagram in Lucid Charts](https://lucid.app/lucidchart/c88c4d16-618d-4905-9987-71cf53745b04/edit?viewport_loc=-669%2C-435%2C1365%2C680%2Cwt8w7ByHRSOc&invitationId=inv_18ac208a-35fa-4dc6-99bb-8a6020d22915)

![Cruddr HW Diagrams - Pre-recorded Logical Diagram](https://user-images.githubusercontent.com/64080430/218748372-3032f387-2782-496b-a9f0-e67d98140ab8.png)<br>

### Create an Admin User

<img width="960" alt="05 create user admin" src="https://user-images.githubusercontent.com/64080430/218744514-6d800f04-2671-48de-a75e-652baa1e5ad6.png"><br>

### Using CloudShell

<img width="960" alt="03 HW HARD - Using CloudShell alt" src="https://user-images.githubusercontent.com/64080430/218747097-a54bfc39-02cd-4254-8807-00c1a0b561e8.png"><br>

### Generating AWS Credentials

<img width="960" alt="02 HW HARD - Generating AWS Credentials alt" src="https://user-images.githubusercontent.com/64080430/218747908-7dc2874a-3da6-49a3-aac6-57db500b43c9.png"><br>

### Install AWS CLI

<img width="960" alt="04 install cli" src="https://user-images.githubusercontent.com/64080430/218744631-594b3ecf-c44e-4a56-9028-4201fca032b3.png"><br>

### Set a Billing alarm

<img width="960" alt="00 HW HARD - Set a Billing alarm" src="https://user-images.githubusercontent.com/64080430/218322602-1f812377-ad99-49ce-a482-8796229792a5.png"><br>

### Set a AWS Budget

<img width="960" alt="01 HW HARD - Set a AWS Budget" src="https://user-images.githubusercontent.com/64080430/218322612-8c2aaba2-9e99-4721-bec9-b3646f9b5565.png"><br>
<br>

## **EXTRA CHALLENGES**

### Destroy your root account credentials, Set MFA, IAM role

<img width="960" alt="setup iam" src="https://user-images.githubusercontent.com/64080430/218747809-f602b67b-a2e8-441e-b3ee-7535bb7d2f74.png"><br>

### Use EventBridge to hookup Health Dashboard to SNS and send notification when there is a service health issue.

- Let's define the terms first:

  - **EventBridge** – provides real-time access to changes in data in AWS services, your own applications, and software as a service (SaaS) applications without writing code[\*](https://aws.amazon.com/eventbridge/faqs/)
  - **Health Dashboard** – shows reported service events for services across AWS Regions[\*](https://docs.aws.amazon.com/health/latest/ug/aws-health-dashboard-status.html)
  - **Simple Notification Service (SNS)** – sends notifications two ways, app-to-app and app-to-person[\*](https://aws.amazon.com/sns/)
  - **"service health issue"** – (I am assumming) this is also what they call "AWS Health events" which can be (1) Public events or (2) Account-specific events[\*](https://docs.aws.amazon.com/health/latest/ug/getting-started-health-dashboard.html#event-types)

- Setup
  - Create SNS Topic
    - Create topic: using health-alert in `TitleHere`

      ```
      aws sns create-topic --name TitleHere
      ```
      
    - Create subscription: using appropriate `TopicARN` and `your@email.com`

      ```
      aws sns subscribe \
          --topic-arn TopicARN \
          --protocol email \
          --notification-endpoint your@email.com
      ```
    <img width="960" alt="step00" src="https://user-images.githubusercontent.com/64080430/219013087-02d855cd-7fe3-4a0e-a172-a157e969f8de.png"><br>

  - Open the [Service Health Dashboard](https://status.aws.amazon.com/) or [Amazon EventBridge console](https://console.aws.amazon.com/events/)
  - Configure an [Amazon EventBridge Rule](https://console.aws.amazon.com/events/home#rules/create) and follow the [documentation](https://docs.aws.amazon.com/health/latest/ug/cloudwatch-events-health.html#creating-event-bridge-events-rule-for-aws-health)
    1. Define rule detail
       - Entered `Name` and `Description`. All else default.

    <img width="960" alt="step1" src="https://user-images.githubusercontent.com/64080430/219013142-b3c23db4-7be9-4538-a9dc-8bf8b28e302d.png"><br>

    2. Build event pattern
       - Under **Event pattern**, edited the `Event source`, `AWS service`, `Event type`, the `Specific service(s)`, and the `Specific event type category(s)` as shown in figure below. All else default.
       
    <img width="960" alt="step2" src="https://user-images.githubusercontent.com/64080430/219013179-b5d6ba3d-91c6-45de-93b2-e442bb54f92d.png"><br>

    3. Select target(s)
       - Selected appropriate `Target types`, `Select a target`, and `Topic` to hookup SNS.

    <img width="960" alt="step3" src="https://user-images.githubusercontent.com/64080430/219013245-c08f96dd-a235-4697-9925-513f30724d73.png"><br>

    4. Configure tags: _skipped_<br>
    5. Review and create: Done!

    <img width="960" alt="step4" src="https://user-images.githubusercontent.com/64080430/219013266-0b6dc83b-75a2-4619-a54e-2fb4626badb9.png">

### Review all the questions of each pillars in the Well Architected Tool (No specialized lens)

- PENDING

### Create an architectural diagram (to the best of your ability) the CI/CD logical pipeline in Lucid Charts

- PENDING

### Research the technical and service limits of specific services and how they could impact the technical path for technical flexibility.

- PENDING

### Open a support ticket and request a service limit

- PENDING
