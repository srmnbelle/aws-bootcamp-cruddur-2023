# Week 1 — App Containerization

## **HW Checklist**

- [**REQUIRED**](#assignments)
  - [ ] [Document the Notification Endpoint for the OpenAPI Document](#document-the-notification-endpoint-for-the-openapi-document)
  - [ ] [Write a Flask Backend Endpoint for Notifications](#write-a-flask-backend-endpoint-for-notifications)
  - [ ] [Write a React Page for Notifications](#write-a-react-page-for-notifications)
  - [ ] [Run DynamoDB Local Container and ensure it works](#run-dynamodb-local-container-and-ensure-it-works)
  - [ ] [Run Postgres Container and ensure it works](#run-postgres-container-and-ensure-it-works)
- [**EXTRA CHALLENGES**](#extra-challenges)
  - [ ] [Run the dockerfile CMD as an external script](#run-the-dockerfile-cmd-as-an-external-script)
  - [ ] [Push and tag a image to DockerHub](#push-and-tag-a-image-to-dockerhub-they-have-a-free-tier)
  - [ ] [Use multi-stage building for a Dockerfile build](#use-multi-stage-building-for-a-dockerfile-build)
  - [ ] [Implement a healthcheck in the V3 Docker compose file](#implement-a-healthcheck-in-the-v3-docker-compose-file)
  - [ ] [Research best practices of Dockerfiles and implement](#research-best-practices-of-dockerfiles-and-attempt-to-implement-it-in-your-dockerfile)
  - [ ] [Install Docker on your local machine](#learn-how-to-install-docker-on-your-localmachine-and-get-the-same-containers-running-outside-of-gitpod--codespaces)
  - [ ] [Launch an EC2 instance and pull a container](#launch-an-ec2-instance-that-has-docker-installed-and-pull-a-container-to-demonstrate-you-can-run-your-own-docker-processes)

## **LECTURES**

### Live Stream | [Week 1 — App Containerization](https://www.youtube.com/watch?v=zJnNe5Nv4tE&list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv&index=23)

- Benefits of containerization
  - makes the code "more portable"
  - minimize the chances of "destroying the environment" ?
  - simplifies the workflow by having specific (& working) config file
- Docker Hub

  - a "container registry"
  - github for images

- Dockerfile

  - list of series of commands
  - `scratch` - a no op file

- Instructional material: [omenking's Week 1 Journal](https://github.com/omenking/aws-bootcamp-cruddur-2023/blob/week-1/journal/week1.md)
- Containerize Backend
  - Initial set-up
    ```
    cd backend-flask
    pip3 install -r requirements.txt
    export FRONTEND_URL="*"
    export BACKEND_URL="*"
    python3 -m flask run --host=0.0.0.0 --port=4567
    cd ..
    ```
  - Add `Dockerfile` in backend-flask
  - Build and run container
    ```
    docker build -t  backend-flask ./backend-flask
    docker run --rm -p 4567:4567 -it -e FRONTEND_URL='*' -e BACKEND_URL='*' backend-flask
    ```
- Containerize Front-end

  - Install npm
  - Add `Dockerfile` in frontend-react-js

- Multiple Containers
  - Create `docker-compose.yml` to run both back-end and front-end containers
  - Right-click and select `Compose Up`
  - Note! Use gitpod in web browser to easily unlock ports 3000 and 4567 (can't find that button when running on my desktop VS code - opening localhost:3000 don't show posts)

### Pre-recorded | [Week 1- After Stream - Commit Your Code](https://www.youtube.com/watch?v=b-idMgFFcpg&list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv&index=24)

- Just a reminder to commit edits ?

### Pre-recorded | [Top 10 Docker Container Security Best Practices with Tutorial](https://www.youtube.com/watch?v=OjZz4D0B-cA&list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv&index=25)

- TO BE WATCHED

### Pre-recorded | [Week 1 - Create the notification feature (Backend and Front)](https://www.youtube.com/watch?v=k-_o0cCpksk&list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv&index=27)

- OpenAPI Swagger
  - good standard to document APIs
  - With free-tier API readme generator: https://readme.so/
- Initial Set-up
  - `Compose Up` the `docker-compose.yml` - but will show Port 3000 Not Found
    - `Compose Down` the `docker-compose.yml`
    - Do `npm i` in `cd frontend-react-js`
  - Click "Join Now" in the Cruddur web app
    - Enter your sign up details with "Confirmation Code" as 1234
- Add backend endpoint

  - Open `openapi-3.0.yml`; library reference: https://spec.openapis.org/oas/v3.1.0
  - Click `OpenAPI: Add new path`
  - Edit the line to `/api/activities/notifications`
  - Pattern content to existing path of `/api/activities/home`
    - Add description, tags, responses format
  - Open the `app.py` file

    - Add the lines

      ```
      from services.notifications_activities import *

      @app.route("/api/activities/notifications", methods=['GET'])
        def data_notifications():
        data = NotificationsActivities.run()
        return data, 200
      ```

    - Create the `notifications_activities.py` file under services folder
      - Copy content from home_activities.py just change class to `NotificationsActivities`

  - Run the address for port 3000 and append `/api/activities/notifications`

- Implement a Frontend UI

  - Open the file `App.js` under /frontend-react-js/src

    - Add the lines

      ```
      import NotificationsFeedPage from './pages/NotificationsFeedPage';

      {
        path: "/notifications",
        element: <NotificationsFeedPage />
      },
      ```

  - Create the `NotificationsFeedPage.js`

    - Copy content from `HomeFeedPage.js`
    - Change the text from "Home" to "Notifications" of the corresponding lines

    ```
    import './NotificationsFeedPage.css';

    export default function NotificationsFeedPage() {

    const backend_url = `${process.env.REACT_APP_BACKEND_URL}/api/activities/notifications`

    <DesktopNavigation user={user} active={'notifications'} setPopped={setPopped} />

    title="Notifications"
    ```

  - Create the `NotificationsFeedPage.css` but put nothing
  - Run the address for port 3000 and append `/api/activities/notifications`

### Pre-recorded | [Week 1 - DynamoDB and Postgres vs Docker](https://www.youtube.com/watch?v=CbQNMaa6zTg&list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv&index=28)

- TO BE WATCHED

## **ASSIGNMENTS**

### Document the Notification Endpoint for the OpenAPI Document

### Write a Flask Backend Endpoint for Notifications

### Write a React Page for Notifications

### Run DynamoDB Local Container and ensure it works

### Run Postgres Container and ensure it works

## **EXTRA CHALLENGES**

### Run the dockerfile CMD as an external script

### Push and tag a image to DockerHub (they have a free tier)

### Use multi-stage building for a Dockerfile build

### Implement a healthcheck in the V3 Docker compose file

### Research best practices of Dockerfiles and attempt to implement it in your Dockerfile

### Learn how to install Docker on your localmachine and get the same containers running outside of Gitpod / Codespaces

### Launch an EC2 instance that has docker installed, and pull a container to demonstrate you can run your own docker processes.
