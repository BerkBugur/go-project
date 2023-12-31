# Go-Project

This project is a RESTful API written in Go. It offers a simple and effective solution for task management. Users can create, update, delete and list tasks.

## Requirements

This section lists the requirements to run the project on your local machine

- You need to install [Go](https://go.dev/dl/)
```bash
Checking for any error

go version
```

- You need to install [Docker](https://docs.docker.com/get-docker/) and [Docker Compose](https://docs.docker.com/compose/)
```bash
Checking for any error

docker version
docker compose version
```

- Clone this source code your machine.

- If you are going to run the application over the cloud (e.g. AWS), **Allow Ports** in the security group so that the services can communicate with each other.

## While starting

In the **Project Directory**, you need to build first after that can run:

`docker compose build`

`docker compose up -d`

and wait some tine for build docker images  then 4 service will be start.
```bash
  [+] Running 4/4
 ✔ Container postgres                Started                               0.0s
 ✔ Container go-project-my-app-1     Started                               0.0s
 ✔ Container go-project-promethus-1  Started                               0.0s
 ✔ Container go-project-grafana-1    S...                                  0.0s

```
## API Documentation
Swagger 2.0 was used for documentation. You can view all APIs from the link below.

`http://<your-ip>:8080/swagger/index.html`

If not shown correctly 
`` swag init --parseDependency true ``

## Testing
Go to controllers folder setup your test db. Can easily create [ElephantSQL](https://www.elephantsql.com/). After set your test database 

`go test`


## Logging and Monitoring

### Monitoring

Grafana and Prometheus were used for monitoring. You can follow the instructions below to visualize and see metric data.

**Prometheus collects metrics**

``http://<your-ip>:8081/metrics ``

**Prometheus page**

``http://<your-ip>:9090/graph``


**Grafana login page**

*username: admin - pass: admin*

``http://<your-ip>:3000/login`` 


<img src="https://github.com/BerkBugur/go-project/assets/56639375/7b736462-dbad-4919-8465-56b59049f152" width=100% height=70%>


### Logging
You can see the app.log file in the directory or we can connect to the container and see it. For this, we connect to the my-app container and then we can read the file.

```bash
docker exec -it go-project-my-app-1 /bin/sh

cat app.log
```

<img src="https://github.com/BerkBugur/go-project/assets/56639375/0a91534b-3560-45db-9843-095f559c4f3f" width=60% height=40%>

## Project Security and JWT Usage

In this project, certain endpoints are secured using JSON Web Tokens (JWT). JWT usage provides protection against unauthorized access by users. Below is a step-by-step guide on how to securely access these endpoints:

- To test these processes, you can use tools such as Postman for managing API requests, or you can use the integrated Swagger interface in your project.
### Sign up Login and Test
- You need to register as a user in the system. To do this, send a POST request to the following endpoint:

  ``http://<your-ip>:8080/users/signup ``

- To log in to the system, send a POST request to the following endpoint:

  ``http://<your-ip>:8080/users/login ``

  > *Upon this request, you will be provided with a JWT token. This token stored as a **COOKIE**. If you encounter any issues with cookies, you can use the returned token for your tests.*

- To verify your login, send a GET request to the following endpoint to check the validity of the token:

  ``http://<your-ip>:8080/users/validate ``

### Example Usage

Once you complete the login process, you can access secure endpoints. If you do not log in, you will receive a "401 unauthorized" For example, to get a paginated task list:

``http://<your-ip>:8080/tasks/paged?page=1&size=10``

This request will return the first 10 tasks.

**For shut down this project go project directory**


``docker compose down``
