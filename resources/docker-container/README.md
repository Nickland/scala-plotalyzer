# Docker Container for the scala-plotalyzer

This container provides the working environment for the Plotalyzer in a Docker container.

## Steps

### Build Container

```bash
DOCKER_BUILDKIT=1 docker build --ssh default -t [env_name] . || docker image prune -a
```

And delete directly if an error occurs.

### Start

Start Container:
```bash
sudo docker run -it --rm \
    # Path to the folder in which we want to have the output.
    # Otherwise we create the output, but delete it after leaving the folder
    -v /path/to/analysis/output/folder/:/path/to/analysis/output/folder/ \
    -e DATABASE_URL="[user]://[host_gateway_docker_container]:[db_port]/[db_name]" \
    [env_name]:latest
```

### Useful Information

Here I am writing down some information that was important to me.

#### Database

In file postgresql.conf listen for all addresses: listen_addresses = '*'.
In file pg_hba.conf add entry: host all all 172.17.0.0/16 trust.

#### Docker

Stop container:
```bash
docker stop [container]
```

See all containers:
```bash
docker ps -a
```

Delete container:
```bash
sudo docker rm name
```

Delete all failed builds:
```bash
docker image prune -a
```

See docker images:
```bash
docker images
```

Delete docker images:
```bash
docker rmi [env]
```
