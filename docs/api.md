## DB
modelation

## Endpoints
!!swagger-http https://atnog-crowdwire1.av.it.pt/api/v1/openapi.json!!

## redis
falar por alto, copiar do relatorio

## websocket
mostrar endpoints

## rabbitmq
mostrar topicos

## How to run locally:

To run the REST API make sure to have Poetry installed first:

```
$ pip3 install poetry
```

Make sure to have Redis, RabbitMQ and PostgreSQL up and running.

PostgreSQL Installation through Docker:

```
$ docker run -P -p 127.0.0.1:5432:5432 -e POSTGRES_PASSWORD="1234" --name pg postgres
```

Redis and RabbitMQ can be installed through the following script, which runs two `docker-compose` files, that use images belonging to [Bitnami](https://bitnami.com/)

```
$ cd api
$ sudo bash ./build-docker.sh
```

**NOTE**: Do not use directly the Redis configuration on production, since it can lead to data inconsistencies on a Sentinel Failure. For more Information Check the [Bitnami Documentation](https://github.com/bitnami/bitnami-docker-redis-sentinel)

Install the dependencies on the `poetry.lock` file and start Uvicorn Server

```
$ poetry install
$ poetry run uvicorn --host=0.0.0.0 app.main:app	
```

Additional notes may be checked on the `api `folder.
