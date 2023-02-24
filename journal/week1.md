# Week 1 — App Containerization

## **HW Checklist**

- [**REQUIRED**](#assignments)
  - [x] [Document the Notification Endpoint for the OpenAPI Document](#document-the-notification-endpoint-for-the-openapi-document)
  - [x] [Write a Flask Backend Endpoint for Notifications](#write-a-flask-backend-endpoint-for-notifications)
  - [x] [Write a React Page for Notifications](#write-a-react-page-for-notifications)
  - [x] [Run DynamoDB Local Container and ensure it works](#run-dynamodb-local-container-and-ensure-it-works)
  - [x] [Run Postgres Container and ensure it works](#run-postgres-container-and-ensure-it-works)
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
    ```sh
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

      ```py
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

      ```js
      import NotificationsFeedPage from './pages/NotificationsFeedPage';

      {
        path: "/notifications",
        element: <NotificationsFeedPage />
      },
      ```

  - Create the `NotificationsFeedPage.js`

    - Copy content from `HomeFeedPage.js`
    - Change the text from "Home" to "Notifications" of the corresponding lines

    ```js
    import './NotificationsFeedPage.css';

    export default function NotificationsFeedPage() {

    const backend_url = `${process.env.REACT_APP_BACKEND_URL}/api/activities/notifications`

    <DesktopNavigation user={user} active={'notifications'} setPopped={setPopped} />

    title="Notifications"
    ```

  - Create the `NotificationsFeedPage.css` but put nothing
  - Run the address for port 3000 and append `/api/activities/notifications`

### Pre-recorded | [Week 1 - DynamoDB and Postgres vs Docker](https://www.youtube.com/watch?v=CbQNMaa6zTg&list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv&index=28)

- DynamoDB **Local** - [set-up guide](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/DynamoDBLocal.DownloadingAndRunning.html)

  - emulation of DynamoDB to interact faster

- Initial Set-up
  - Open `docker-composer.yml` file
  - Append the Postgres and DynamoDB Local code sections
    ```yml
    dynamodb-local:
      user: root
      command: "-jar DynamoDBLocal.jar -sharedDb -dbPath ./data"
      image: "amazon/dynamodb-local:latest"
      container_name: dynamodb-local
      ports:
        - "8000:8000"
      volumes:
        - "./docker/dynamodb:/home/dynamodblocal/data"
      working_dir: /home/dynamodblocal
    db:
      image: postgres:13-alpine
      restart: always
      environment:
        - POSTGRES_USER=postgres
        - POSTGRES_PASSWORD=password
      ports:
        - "5432:5432"
      volumes:
        - db:/var/lib/postgresql/data
    ```
  - Append the volumes section at the end
    ```yml
    volumes:
      db:
        driver: local
    ```
- Running and testing DynamoDB Local
  - Right click the .yml file to `Compose Up`
  - Check if AWS CLI commands works by typing `aws`
  - Test responses using AWS CLI commands - [/100DaysOfCloud reference](https://github.com/100DaysOfCloud/challenge-dynamodb-local)
    - Create a table
    - Create an item
    - List Tables
    - Get Records
    ```
    aws dynamodb scan --table-name Music --query "Items" --endpoint-url http://localhost:8000
    ```
- Running and testing Postgres
  - Install the postgres client into Gitpod
    - Open `.gitpod.yml` file
    - Add under `tasks:`
    ```yml
    - name: postgres
      init: |
        curl -fsSL https://www.postgresql.org/media/keys/ACCC4CF8.asc|sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/postgresql.gpg
        echo "deb http://apt.postgresql.org/pub/repos/apt/ `lsb_release -cs`-pgdg main" |sudo tee  /etc/apt/sources.list.d/pgdg.list
        sudo apt update
        sudo apt install -y postgresql-client-13 libpq-dev
    ```
    - Run each commands by line in terminal
  - Create the standard tables in Postgres database
    - Install the PostgreSQL extension
    - Open the Database Explorer
    - Add connection using + button
      - Select `PostgresSQL` tab
      - Edit name to "database connection"
      - Change password to "password"
      - Remove "special connection database" auto-filled name
  - Test `psql`
    - Debugging
      - `Compose down` the docker-compose.yml file
      - `Compose up` again
    - Use `psql -Upostgres --host localhost`
      - Type in "password"
      - Test commands
        - `\l` to show the standard tables
        - `\q` to quit

### Pre-recorded | [Top 10 Docker Container Security Best Practices with Tutorial](https://www.youtube.com/watch?v=OjZz4D0B-cA&list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv&index=25)

- Container Security
  - protecting "compute service"/containers
  - Unmanaged vs Managed containers
    - Unmanaged: Docker or containers that run outside the cloud
    - Managed: ECS, ECR
- Best Practices
  - Docker & host config
    - Update security patches
    - Non-root user mode from "docker daemon & containers"
  - Securing images
    - Images should only include what the application needed
    - Private vs Public image registry
  - Secret management
    - No sensitive data
  - Data Security
    - Read-only file system
  - Application Security
    - Use "DevSecOps" practices
    - Test code for vulnerability
- Docker Compose
  - Snyk OpenSource Security - to secure dependencies
- AWS Secret Manager or Hashicorp Vault
  - to store secrets
- AWS Inspector or Clair
  - to scan AMI/ image vulnerabilities?
- Snyk demo

### Pre-recorded | [AWS Bootcamp Week 1 - Gitpod, Github Codespaces, AWS Cloud9 and Cloudtrail](https://www.youtube.com/watch?v=OAMHu1NiYoI&list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv&index=25)

- Gitpod limit
  - 50 hr/month
- Github codespaces
  - 2-core: 60 hr/month
  - 4-core: 30 hr/month
  - 8-core: 15 hr/month
- AWS Cloud9
  - Uses ec2
- Cloudtrail
  - **avoid** using as not needed for the bootcamp

## **ASSIGNMENTS**

### Document the Notification Endpoint for the OpenAPI Document

<img width="960" alt="HW1 notifications" src="https://user-images.githubusercontent.com/64080430/219949125-6f75f2a7-0660-4534-9b1c-d95945a9c247.png">

### Write a Flask Backend Endpoint for Notifications

<img width="580" alt="HW1 backend endpoint" src="https://user-images.githubusercontent.com/64080430/219949130-b621c885-ef69-4f63-8d57-1ac87956235a.png">

### Write a React Page for Notifications

<img width="859" alt="HW1 frontend endpoint" src="https://user-images.githubusercontent.com/64080430/219949133-bcc0ca54-e50b-4700-bd56-259090a3ae81.png">

### Run DynamoDB Local Container and ensure it works

<img width="960" alt="HW wk1 pt2 dynamoDB local" src="https://user-images.githubusercontent.com/64080430/221187140-c98ec391-566d-4d8c-8d01-2912ed4600ac.png">

### Run Postgres Container and ensure it works

<img width="960" alt="HW wk1 pt2 postgres" src="https://user-images.githubusercontent.com/64080430/221187156-f6efa472-e2ad-4534-8d97-7929da10aacb.png">

## **EXTRA CHALLENGES**

### Run the dockerfile CMD as an external script

### Push and tag a image to DockerHub (they have a free tier)

### Use multi-stage building for a Dockerfile build

### Implement a healthcheck in the V3 Docker compose file

### Research best practices of Dockerfiles and attempt to implement it in your Dockerfile

### Learn how to install Docker on your localmachine and get the same containers running outside of Gitpod / Codespaces

### Launch an EC2 instance that has docker installed, and pull a container to demonstrate you can run your own docker processes.
