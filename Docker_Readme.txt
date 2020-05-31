https://www.youtube.com/watch?v=fqMOX6JJhGo
Docker Tutorial for Beginners - A Full DevOps Course on How to Run Applications in Containers

Docker Demo - kodekloud.com/p/docker-labs

pull - Download image
> docker pull nginx
-- --------------------------------------------------

Run - Start a container from image
> docker run nginx

> docker run ubuntu sleep 500

*** Interactive mode : To get std.in on screen ***
> docker run -it <containerName>

*** Tag ***
> docker run redis:4.0

*** Detached Mode ***
> docker run -d kodekloud/simple-webapp

*** Re-attached Mode ***
docker attach <containerId first few characters>

*** Port mapping ***
docker run -p <externalPort>:<internalPort> kodekloud/simple-webapp
docker run -p 80:5000 kodekloud/simple-webapp

*** Volume Mapping ***
> docker run -v <dir outside container>:<dir inside container> mysql
> docker run -v /opt/datadir:/var/lib/mysql mysql

*** Environment Variable : Check this using "docker inspect" cmd ***
> docker run -e APP_COLOR=blue simple-webapp-color
-- --------------------------------------------------

ps - Lists containers and their info

# Get all running containers
> docker ps
CONTAINER ID	IMAGE                 COMMAND                  CREATED      	STATUS    	PORTS                 	NAMES
c7a39ab72331    mayanedms/mayanedms   "entrypoint.sh mayan"    13 months ago	Up 6 hours	0.0.0.0:80->8000/tcp  	mayan-edms
ca78831d6e77    postgres:9.5          "docker-entrypoint.s…"   13 months ago	Up 6 hours	0.0.0.0:5432->5432/tcp	mayan-edms-postgres

# To see all containers (stopped and previously executed)
> docker ps -a
CONTAINER ID   	IMAGE                 COMMAND                  CREATED             STATUS                      PORTS                    NAMES
2c0f5f3a2365   	docker/whalesay       "cowsay boo"             20 minutes ago      Exited (0) 19 minutes ago                            tender_franklin
c7a39ab72331   	mayanedms/mayanedms   "entrypoint.sh mayan"    13 months ago       Up 6 hours                  0.0.0.0:80->8000/tcp     mayan-edms
ca78831d6e77   	postgres:9.5          "docker-entrypoint.s…"   13 months ago       Up 6 hours                  0.0.0.0:5432->5432/tcp   mayan-edms-postgres
-- --------------------------------------------------

inspect - Inspect container (Output is in JSON)
> docker inspect <containerName>
-- --------------------------------------------------

logs Background Container Logs
> docker logs <containerName>

-- --------------------------------------------------
stop - To stop the container
> docker stop <containerId | containerName>

> docker stop mayan-edms
mayan-edms

> docker ps -a
CONTAINER ID        IMAGE                 COMMAND                  CREATED             STATUS                      PORTS               		NAMES
2c0f5f3a2365        docker/whalesay       "cowsay boo"             27 minutes ago      Exited (0) 27 minutes ago                       		tender_franklin
c7a39ab72331        mayanedms/mayanedms   "entrypoint.sh mayan"    13 months ago       Exited (0) 3 minutes ago								mayan-edms
ca78831d6e77        postgres:9.5          "docker-entrypoint.s…"   13 months ago       Up 6 hours                  0.0.0.0:5432->5432/tcp	mayan-edms-postgres
-- --------------------------------------------------

rm - To remove a container
> docker rm <containerId | containerName>
-- --------------------------------------------------

exec - Execute a command
> docker exec <containerName> <command>

> docker exec mayan-edms cat /etc/hosts
-- --------------------------------------------------

images - To list images present on host 

> docker images
REPOSITORY            TAG                 IMAGE ID            CREATED             SIZE
mayanedms/mayanedms   latest              453dcbfe6c6c        14 months ago       1.25GB
postgres              9.5                 77f0128abafc        14 months ago       227MB
docker/whalesay       latest              6b362a9f73eb        5 years ago         247MB
-- --------------------------------------------------

rmi - To remove images
> docker rmi <imageName(REPOSITORY)>

NOTE : Remove all dependent containers first

> docker rmi mayanedms/mayanedms
-- --------------------------------------------------

history - To see layers while image is created
> docker history <imageName>
-- --------------------------------------------------

How to create an image?
											Dockerfile
1. OS-Ubuntu								FROM Ubuntu
2. Update apt repo							RUN apt-get update
3. Install dependencies using apt			RUN apt-get install python
4. Install Python dependencies using pip	RUN pip install flask; RUN pip install flask-mysql
5. Copy source code to /opt folder			COPY . /opt/source-code
6. Run web server using "flask" cmd			ENTRYPOINT FLASK_APP=/opt/source-code/app.py flask run
											> docker build Dockerfile -t nik/my-custom-app
											> docker push nik/my-custom-app

Dockerfile : Instruction + Argument
