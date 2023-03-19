# Week 3 — Decentralized Authentication

## **HW Checklist**

- [**REQUIRED**](#assignments)
  - [x] [Setup Cognito User Pool](#setup-cognito-user-pool)
  - [ ] [Implement Custom Signin Page](#implement-custom-signin-page)
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
- AWS Amplify - used to get Cognito javascript library

### Security Session | [Amazon Cognito Security Best Practices](https://www.youtube.com/watch?v=tEJIeII66pY&list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv&index=39)

- to be watched

### Additional Instructions | [Week 3 Cognito Custom Pages](https://www.youtube.com/watch?v=T4X4yIzejTc&list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv&index=42)

- to edit

### Additional Instructions | [Week 3 Congito JWT Server side Verify](https://www.youtube.com/watch?v=d079jccoG-M&list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv&index=43)

- to edit

### Additional Instructions | [Week 3 - Exploring JWTs](https://www.youtube.com/watch?v=nJjbI4BbasU&list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv&index=44)

- to edit

### Additional Instructions | [Week 3 Improving UI Contrast and Implementing CSS Variables for Theming](https://www.youtube.com/watch?v=m9V4SmJWoJU&list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv&index=45)

- to edit

### Pricing Session | [no link]()

- no video in playlist

### Cloud Career Session | [no link]()

- no video in playlist

## **ASSIGNMENTS**

### Setup Cognito User Pool
<img width="956" alt="create user pool" src="https://user-images.githubusercontent.com/64080430/226156584-42704154-7cd8-47cc-9509-cb0d054e709a.png">

### Implement Custom Signin Page

- to do

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
