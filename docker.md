# Command to login docker container
docker exec -it 6a4f2dba71c2 /bin/bash
# docker cp
docker cp containerId:/file/path/in/container/file /host/local/path/file
docker cp /host/local/path/file containerId:/file/path/in/container/file
