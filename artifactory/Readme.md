# Volumes

Artifactories data, logs and backup directories are exported as volumes:
```
/artifactory/data
/artifactory/logs
/artifactory/backup
```

# Ports

The web server is accessible through port 8080.

Example

To run artifactory do:
```bash
docker run -p 8080:8080 mattgruter/artifactory
Now point your browser to http://localhost:8080.
```

# Runtime options

Inject the environment variable RUNTIME_OPTS when starting a container to set Tomcat's runtime options (i.e. CATALANA_OPTS). The most common use case is to set the heap size:
```
docker run -e RUNTIME_OPTS="-Xms256m -Xmx512m" -P mattgruter/artifactory
Switching to Artifactory Pro
```
If you are using Artifactory Pro, the artifactory war archive has to be replaced. The Dockerfile includes a ONBUILD trigger for this purpose. Unpack the Artifactory Pro distribution ZIP file and place the file artifactory.war (located in the webapps subdirectory) in the same directory as a simple Dockerfile that extends this image:

# Dockerfile for Artifactory Pro
FROM mattgruter/artifactory
Now build your child docker image:

```
docker build -t yourname/myartifactory
```

The ONBUILD trigger makes sure that your artifactory.war is picked up and applied to the image upon build.

```
docker run -P yourname/myartifactory
```

# Using Boot2Docker
  ```
  for i in {10000..10999}; do
      VBoxManage modifyvm "boot2docker-vm" --natpf1 "tcp-port$i,tcp,,$i,,$i";
      VBoxManage modifyvm "boot2docker-vm" --natpf1 "udp-port$i,udp,,$i,,$i";
  done
  ```
