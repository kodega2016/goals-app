Lets create a docker network for this application

```bash
docker network create goals_app_net
```

After that create a docker container for mongo db container within the network we just created

```bash
docker container run -d --name goals_app_db --network goals_app_net mongo
```

now create docker container for the backend application

```bash
docker image build -t goals_app_backend ./backend
docker container run -d --name goals_app_backend --network goals_app_net goals_app_backend
```

now create docker container for the frontend application

```bash
docker image build -t goals_app_frontend ./frontend
docker container run -d --name goals_app_frontend --network goals_app_net -v $(pwd):/app -v /app/node_modules goals_app_frontend
```
