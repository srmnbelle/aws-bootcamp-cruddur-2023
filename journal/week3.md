# Week 3 — Decentralized Authentication

## **HW Checklist**

- [**REQUIRED**](#assignments)
  - [x] [Setup Cognito User Pool](#setup-cognito-user-pool)
  - [x] [Implement Custom Signin Page](#implement-custom-signin-page)
  - [ ] [Implement Custom Signup Page](#implement-custom-signup-page)
  - [ ] [Implement Custom Confirmation Page](#implement-custom-confirmation-page)
  - [ ] [Implement Custom Recovery Page](#implement-custom-recovery-page)
  - [ ] [Watch about different approaches to verifying JWTs](#watch-about-different-approaches-to-verifying-jwts)
- [**EXTRA CHALLENGES**](#extra-challenges)
  - [ ] [Flask Middleware](#medium-decouple-the-jwt-verify-from-the-application-code-by-writing-a-flask-middleware)
  - [ ] [Container Sidecar pattern](#hard-decouple-the-jwt-verify-by-implementing-a-container-sidecar-pattern-using-awss-official-aws-jwt-verifyjs-library)
  - [ ] [Envoy as a sidecar](#hard-decouple-the-jwt-verify-process-by-using-envoy-as-a-sidecar-httpswwwenvoyproxyio)
  - [ ] [Implement a IdP login](#hard-implement-a-idp-login-eg-login-with-amazon-or-facebook-or-apple)
  - [ ] [Implement MFA](#easy-implement-mfa-that-send-an-sms-text-message-warning-this-has-spend-investigate-spend-before-considering-text-messages-are-not-eligible-for-aws-credits)

## **LECTURES**

### Live Stream | [Week 3 - Decentralized Authenication](https://www.youtube.com/watch?v=9obl7rVgzJw&list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv&index=40)

- Decentrialized Authentication
  - mechanism to log in/out, reset our passwords
  - to integrate in back-end application with custom log in pages
- Amazon Cognito via web UI
  - Under `User pools` on the left menu, click `Create user pool`
  - STEP 1 OF 6: Under `Cognito user pool sign-in options`, select `User name` and `Email`
  - STEP 2 OF 6: Under `Multi-factor authentication`, select `No MFA`
  - STEP 3 OF 6: Under `Required attributes`, add `name`
  - STEP 4 OF 6: Under `Email`, select `Send email with Cognito`
  - STEP 5 OF 6:
    - Under `User pool name`, type `cruddur-user pool`
    - Under `App client name`, type `cruddur`
  - STEP 6 OF 6: as is
  - Rest on default
- **REFERENCE INSTRUCTIONS:** [omenking's Week 3](https://github.com/omenking/aws-bootcamp-cruddur-2023/blob/week-3/journal/week3.md)
- Install AWS Amplify - used to get Cognito javascript library
  - Change directory `cd frontend-react-js/`
  - Install by running `npm i aws-amplify --save`
- Configure Amplify
  - Under `/frontend-react-js/src/`, open `App.js`
  - Paste the code blocks from week 3 reference instruction
  - Set the env variables on `docker-compose.yml`:
    ```
      REACT_APP_AWS_PROJECT_REGION: "${AWS_DEFAULT_REGION}"
      # REACT_APP_AWS_COGNITO_IDENTITY_POOL_ID: "" # not using identity pool
      REACT_APP_AWS_COGNITO_REGION: "${AWS_DEFAULT_REGION}"
      REACT_APP_AWS_USER_POOLS_ID: "" #from the user pool settings
      REACT_APP_CLIENT_ID: "" #under app integrations tab
    ```
- Conditionally show components based on logged in or logged out
  - Under `/frontend-react-js/src/pages`, open `HomeFeedPage.js`
    - Paste the code blocks from week 3 reference instruction
    - Some are already implemented
  - Under `/frontend-react-js/src/components`, open `DesktopNavigation.js`
    - Already implemented.
  - From the `DesktopNavigation.js` CTRL+ALT+CLICK `ProfileInjo.js` to eliminate explorer navigation
    - Paste the code blocks from week 3 reference instruction
  - `Compose Up` the docker file
    - port 3000: should be blank dark purple page; console saying "Uncaught Error: Both UserPoolId and ClientId are required."
    - edit `App.js` to correct the lines
    ```js
    region: process.env.REACT_APP_AWS_PROJECT_REGION;
    userPoolWebClientId: process.env.REACT_APP_CLIENT_ID;
    ```
- Sign in page
  - Under `/frontend-react-js/src/pages`, open `SigninPage.js`
    - Paste the code blocks from week 3 reference instruction
    - Some are already implemented
    - Change `setCognitoErrors` to `setErrors`
    - Change `Auth.signIn` variable from username to email
    - Check port:3000
  - Create new user pool - initially made one has incorrect configuration
    - STEP 3 OF 6: Under `Required attributes`, add `name` AND `preferred_username`
    - Reinitialize env var in `docker-compose.yml`
  - Update `onsubmit` code chunk to show `Incorrect username or password.` prompt on UI
  - (no email received) Create new user on AWS Cognito User Pool

### Additional Instructions | [Week 3 Cognito Custom Pages](https://www.youtube.com/watch?v=T4X4yIzejTc&list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv&index=42)

- **REFERENCE INSTRUCTIONS:** [omenking's Week 3](https://github.com/omenking/aws-bootcamp-cruddur-2023/blob/week-3/journal/week3.md)
- Sign in Page (continuation)
  - Using AWS CLI, do Force Change Password
    - `cd ..` then `sudo ./aws/install`
    - RUN `aws cognito-idp admin-set-user-password --username <INSERT USERNAME> --password <INSERT PASSWORD> --user-pool-id us-east-1_IOEdNYaQy --permanent`
  - Change `name` and `preferred username` on AWS Cognito UI
  - Done!
- Sign up Page
  - Under `/frontend-react-js/src/pages`, open `SignupPage.js`
  - Paste the code blocks from week 3 reference instruction
    - Some are already implemented
- Confirmation Page
  - Under `/frontend-react-js/src/pages`, open `ConfirmationPage.js`
  - Paste the code blocks from week 3 reference instruction
    - Some are already implemented
- Debugging
  - Create new user pool again
    - STEP 1 OF 6: Under `Cognito user pool sign-in options`, select ONLY `Email`
    - Reinitialize env var in `docker-compose.yml`
  - Done
  

### Additional Instructions | [Week 3 Congito JWT Server side Verify](https://www.youtube.com/watch?v=d079jccoG-M&list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv&index=43)

- to edit

### Additional Instructions | [Week 3 - Exploring JWTs](https://www.youtube.com/watch?v=nJjbI4BbasU&list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv&index=44)

- to edit

### Security Session | [Amazon Cognito Security Best Practices](https://www.youtube.com/watch?v=tEJIeII66pY&list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv&index=39)

- to be watched

### Additional Instructions | [Week 3 Improving UI Contrast and Implementing CSS Variables for Theming](https://www.youtube.com/watch?v=m9V4SmJWoJU&list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv&index=45)

- to be watched

### Pricing Session | [no link]()

- no video in playlist

### Cloud Career Session | [no link]()

- no video in playlist

## **ASSIGNMENTS**

### Setup Cognito User Pool

<img width="956" alt="create user pool" src="https://user-images.githubusercontent.com/64080430/226156584-42704154-7cd8-47cc-9509-cb0d054e709a.png">

### Implement Custom Signin Page

<img width="959" alt="singin page landing page with username" src="https://user-images.githubusercontent.com/64080430/226173316-34bec29a-32f0-4435-8f75-ed4e08676287.png">

### Implement Custom Signup Page

- to do

### Implement Custom Confirmation Page

- to do

### Implement Custom Recovery Page

- to do

### Watch about different approaches to verifying JWTs

- to do

## **EXTRA CHALLENGES**

### [Medium] Decouple the JWT verify from the application code by writing a Flask Middleware

### [Hard] Decouple the JWT verify by implementing a Container Sidecar pattern using AWS’s official Aws-jwt-verify.js library

### [Hard] Decouple the JWT verify process by using Envoy as a sidecar https://www.envoyproxy.io/

### [Hard] Implement a IdP login eg. Login with Amazon or Facebook or Apple.

### [Easy] Implement MFA that send an SMS (text message), warning this has spend, investigate spend before considering, text messages are not eligible for AWS Credits
