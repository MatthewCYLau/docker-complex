# Multi-service Docker Reference Project

This is reference project which "dockerised" multiple services which include:

- Nginx
- React frontend client
- Node backend server
- Postgres database
- Redis cache

Inspired by [this](https://www.udemy.com/course/docker-and-kubernetes-the-complete-guide/) Udemy course by Stephen Grider

Stephen's Github repo for his origin project [here](https://github.com/StephenGrider/multi-docker)

## Build/Run Locally

To build the Docker image , run the following command:

```bash
docker-compose up --build
```

To run the app locally , run the following command:

```bash
docker-compose up # app starts at http://localhost:3050/
```

## Components

This app composes of the following components:

- Nginx
- React frontend client
- Node backend server
- Postgres database
- Redis cache

### Nginx

- Listens on container port 80
- Routes traffic to `/` to the frontend client which is listening on port 3000
- Routes traffic to `/api` to the backend server which is listening on port 5000
- See `/nginx/default.conf`

### React frontend client

- A React app which is listening on port 3000

### Node backend server

- A backend server which is listening on port 5000
- Communicates to PostgreSQL database, and Redis cache

### Postgres database

- Listens on default port 5432

### Redis cache

- Listens on default port 6379
- Communicates to `/worker/index.js`, a worker component which contains business logic in calculating fibonacci numbers

## Deployment to AWS Elastic Beanstalk

- The `Dockerrun.aws.json` provides the container task definitions to deploy a multicontainer Docker app on AWS EB. See AWS EB documentation [here](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/create_deploy_docker_ecs.html#create_deploy_docker_ecs_dockerrun) for more details
- Pulls images from Docker hub (i.e. [my Docker hub](https://hub.docker.com/u/matlau)) as part of deployment
- You may choose to create a Redis cluster on [Amazon ElastiCache](https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/GettingStarted.html) and create a PostgreSQL database instance on [Amazon Relational Database Service (RDS)](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_GettingStarted.CreatingConnecting.PostgreSQL.html)
- Additional steps include:
  - Create a Security Group; add the AWS EB app environment, Redis cluster, and PostgreSQL database instance to the security group
  - Set the Redis cluster, and PostgreSQL database connection endpoints as the `REDIS_HOST`, and `PGHOST` AWS EB environment variable value

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License

[MIT](https://choosealicense.com/licenses/mit/)
