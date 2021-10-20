# mule4docker

**mule4docker** is just an attempt to build a docker container with Mule4 runtime. Once the container has started, you can change a couple of configurations in your own mule app and copy it to apps directory (within container using volume mapping) to run them. The port remains same as long as the app is using Mule domain configurations for HTTP_Listener_Config. 

Note: You will need to download the Mule4 runtime separately from [Mulesoft website](https://www.mulesoft.com/lp/dl/mule-esb-enterprise).

##  Repository Content
This repository includes the following:-
1. Dockerfile
2. A sample Mule4 application (with source embedded)
3. A sample Mule domain JAR Project (with source embedded)
   - Domain files are used for sharing resources (port number in this case) with all the mule applications deployed alongside.
   - In this Dockerfile, the Mule Domain Project has HTTP_Listener_Config set to port 8081 which has been exposed. Now all the applications hosted withing this container can share this same configuration (and hence port). The applications can be segregated by different **Path** value.


## DockerHub
If you just want to see it in action and skip all the nonsense below, the docker image is uploaded at [DockerHub](https://hub.docker.com/r/apurba/mule4docker). 

Docker Pull Command
```bash
docker pull apurba/mule4docker
```


## Creating the docker image
1. Install [Docker Engine](https://docs.docker.com/engine/install/) (duh!)
2. Download the [Mule EE Runtime](https://www.mulesoft.com/lp/dl/mule-esb-enterprise) archive
2. Download **Dockerfile**, **hello-mule.jar** and **docker-mule-common-domain-app.jar** from this repository
4. Copy all 4 files in one directory
5. Make any necessary changes to the *Dockerfile* like:
   - Changing MULE_RUNTIME_ARCHIVE name based on your downloaded version
   - Changing MULE_RUNTIME_FOLDER name based on extracted folder name
   - Optional changes like - changing linux version from Alpine to Ubuntu 
6. Open CLI / Command Prompt and navigate to the directory (with these files)
7. Use following command to build the docker image
  
```bash
docker build . -t apurbagiri/mule4docker
```

## Starting the container

```python
docker run -it --name mule4docker --rm -p 8081:8081 apurbagiri/mule4docker
```

## Push container to DockerHub

```bash
docker tag apurbagiri/mule4docker dockerid/container_name:versiontag
docker push dockerid/container_name:versiontag
```

## Contributing
Pull requests are welcome.

## DISCLAIMER
- This is just a basic Dockerfile to make Mule4 runtime up and running. By no means does it claim to be the best way to achieve this.
- This container could be a RAM hog. 

