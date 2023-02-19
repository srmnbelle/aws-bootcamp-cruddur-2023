# Week 1 — App Containerization

## **HW Checklist**

- [**REQUIRED**](#assignments)
  - [ ] line 1
- [**EXTRA CHALLENGES**](#extra-challenges)
  - [ ] line 1

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

-

### Pre-recorded | [Top 10 Docker Container Security Best Practices with Tutorial](https://www.youtube.com/watch?v=OjZz4D0B-cA&list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv&index=25)

- TO BE WATCHED

### Pre-recorded | [Week 1 - Create the notification feature (Backend and Front)](https://www.youtube.com/watch?v=k-_o0cCpksk&list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv&index=27)

- TO BE WATCHED

### Pre-recorded | [Week 1 - DynamoDB and Postgres vs Docker](https://www.youtube.com/watch?v=CbQNMaa6zTg&list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv&index=28)

- TO BE WATCHED

## **ASSIGNMENTS**

## **EXTRA CHALLENGES**

### Run the dockerfile CMD as an external script

### Push and tag a image to DockerHub (they have a free tier)

### Use multi-stage building for a Dockerfile build

### Implement a healthcheck in the V3 Docker compose file

### Research best practices of Dockerfiles and attempt to implement it in your Dockerfile

### Learn how to install Docker on your localmachine and get the same containers running outside of Gitpod / Codespaces

### Launch an EC2 instance that has docker installed, and pull a container to demonstrate you can run your own docker processes.
