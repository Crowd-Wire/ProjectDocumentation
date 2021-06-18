## DB Modelation
To model our database we used the following diagram:



## ![Relational_Schema](./assets/Images/Database Modelation/Relational_Schema.png)Endpoints
!!swagger-http https://atnog-crowdwire1.av.it.pt/api/v1/openapi.json!!

## Redis
For integration with redis we used [aioredis](https://aioredis.readthedocs.io/en/latest/), therefore all operations are
being ran on a asynchronous loop. Great part of PostgreSQL queries are stored in redis, as a way to cache the query. Besides this
all information about users in a world are stored on Redis, following the next pattern, as a key:
- `world:{world_id}:user:{user_id}`, where `{world_id}`is the ID of a world, and `{user_id}`the ID of a user.

The values stored for keys of the previous pattern can be the user's username, choosen avatar and current position on the world's Map.


## Websockets
User events when inside a world in the client interface are sent using websockets. It allows a stateful and faster connection between the API and the client. The API server then makes the calculations in order to ensure that the everything the interface works smoothly.  
Only one Websocket endpoint is being used, which is:
```
/ws/{world_id}?token={AUTHENTICATION_TOKEN}
```
- `{world_id}`, the ID of the world where the WebSocket is being connected.
- `{AUTHENTICATION_TOKEN}`, the token provided by the API.

The content of a WebSocket Message should be in JSON format and have at least: the following content:

```json
{
    "topic": '{TOPIC_NAME}'
}
```

The `{TOPIC_NAME}`, should be one of the following:

```python
class WebsocketProtocol:
    PING = 'PING'
    PONG = 'PONG'
    SEND_MESSAGE = 'SEND_MESSAGE'
    JOIN_PLAYER = 'JOIN_PLAYER'
    LEAVE_PLAYER = 'LEAVE_PLAYER'
    JOIN_CONFERENCE = 'JOIN_CONFERENCE'
    LEAVE_CONFERENCE = 'LEAVE_CONFERENCE'
    PLAYER_MOVEMENT = 'PLAYER_MOVEMENT'
    PLAYERS_SNAPSHOT = 'PLAYERS_SNAPSHOT'
    CHANGE_ROOM = 'CHANGE_ROOM'
    WIRE_PLAYER = 'WIRE_PLAYER'
    MESSAGE_TO_ALL = 'ALL'
    MESSAGE_TO_NEARBY = 'NEARBY'
    REQUEST_TO_SPEAK = 'REQUEST_TO_SPEAK'
    PERMISSION_TO_SPEAK = 'PERMISSION_TO_SPEAK'
    GET_ROOM_USERS_FILES = 'GET_ROOM_USERS_FILES'
    REMOVE_ALL_USER_FILES = 'REMOVE_ALL_USER_FILES'
    DOWNLOAD_REQUEST = 'DOWNLOAD_REQUEST'
    DENY_DOWNLOAD_REQUEST = 'DENY_DOWNLOAD_REQUEST'
    ADD_USER_FILES = 'ADD_USER_FILES'
    ACCEPT_DOWNLOAD_REQUEST = 'ACCEPT_DOWNLOAD_REQUEST'
    START_DOWNLOAD = 'START_DOWNLOAD'
    REMOVE_USER_FILE = 'REMOVE_USER_FILE'
    UNWIRE_PLAYER = 'UNWIRE_PLAYER'
    JOIN_AS_NEW_PEER = 'join-as-new-peer'
    ADD_SPEAKER = 'add-speaker'
    JOIN_AS_SPEAKER = 'join-as-speaker'
    ACTIVE_SPEAKER = 'active_speaker'
    CONNECT_TRANSPORT = '@connect-transport'
    GET_RECV_TRACKS = '@get-recv-tracks'
    CONNECT_TRANSPORT_SEND_DONE = '@connect-transport-send-done'
    SEND_TRACK = '@send-track'
    SEND_FILE = '@send-file'
    CLOSE_MEDIA = 'close-media'
    TOGGLE_PRODUCER = 'toggle-producer'
    TOGGLE_PEER_PRODUCER = 'toggle-peer-producer'
    KICKED = 'KICKED'
    SPEAKING_CHANGE = 'speaking_change'
```



## Rabbitmq
We used [aio-pika](https://aio-pika.readthedocs.io/en/latest/) to integrate rabbitMQ with our API, taking advantage of the fact that FastAPI is asynchronous. Communication between MediaSoup server and FastAPI is made using rabbitMQ.


Also rabbitMQ is used to share information between the API replicas created by kubernetes. Each of the replicas is consumer and producer in the `replicas queue`. Here we are using `FANOUT` exchange in order to broadcast the message to every replica. 

The different protocols used in the rabbitMQ channels are present in the `RabbitProtocol` class:

```python
class RabbitProtocol:
    GET_RECV_TRACKS_DONE = '@get-recv-tracks-done'
    SEND_TRACK_SEND_DONE = '@send-track-send-done'
    SEND_FILE_SEND_DONE = '@send-file-send-done'
    CONNECT_TRANSPORT_RECV_DONE = '@connect-transport-recv-done'
    CONNECT_TRANSPORT_SEND_DONE = '@connect-transport-send-done'
    YOU_JOINED_AS_PEER = 'you-joined-as-peer'
    YOU_JOINED_AS_SPEAKER = 'you-joined-as-speaker'
    YOU_ARE_NOW_A_SPEAKER = 'you-are-now-a-speaker'
    NEW_PEER_PRODUCER = 'new-peer-producer'
    NEW_PEER_DATA_PRODUCER = 'new-peer-data-producer'
    ERROR = 'error'
    CREATE_NEW_REPLICA = 'CREATE_NEW_REPLICA'
```


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
