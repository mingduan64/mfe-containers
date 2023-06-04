## Getting Started

Clone this repository using 

```shell
git clone https://github.com/vanduc2514/microfe-containers.git
```

Follows the guide below for a specific scenario

### Multiple Remotes Containers

Create containers using Docker Compose

```shell
docker compose -f ./docker/multi/docker-compose.yaml up
```

This command creates these containers, each of theese containers serve multiple frontends from the default static folder of `nginx`.

| Container     | URI                 | Description                                    |
|---------------|---------------------|------------------------------------------------|
|`mfe-container`|http://localhost     |Root container for master view                  |
|`mfe-auth`     |http://localhost:8091|Auth container for authentication view          |
|`mfe-marketing`|http://localhost:8092|Marketing container for displaying category view|
|`mfe-dashboard`|http://localhost:8093|Dashboard container for user dashboard          |   

Access the micro frontends application from the root container at http://localhost

### Single Remote Container

Create containers using Docker Compose

```shell
docker compose -f ./docker/single/docker-compose.yaml up
```

This command creates only one single container `mfe-single` that serve multiple frontends from the default static content folder of `nginx`.

Access the micro frontends application from the root container at http://localhost