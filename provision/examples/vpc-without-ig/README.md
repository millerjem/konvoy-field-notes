### Using an existing VPC without an Internet Gateway

1. Use docker to determine the correct Konvoy image to use.
```
$ docker images | grep konvoy
mesosphere/konvoy v1.1.5
```

2. Run the docker image in interactive mode
```
$ docker run -it --entrypoint /bin/sh mesosphere/konvoy:v1.1.5
```

3. Open another terminal and run docker to locate process id
```
$ docker ps | grep konvoy
```

4. Use the docker process id to copy the default aws terraform files
```
$ docker cp 1c7db0e41238:/opt/konvoy/providers/aws .
```

5. Modify the desired files
```
$ vi aws/main.tf
```
Or use the example files in the extras/provisioner directory

6. Copy the modified file to extras/provisioner inside the konvoy cluster directory
```
$ mkdir -p extras/provisioner
$ cp aws/main.tf extras/provisioner
```
Or copy the example files in the extras/provisioner directory

7. Run konvoy to provision AWS
```
$ konvoy provision -y
```

