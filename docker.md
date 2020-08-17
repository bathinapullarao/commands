## Command to login docker container
docker exec -it 6a4f2dba71c2 /bin/bash
1. Container -> Local Host
# Copy file or folder from a docker container to the local file system.
docker cp <containerId>:/file/path/in/container/file /host/local/path/file
2. Local Host -> Container
Copy file or folder from the local file system to a docker container, it works the same.
docker cp /host/local/path/file <containerId>:/file/path/in/container/file
