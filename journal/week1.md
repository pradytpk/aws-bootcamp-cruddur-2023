# 1. Week 1 — App Containerization
---------------

- [1. Week 1 — App Containerization](#1-week-1--app-containerization)
  - [1.1. Task List of 19/02/2023 to 25/02/2023](#11-task-list-of-19022023-to-25022023)
  - [1.2. Spending Considerations](#12-spending-considerations)
    - [1.2.1. Gitpod](#121-gitpod)
    - [1.2.2. Codespaces](#122-codespaces)
    - [1.2.3. Cloud9](#123-cloud9)
  - [1.3. Container Security Considerations](#13-container-security-considerations)
    - [1.3.1. What is Container Security?](#131-what-is-container-security)
    - [1.3.2. Why care about cloud security?](#132-why-care-about-cloud-security)
    - [1.3.3. Why container security requires practice](#133-why-container-security-requires-practice)
    - [1.3.4. Container Security Components](#134-container-security-components)
    - [1.3.5. Top 10 Security Best Practices](#135-top-10-security-best-practices)
    - [1.3.6. Tools](#136-tools)
  - [1.4. Containerize Application (Dockerfiles, Docker Compose](#14-containerize-application-dockerfiles-docker-compose)
    - [1.4.1. Backend Docker creation](#141-backend-docker-creation)
      - [1.4.1.1. Run Python](#1411-run-python)
      - [1.4.1.2. Add Dockerfile](#1412-add-dockerfile)
        - [1.4.1.2.1. Docker File Link](#14121-docker-file-link)
        - [1.4.1.2.2. Build the backend container](#14122-build-the-backend-container)
        - [1.4.1.2.3. Run the backend container](#14123-run-the-backend-container)
    - [1.4.2. Frontend Docker creation](#142-frontend-docker-creation)
      - [1.4.2.1. Run NPM Install](#1421-run-npm-install)
      - [1.4.2.2. Create Docker File](#1422-create-docker-file)
        - [1.4.2.2.1. Docker File Link](#14221-docker-file-link)
        - [1.4.2.2.2. Build the Frontend Container](#14222-build-the-frontend-container)
        - [1.4.2.2.3. Run the Frontend Container](#14223-run-the-frontend-container)
    - [1.4.3. Multiple Containers](#143-multiple-containers)
      - [1.4.3.1. Create a docker-compose file](#1431-create-a-docker-compose-file)
  - [1.5. Document the Notification Endpoint for the OpenAI Document](#15-document-the-notification-endpoint-for-the-openai-document)
    - [1.5.1. API Code](#151-api-code)
    - [1.5.2. Open API document preview](#152-open-api-document-preview)
  - [1.6. Write a Flask Backend Endpoint for Notifications](#16-write-a-flask-backend-endpoint-for-notifications)
    - [1.6.1. Notification Backend Response](#161-notification-backend-response)
    - [1.6.2. Notification Backend Code Commit Link](#162-notification-backend-code-commit-link)
  - [1.7. Write a React Page for Notifications](#17-write-a-react-page-for-notifications)
    - [1.7.1. Notification Frontend Screen](#171-notification-frontend-screen)
    - [1.7.2. Notification Frontend Code Commit Link](#172-notification-frontend-code-commit-link)
  - [1.8. Run DynamoDB Local Container and ensure it works](#18-run-dynamodb-local-container-and-ensure-it-works)
    - [1.8.1. Docker setup for DynamoDB](#181-docker-setup-for-dynamodb)
      - [1.8.1.1. Make Sure Docker is Running](#1811-make-sure-docker-is-running)
        - [1.8.1.1.1. Create a table](#18111-create-a-table)
        - [1.8.1.1.2. Create an Item](#18112-create-an-item)
        - [1.8.1.1.3. List Tables](#18113-list-tables)
        - [1.8.1.1.4. Get Records](#18114-get-records)
  - [1.9. Run Postgres Container and ensure it works](#19-run-postgres-container-and-ensure-it-works)
    - [1.9.1. Docker setup for Postgres](#191-docker-setup-for-postgres)
    - [1.9.2. Gitpod client setup for Postgres](#192-gitpod-client-setup-for-postgres)
    - [1.9.3. Postgres Plugin setup check](#193-postgres-plugin-setup-check)
  - [1.10. References](#110-references)
    - [1.10.1. VSCode Docker Extension](#1101-vscode-docker-extension)
      - [1.10.1.1. Return the container id into an Environment variables](#11011-return-the-container-id-into-an-environment-variables)
      - [1.10.1.2. Get Container Images or Running Container Ids](#11012-get-container-images-or-running-container-ids)
      - [1.10.1.3. Send Curl to Test Server](#11013-send-curl-to-test-server)
      - [1.10.1.4. Check Container Logs](#11014-check-container-logs)
      - [1.10.1.5. Debugging  adjacent containers with other containers](#11015-debugging--adjacent-containers-with-other-containers)
      - [1.10.1.6. Gain Access to a Container](#11016-gain-access-to-a-container)
      - [1.10.1.7. Delete an Image](#11017-delete-an-image)
      - [1.10.1.8. Overriding Ports](#11018-overriding-ports)
---------------
## 1.1. Task List of 19/02/2023 to 25/02/2023
---------------
- [x] Watched Grading Homework Summaries(19/02/2023)
- [x] Watched Week 1 - Live Streamed Video(19/02/2023)
- [x] Watched Ashish's Week 1 - Container Security(24/02/2023)
- [x] Week 1 - Containerize Application (Dockerfiles, Docker Compose)(24/02/2023)
- [x] Document the Notification Endpoint for the OpenAI Document(23/02/2023)
- [x] Write a Flask Backend Endpoint for Notifications(23/02/2023)
- [x] Write a React Page for Notifications(23/02/2023)
- [x] Run DynamoDB Local Container and ensure it works(23/02/2023)
- [x] Run Postgres Container and ensure it works(24/02/2023)


---------------
## 1.2. Spending Considerations
---------------
### 1.2.1. Gitpod
- upto 50hrs free
- free 500 credit 
- Monthly renewal

### 1.2.2. Codespaces
 - upto 60hrs free

### 1.2.3. Cloud9
 - t2.micro using free tier
 - Better avoid due to cost related difficulty

---------------
## 1.3. Container Security Considerations
---------------
### 1.3.1. What is Container Security?
- Container Security is the practice of protecting your applicatoins hosted on computer services like containers.
- Common Examples of applications can be SPA, Microservices, API etc

### 1.3.2. Why care about cloud security?
- Container First Strategy
- Cloud Native
- Reducing impact of breach
- Automation can reduce recovery time to known good state fairly easy

### 1.3.3. Why container security requires practice
- Complexity with containers
- Relying on CSPs for features
- UnManaged Requiers a lot more hours of work.

### 1.3.4. Container Security Components
- Docker & Host Configuration
- Security Images
- Secret Management
- Application Security
- Data Security
- Monitoring Containers
- Compliance Frame Works

### 1.3.5. Top 10 Security Best Practices
- Keep Host & Docker Updated to latest security Patches
- Docker daemon & containers should run in non-root user mode
- Image Vulnerability Scanning
- Trusting a Private vs Public Image Registry
- No Sensitive Data in Docker files or Images
- Use Secret Management Services to Share secrets
- Read only File system and Volume for Docker
- Separate databases for long term storage
- Use DevSecOps practices while building application security
- Ensure all Code is tested for vulnerabilities before production use

### 1.3.6. Tools
- Snyk (Open Source Available)
- AWS Secrets Manager  
- Clair / AWS Inspector 
- Hashicorp Vault
---------------
## 1.4. Containerize Application (Dockerfiles, Docker Compose
---------------

### 1.4.1. Backend Docker creation

#### 1.4.1.1. Run Python

```sh
cd backend-flask
export FRONTEND_URL="*"
export BACKEND_URL="*"
python3 -m flask run --host=0.0.0.0 --port=4567
cd ..
```
#### 1.4.1.2. Add Dockerfile

Create a file here: `backend-flask/Dockerfile`

```dockerfile
FROM python:3.10-slim-buster
WORKDIR /backend-flask
COPY requirements.txt requirements.txt
RUN pip3 install -r requirements.txt
COPY . .
ENV FLASK_ENV=development
EXPOSE ${PORT}
CMD [ "python3", "-m" , "flask", "run", "--host=0.0.0.0", "--port=4567"]
```
##### 1.4.1.2.1. Docker File Link
[Dockerfile](https://github.com/pradytpk/aws-bootcamp-cruddur-2023/blob/main/backend-flask/Dockerfile)

##### 1.4.1.2.2. Build the backend container

```sh
docker build -t  backend-flask ./backend-flask
```
![python_docker_build](../_docs/assets/python_docker_build.png)

##### 1.4.1.2.3. Run the backend container
 
```sh
docker run --rm -p 4567:4567 -it backend-flask
```
![python_docker_run](../_docs/assets/python_docker_run.png)


### 1.4.2. Frontend Docker creation

#### 1.4.2.1. Run NPM Install

```
cd frontend-react-js
npm i
```
![npm_version](../_docs/assets/npm_version.png)

#### 1.4.2.2. Create Docker File

Create a file here: `frontend-react-js/Dockerfile`

```dockerfile
FROM node:16.18
ENV PORT=3000
COPY . /frontend-react-js
WORKDIR /frontend-react-js
RUN npm install
EXPOSE ${PORT}
CMD ["npm", "start"]
```
##### 1.4.2.2.1. Docker File Link
[Dockerfile](https://github.com/pradytpk/aws-bootcamp-cruddur-2023/blob/main/frontend-react-js/Dockerfile)


##### 1.4.2.2.2. Build the Frontend Container

```sh
docker build -t frontend-react-js ./frontend-react-js
```
![frontend_docker_build](../_docs/assets/front_docker_build.png)

##### 1.4.2.2.3. Run the Frontend Container

```sh
docker run -p 3000:3000 -d frontend-react-js
```
![frontend_docker_run](../_docs/assets/front_docker_run.png)

### 1.4.3. Multiple Containers

#### 1.4.3.1. Create a docker-compose file

Create `docker-compose.yml` at the root of your project.

```yaml
version: "3.8"
services:
  backend-flask:
    environment:
      FRONTEND_URL: "https://3000-${GITPOD_WORKSPACE_ID}.${GITPOD_WORKSPACE_CLUSTER_HOST}"
      BACKEND_URL: "https://4567-${GITPOD_WORKSPACE_ID}.${GITPOD_WORKSPACE_CLUSTER_HOST}"
    build: ./backend-flask
    ports:
      - "4567:4567"
    volumes:
      - ./backend-flask:/backend-flask
  frontend-react-js:
    environment:
      REACT_APP_BACKEND_URL: "https://4567-${GITPOD_WORKSPACE_ID}.${GITPOD_WORKSPACE_CLUSTER_HOST}"
    build: ./frontend-react-js
    ports:
      - "3000:3000"
    volumes:
      - ./frontend-react-js:/frontend-react-js
networks: 
  internal-network:
    driver: bridge
    name: cruddur
```

---------------
## 1.5. Document the Notification Endpoint for the OpenAI Document
---------------
### 1.5.1. API Code
```yml
  /api/activities/notifications: 
    get:
      description: 'Return a feed of activity for all of those that I follow'
      tags:
        - activities
      parameters: []
      responses:
        '200':
          description: Return array of activities
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/Activity'
```
### 1.5.2. Open API document preview
![notification_openApi](../_docs/assets/notifications_openapi.png)

---------------
## 1.6. Write a Flask Backend Endpoint for Notifications
---------------
### 1.6.1. Notification Backend Response
![notification_backend_response](../_docs/assets/notification_backend_response.png)
### 1.6.2. Notification Backend Code Commit Link
- https://github.com/pradytpk/aws-bootcamp-cruddur-2023/commit/09c8022b6dac0d96811b8ea60735a939a4681e8c

---------------
## 1.7. Write a React Page for Notifications
---------------

### 1.7.1. Notification Frontend Screen
![notification_frontend_screen](../_docs/assets/notification_frontend_screen.png)
### 1.7.2. Notification Frontend Code Commit Link
- https://github.com/pradytpk/aws-bootcamp-cruddur-2023/commit/ebcbc6099122e26bff1b0c166d44a0bd764a454d

---------------
## 1.8. Run DynamoDB Local Container and ensure it works
---------------

### 1.8.1. Docker setup for DynamoDB

```yaml
services:
  dynamodb-local:
    # https://stackoverflow.com/questions/67533058/persist-local-dynamodb-data-in-volumes-lack-permission-unable-to-open-databa
    # We needed to add user:root to get this working.
    user: root
    command: "-jar DynamoDBLocal.jar -sharedDb -dbPath ./data"
    image: "amazon/dynamodb-local:latest"
    container_name: dynamodb-local
    ports:
      - "8000:8000"
    volumes:
      - "./docker/dynamodb:/home/dynamodblocal/data"
    working_dir: /home/dynamodblocal
```
```yaml
volumes: 
- "./docker/dynamodb:/home/dynamodblocal/data"
```
#### 1.8.1.1. Make Sure Docker is Running
![dynamodb_docker](../_docs/assets/docker_dynamodb.png)

##### 1.8.1.1.1. Create a table
```
aws dynamodb create-table \
    --endpoint-url http://localhost:8000 \
    --table-name Music \
    --attribute-definitions \
        AttributeName=Artist,AttributeType=S \
        AttributeName=SongTitle,AttributeType=S \
    --key-schema AttributeName=Artist,KeyType=HASH AttributeName=SongTitle,KeyType=RANGE \
    --provisioned-throughput ReadCapacityUnits=1,WriteCapacityUnits=1 \
    --table-class STANDARD
```
![create_table](../_docs/assets/dynamoDB-1.png)

##### 1.8.1.1.2. Create an Item
```
aws dynamodb put-item \
    --endpoint-url http://localhost:8000 \
    --table-name Music \
    --item \
        '{"Artist": {"S": "No One You Know"}, "SongTitle": {"S": "Call Me Today"}, "AlbumTitle": {"S": "Somewhat Famous"}}' \
    --return-consumed-capacity TOTAL  
```
![create_item](../_docs/assets/dynamoDB-2.png)
##### 1.8.1.1.3. List Tables
```
aws dynamodb list-tables --endpoint-url http://localhost:8000
```
![list_table](../_docs/assets/dynamoDB-3.png)
##### 1.8.1.1.4. Get Records
```
aws dynamodb scan --table-name Music --query "Items" --endpoint-url http://localhost:8000
```
![get_record](../_docs/assets/dynamoDB-4.png)

---------------
## 1.9. Run Postgres Container and ensure it works
---------------
### 1.9.1. Docker setup for Postgres
```yaml
services:
  db:
    image: postgres:13-alpine
    restart: always
    environment:
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=password
    ports:
      - '5432:5432'
    volumes: 
      - db:/var/lib/postgresql/data
volumes:
  db:
    driver: local
```

```yaml
volumes: 
  - db:/var/lib/postgresql/data
volumes:
  db:
    driver: local
```
![Postgres_docker_Setup](../_docs/assets/docker_postgresdb.png)

### 1.9.2. Gitpod client setup for Postgres

```sh
  - name: postgres
    init: |
      curl -fsSL https://www.postgresql.org/media/keys/ACCC4CF8.asc|sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/postgresql.gpg
      echo "deb http://apt.postgresql.org/pub/repos/apt/ `lsb_release -cs`-pgdg main" |sudo tee  /etc/apt/sources.list.d/pgdg.list
      sudo apt update
      sudo apt install -y postgresql-client-13 libpq-dev
```
![Postgres_Client_Setup](../_docs/assets/dataconnection_postgresclient.png)

### 1.9.3. Postgres Plugin setup check
![plugin_check](../_docs/assets/dataconnection_postgres.png)

---------------
## 1.10. References
---------------
Good Article for Debugging Connection Refused
https://pythonspeed.com/articles/docker-connection-refused/

###  1.10.1. VSCode Docker Extension

Docker for VSCode makes it easy to work with Docker

https://code.visualstudio.com/docs/containers/overview

> Gitpod is preinstalled with theis extension

```sh
FRONTEND_URL="*" BACKEND_URL="*" docker run --rm -p 4567:4567 -it backend-flask
export FRONTEND_URL="*"
export BACKEND_URL="*"
docker run --rm -p 4567:4567 -it -e FRONTEND_URL='*' -e BACKEND_URL='*' backend-flask
docker run --rm -p 4567:4567 -it  -e FRONTEND_URL -e BACKEND_URL backend-flask
unset FRONTEND_URL="*"
unset BACKEND_URL="*"
docker container run --rm -p 4567:4567 -d backend-flask
```

#### 1.10.1.1. Return the container id into an Environment variables

```sh
CONTAINER_ID=$(docker run --rm -p 4567:4567 -d backend-flask)
```

#### 1.10.1.2. Get Container Images or Running Container Ids

```
docker ps
docker images
```


#### 1.10.1.3. Send Curl to Test Server

```sh
curl -X GET http://localhost:4567/api/activities/home -H "Accept: application/json" -H "Content-Type: application/json"
```

#### 1.10.1.4. Check Container Logs

```sh
docker logs CONTAINER_ID -f
docker logs backend-flask -f
docker logs $CONTAINER_ID -f
```

####  1.10.1.5. Debugging  adjacent containers with other containers

```sh
docker run --rm -it curlimages/curl "-X GET http://localhost:4567/api/activities/home -H \"Accept: application/json\" -H \"Content-Type: application/json\""
```

busybosy is often used for debugging since it install a bunch of thing

```sh
docker run --rm -it busybosy
```

#### 1.10.1.6. Gain Access to a Container

```sh
docker exec CONTAINER_ID -it /bin/bash
```

> You can just right click a container and see logs in VSCode with Docker extension
#### 1.10.1.7. Delete an Image

```sh
docker image rm backend-flask --force
```

> docker rmi backend-flask is the legacy syntax, you might see this is old docker tutorials and articles.
> There are some cases where you need to use the --force
#### 1.10.1.8. Overriding Ports

```sh
FLASK_ENV=production PORT=8080 docker run -p 4567:4567 -it backend-flask
```

> Look at Dockerfile to see how ${PORT} is interpolated

---------------