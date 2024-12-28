# `DOCKER`

- [DOCKER](#docker)
    - [why Docker is needed](#why-docker-is-needed)
    - [containers](#containers)
    - [difference between Containers & VM](#difference-between-containers--vm)
    - [Docker images](#docker-images)
- [SETTING UP DOCKER](#setting-up-docker)
    - [Linux](#linux)
    - [windows](#windows)
        - [docker tool box](#docker-tool-box)
        - [docker desktop for windows](#docker-desktop-for-windows)
        - [container types (2 types)](#container-types-2-types)
- [COMMANDS](#commands)
    - [show version](#show-version)
    - [create ,stop or remove a container](#create-stop-or-remove-a-container)
    - [show exited & running containers](#show-exited--running-containers)
    - [pull or remove an image](#pull-or-remove-an-image)
    - [remove all images](#remove-all-images)
    - [delete all containers](#delete-all-containers)
- [Docker Run](#docker-run)
    - [Run-names](#run-names)
    - [append & exec a command](#append--exec-a-command)
    - [Run-stdin](#run-stdin)
    - [Run - attach & detach](#run---attach--detach)
    - [Run-tags](#run-tags)
    - [Run-PORT mapping|publishing](#run-port-mappingpublishing)
    - [Run-Volume mapping](#run-volume-mapping)
    - [attach a container to a network](#attach-a-container-to-a-network)
    - [inspecting containers details & logs](#inspecting-containers-details--logs)
- [CREATING IMAGES](#creating-images)
    - [steps of creating a docker image](#steps-of-creating-a-docker-image)
    - [create docker image](#create-docker-image)
    - [publish a docker image](#publish-a-docker-image)
    - [chek image history](#chek-image-history)
    - [failure & cached layers](#failure--cached-layers)
- [ENVIRONMENT VARIABLES](#environment-variables)
    - [setting up environment vars](#setting-up-environment-vars)
    - [show container's env vars](#show-containers-env-vars)
- [COMMANDS & ENTRYPOINTS](#commands--entrypoints)
    - [Commands](#commands)
    - [Entrypoints](#entrypoints)
    - [missing operand](#missing-operand)
    - [overriding Entrypoints](#overriding-entrypoints)
- [DOCKER COMPOSE](#docker-compose)
    - [installing docker compose](#installing-docker-compose)
    - [setting up docker compose](#setting-up-docker-compose)
    - [voting app](#voting-app)
    - [run the app stack (yml file)](#run-the-app-stack-yml-file)
    - [docker compose build](#docker-compose-build)
    - [docker compose versions](#docker-compose-versions)
    - [docker compose networks](#docker-compose-networks)
    - [docker compose enivironmet](#docker-compose-enivironmet)
    - [docker compose entrypoint & command](#docker-compose-entrypoint--command)
- [DOCKER REGISTRY](#docker-registry)
    - [private regitry](#private-regitry)
    - [deploy a private regitry](#deploy-a-private-regitry)
- [DOCKER ENGINE ,STORAGE & NETWORK](#docker-engine-storage--network)
    - [docker engine](#docker-engine)
        - [containerazation](#containerazation)
        - [list container's processes](#list-containers-processes)
    - [docker storage](#docker-storage)
        - [volumes](#volumes)
        - [show docker's information](#show-dockers-information)
        - [show the creation steps of an image](#show-the-creation-steps-of-an-image)
        - [docker system](#docker-system)
    - [docker network](#docker-network)
        - [custom networks](#custom-networks)
        - [inspect networks](#inspect-networks)
        - [embedded dns](#embedded-dns)
- [DOCKER ORCHESTRATION](#docker-orchestration)
    - [docker orchestration](#docker-orchestration)
    - [docker swarm](#docker-swarm)
    - [kubernetes](#kubernetes)
        - [kubernetes components](#kubernetes-components)
        - [kubectl](#kubectl)
                            
## `why Docker is needed` :

    * compatibility/dependency (all different services must be compatible "versions" on the same infrastructure "os")
    * some services may require different versions and libraries of the same dependency
    * long setup time (the project changes over time that requires updating dependency and changing the infrastructure "Matrix-Hell")
    * different Dev/Test/Prod environments (new develpers have to set up thier working environment form scratch wich is tedious)
    * the main purpose of Docker is to package ,contanerize applications ,ship them and run them anywhere   

## `containers` :

    * isolated environments (Processes,Network,Mounts)
    * some kind of virtual machines but all chare the same os kernel 
    * you can run each service on a seperate container with its dependecys and libraries
    * u can run oss on containers as long as they are based on the same kernel as the hosting machine (win containers cant run on a linux infrustructure)

## `difference between Containers & VM` :

    * Virtual Machine (Apps,Libs & Deps,OS) => Hypervisor => Hardware
    * Container(Apps,Libs & Deps) => Docker => OS => Hardware
    * Containers consume less resources unlike VMs
    * Containes & VMs work together (VMs provsion containers wich provisoin apps and scale them this allows of the support of large amount apps running on multiple Docker hosts)
    * Containers are not meant to host an OS ,their are meant to run a specific task or a process (web server ,data-base ,...)
    * once the container completes its task or the process inside of it ,it exits 
 
## `Docker images` :

    * a Docker image is a Package ,Template or Plan (service ,application)
    * containers are running instances of images wich have their own environments
    * create personal images and push it to "Docker Hub" repo
    * Docker images are found in Docker Hub "hub.docker.com"

#                            [`SETTING UP DOCKER`]

* "docs.docker.com" => get Docker => select OS => follow the listed steps

## `Linux` :

    * installing docker using the convinience script is mush easier 
        - curl -fsSL https://get.docker.com -o get-docker.sh
        - sudo sh get-docker.sh --dry-run (show the script steps)
        - sudo sh get-docker.sh (run the script)

## `windows` :

### `docker tool box` :

    * a pack of software that will set up a docker VM on youre win machine
    * this will only run linux containers 

### `docker desktop for windows` :
    
    * same virtualization but with micorsoft's Hyper-V technologie
    * this will run linux containers by default but it's also capable of running windows coantainers (with some config)

### `container types (2 types)` :

    * window server container (kernel is shared with containers like linux)
    * Hyper-V isolation (avry containers runs on its own highly optimised VM with seperate kernels)
    * base images :
        - Windows Server Core
        - Nano Server

#                            [`COMMANDS`]

* higher priveliges are requierd to run docker commands

## `show version` :

    - sudo docker version

## `create ,stop or remove a container` :

    - docker run <image name|id> (run an instance "container" of an image "if the image dosen't exist localy it will be pulled from Docker Hub")
    - docker stop <container name|id>
    - docker rm <container name|id> (delete stoped or a running container)
        - docker rm <id1> <id3> <name4> (specifie multiple containers)
    - docker rm -v -f $(docker ps -qa) (remove all containers)

## `show exited & running containers` :

    - docker ps (show current running containers)
    - docker ps -a (show all containers "running & stoped") 

## `pull or remove an image` :

    - docker pull <image name|id> from Docker Hub"
    - docker rmi <image name|id> 
    - docker images (show current installed images)
        * all runnig instances "containers" of the image must be removed first

## `remove all images` :
    
    - docker image prune -a
    - docker rmi -f $(docker images | grep "<none>" | awk '{print $3}') // <none> images

## `delete all containers` :

    - docker rm -f $(docker ps -aq)
    - docker rm -f $(docker ps -a | grep Exited | awk '{print $1}') //Exited containers
    
#                            [`Docker Run`]

 * containers run under a docker host

## `Run-names` :

    - docker run --name=<custom name> <image name|id> (spcifie container name)

## `append & exec a command` :

    - docker run <image name|id>(ubuntu) <command>
        - docker run -it centos bash (create and enter a centos bash)
    - docker run ubuntu sleep 100 seconds (u can run other commands in this 100s periode)
        - docker exec <container name|id> <command> (append a command to a specified container)
        - docker exec -it <container name|id> bash 

## `Run-stdin` :

    - docker run -i <image name|id> (run in interactive mode)
        * this will make the container listen to inputs
        * add "-t" to attach a terminal (this will print prompts) 

## `Run - attach & detach` :

    * containers run in attached mode (wont let u interact with shell unless u force stop it Crtl+c)
    - docker run -d <image name|id> (run a container in detached mode or in background)
        -docker attach <container name|id> (run a container in the foreground )

## `Run-tags` :

    * tags specifie the image version ,by default the tag is specified as latest
    - docker run <image name|id>:<tag>
        - docker run redis:4.0

## `Run-PORT mapping|publishing` :  

    * a web-app (cantainer) with an ip@ on port 5000 can be accessed via the docker host with an ip@ on port 80 (5000 <=> 80)
    - docker run -p <doker host port>:<container port> <image name|id> 
        - docker run -p 80:5000 hamdi/web-app
        * now a user can access this web-app using "http://docker-host-ip@:80"

## `Run-Volume mapping` :

    * deleting a database container may result in the loss of all its data 
    * volume mapping allows backing up container data under the docker host
    - docker run -v <docker host dir>:<container dir> <image name|id> 
        - docker run /opt/data:/var/lib/mysql mysql
        - docker run -v /home/hamdi/jenkins:/var/jenkins_home -u root jenkins/jenkins
        - docker volume inspect <volume name>

## `attach a container to a network` :

    - docker run --network <network name|@> <image name|id>

## `inspecting containers details & logs` : 

    - docker inspect <container name|id> (show container details)
    - docker logs <container name|id> (show conatiner log)

#                            [`CREATING IMAGES`]

## `steps of creating a docker image` :

* <a href="src/dockerfile instructions.md">Dockerfile Instructions</a>

* example of setting up a web app based on flask :
    - OS (ubuntu)
    - update apt repo
    - install dependencies using apt
    - install python dependencies
    - copy source code to /opt dir
    - run the web server using "flask" command
* a docker file is needed to complete these steps :
* "INSTRUCTION" => "argument"
* it follows a layered architecture (OS => dependencys and tools => source-code => entrypoint)
    - Dockerfile contents :

        FROM Ubuntu

        RUN apt-get update
        RUN apt-get install python3
        RUN pip install python3-flask

        COPY app.py /opt/source-code (copy the app source-code to /opt)
        ENTRYPOINT python3 /opt/source-code (this command will run if a container is created)

## `create docker image `:

    - docker build <path containing the Dockerfile> -t(tag) <account name/web-app>

## `publish a docker image `:
    
    * it's necessary to login to ur account first 
        - docker login
    - docker push <account name/webapp>

## `chek image history` :

    - docker history <image name|id> 

## `failure & cached layers` :

    * docker image layers are cached (the build will continue from the last failed layer)
    * this helpfull when changing the source-code frequintly (lower layers are cached no need to rebuilt only the above layers need to)

#                            [`ENVIRONMENT VARIABLES`]

## `setting up environment vars` :

    * env vars allow adding changes without modifying the source-code
    * it allow modifying the container form outside(host)
    * ur source-code have to read the env var in order to apply changes :
        * in pyhton :
            - import os
            - "var"=os.eniron.get("env var name")
        * js :
            - const "var"=process.env."env var name"
    - docker run -e <environment variable> <image name|id> (this will set up an env var inside the container's OS)
        - docker run -e BG_COLOR=blue hamdiz0/web-app

## `show container's env vars` :
    * env vars can be found under "Env" in the container config :
        - docker inspect <container name|id>

#                            [`COMMANDS & ENTRYPOINTS`]     

## `Commands` :

    * it's possible to pass in commands when running a container :
        -docker run <image name|id> <command>
            - docker ubuntu sleep 5
    * it's possible to make these permenet inside a container by modifing the image (Dockerfile ,both forms are valid) :
        - CMD sleep 5 
        - CMD [<command>,<parameter>] (json format)

## `Entrypoints` :

    * it will run a command when a container is created :
        - ENTRYPOINT ["command with out parameters"] (json format)
        - ENTRYPOINT ["sleep"]
        - docker run <image name|id> <parameter>
            -docker run lazy-ubuntu 60
 
## `missing operand` :

    * this issue will happen when u don't specifie the parameter :
        - docker run lazy-ubuntu "missing parameter"
    * to fix this ,a combination of Entrypoints & Commands is needed (NOITCE:they must be specified in a json format ["cmd|param"]) :
        - ENTRYPOINT ["sleep"]
        - CMD ["60"]

## `overriding Entrypoints` :

    * it's possible to override entrypoints during container runtime :
        - docker run --etrypoint <command> <image name|id> <parameter>
            - docker run --entrypoint sleep2.0 lazy-ubuntu 60

#                            [`DOCKER COMPOSE`] 

* Docker Compose is usefull for setting up porjects with multiple services (containers)

## `installing docker compose` :

    * "https://docs.docker.com" => Docker Compose => install => follow the listed steps
    - curl -SL https://github.com/docker/compose/releases/download/v2.29.1/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose
    
## `setting up docker compose` :

    * create a docker-compose.yml to manage multiple services and specific options needed in one file wish is easier to implement ,run and maintain
    * this is only possible on a single docker host

## `voting app` :

    * this helps understanding app-stack
    |voting-app(Python)|                    |result-app(Node.js)|
            ||                                       /\   
            \/                                       ||
    |in-memory-db(Redis)| => |worker(.NET)| => |db(PostgreSQL)|      

    * creating this app using doker run (naming containers is important):
        - docker run -d --name=redis redis
        - docker run -d --name=db db
        - docker run -d --name=vote -p 5000:80 voting-app
        - docker run -d --name=result -p 5001:80 result-app
        - docker run -d --name=worker worker
    * after running all of these containers ,links must be established for this to work (voting-app needs to recognize the redis db for example):
        - docker run --link <image name|id of the container u want to link>:<container name> <image name|id> 
            - docker run -d --name=vote -p 5000:80 --link redis:redis voting-app (this will create an entry in /etc/hosts of the voting's app container "ip@ redis")
            - docker run -d --name=result -p 5001:80 --link db:db result-app
            - docker run -d --name=worker --link redis:redis --link db:db worker
    * creating this app using docker compose :
        - docker-compose.yml :
            redis:
                image: redis
            db:
                image: db
            vote:
                image: voting-app
                ports:
                    - 5000:80
                links:
                    - redis
            result:
                image: result-app
                ports:
                    - 5001:80
                links:
                    - db
            worker:
                image: worker
                links:
                    - redis
                    - db
            
## `run the app stack (yml file)` :

    - docker-compose up (bring the entire application stack)

## `docker compose build` :
    
    * docker compose build allow building an application stack when some services or parts are not completely developed yet
    * to accoplish this the "image" attribute must be swaped with "build" :
        - docker-compose.yml :
            vote:                 => vote:
                image: voting-app        build: ./vote
        * "./vote" containes source-code (development in progress) and a docker file with instructions to build the docker image

## `docker compose versions` :
    
    * version 1 : (creating this app using docker compose)
    * version 2 : same as version 1 but all of the services must be under a proprity named "services" and the version must be specified 
    * version 2 will eleminate the need for links as it sets up a bridged connection between services automaticly 
        - docker-compose file :
            version: '2'
            services:
                same code as version 1 but without the links part
        * to set dependencys between certain services u can add "depends_on" attribute :
            - docker-compose file :
                vote:
                    depends_on:
                        - redis 
    version 3 : same as version 2 with removed and added features and it has "docker swarm"

## `docker compose networks` :

        * say if we want to split these services into two networks "back-end" and "front-end"
        - docker-compose file :
            version: '2'
            services:
                redis:
                    image: redis
                    networks: 
                        - back-end
                db:
                    image: db
                    networks: 
                        - back-end
                vote:
                    image: voting-app
                    networks: 
                        - back-end
                        - front-end
                ...
            networks:
                - back-end:
                - front-end: 

## `docker compose enivironmet` :

    * u can set a value to an env var inside a container 
    - docker-compose file :
        db:
            image:postgres
            environment:
                POSTGRES_USER: postgres
                POSTGRES_PASSWORD: postgres

## `docker compose entrypoint & command` :

    * u can set up an entrypoint or a command for a container in a docker compose file:
    - docker-compose file :
        lazy-ubuntu:
            image: lazy-ubuntu
            command:"World"  
            entrypoint:["echo","Hello"] (entrypoint: ["sh", "-c", "grep root /etc/passwd"])
        * prints out "Hello World"
        

#                            [`DOCKER REGISTRY`]

## `private regitry` :

    * cloud providers like azure & aws provide a private registry by default when creating an account
    * loging in to a private registry :
        - docker login <private-registry.io>

## `deploy a private regitry` :
    
    * create a custom registry :
        - docker run -d -p 5000:5000 --name <name> --restart <always> <registry name> 
    * pushing an image to the registry :
        - docker image tag <image> <localhost|ip@>:<5000>/<image> (change image tag)
        - docker push <localhost|ip@>:<5000>/<image>
    * pulling an image from a custom registry :
        - docker pull <localhost|ip@>:<5000>/<image>
    * checking pushed images :
        - curl -X GET localhost:5000/v2/_catalog

#                            [`DOCKER ENGINE ,STORAGE & NETWORK`]

## `docker engine` :

    * its basicly a host with docker installed on it
    * Docker Deamon : background process that manages docker object (imges,containersnnetworks,...)
    * REST API : programs can use to talk to the daemon and provide instructions (u can create youre own tools with this api)
    * Docker CLI : command line interface (it uses the Rest API to communicate with the Docker Daemon) 
    * Docker CLI dosen't have to be on the same host (remote docker engine)
        - docker -H=<remote-docker-engine>:<port> run <image name|id>

                        /----------------\
                       /  - Docker CLI    \
    - docker engine =>|   - REST API       | 
                       \  - Docker Deamon /    
                        \----------------/

### `containerazation` :

    * namespace (process id ,network ,mount ...) provide isolation between containers
    * namespace-pid : containers share same resources as the host but the same processes have different ids in the container (a subsystem wich thinks that is has its own processes) and in the host 
        * basicly namespace-pid will providee multiple ids for the same process for the host and the container
    * cgroups (control groups): control the amount of resources allocated for each container
        - docker run --cpus=<value> <image name|id>
            - docker run --cpus=.5 ubuntu (this will ensure that the container won't take up more than 50% of the host cpu resources)
        - docker run --memory=<value&unit> <image name|id>
            - docker run --memory=100m ubuntu (m:megabytes) 

### `list container's processes` :

    - docker exec <container name|id> ps -eaf
    * u can find the same process in the host but with a different pid :
        - ps -eaf | grep <process name>

## `docker storage` :

    * when u install docker on a system ,it creates this folder structure "/var/lib/docker" wich contains multiple dirs used for storage (containers ,image ,volumes)
    * docker saves cache (layered structue) wich saves time and space updating and creating similar layered structure images
    * when an image is built its layers are read only (the only way to modify them is by rebuilding the image) ,when running a built image a new layer is created wich is the container layer ,when the container stops all related files and cjanges of that layer are stoped also

### `volumes` :

    * copy-on-write u can modify files and update image source-code as a copy in the container layer
    * when the container stops all of its layer changes are gone ,that where volumes are needed to add persistant storage for the container
    - docker volume create <volume name>
        * creates a dir named <colume name> under "/var/lib/docker/volumes"
    - docker run -v <volume name>:<path> <image name|id>
        * this will mount the volume inside a specified path in the container
    - docker run \
      --mount type=<type(bind)>,source=<from source>,target=<to target> <image name|id>
    * docker usues different types of storage drivers based on the hosting os (AUFS ,ZFS ,Overlay ,Device Mapper,...)
    * https://docs.docker.com/engine/storage/drivers/select-storage-driver/

### `show docker's information` :

    - docker info 

### `show the creation steps of an image` :

    - docker history <image name|id|id>

### `docker system` :

    * show used space :
        - docker system df (-v show all images)
    * delete unused files :
        - docker system prune
    * Get real time events from the server :
        - docker system events

## `docker network` :

    * when docker is installed three networks are automaticly made (Bridge,None & Host)
    * Bridge : is a default network a container gets attached to (private internal network "172.17.0.0")
    * None ,Host : sepecify network manually
        - docker run <image name|id> --network=none|host
    * when specifying the network as host there will be no need to add port mapping to access internal web services inside the container as it directly posts on the host ,but multiple containers won't share the same port unlike the Bridge network
    * None nerwork basicly isolates the container from any type of network

### `custom networks` :

    * these networks are user defined ,u can create ur own networks other than the "172.17.0.0" :
        - docker network \
            --driver <network-type(bridge)>
            --subnet <network-@ "182.18.0.0/16">
            <network name>

### `inspect networks` :

    * show all networks :
        - docker network ls
    * inspect a network : 
        - docker inspect <container name|id> (network config is under "Networks")
    
### `embedded dns` :

    * a built in dns server "172.0.0.11" that helps containers recognize each other in a network

#                            [`DOCKER ORCHESTRATION`]

## `docker orchestration` :

    * one instance of a service may not be sufficient as it can't handle multiple users so multiple instances are needed (docker rum multiple times) 
    * these instances must be maintained as they can fail
    * the host also must be maintained as it can crash
    * you can build scripts that manages these essus ,maintain all instances of the services and the host
    * container orchestration is basicly a bunsh of tools and scripts that helps you maintain containers in a production environment
    * a platform of multiple hosts that run a large number of containers :
        - docker service create --replicas=100 nodejs (a docker swarm command)
    * some orchestration solution can scale up or down the number of instances based on the number of users ,some will add additional hosts 
    * orchestration solutions may also provide support for advanced networking betwween containers across hosts ,load balancing user requests ,storage sharing ,vonfiguration and security
    * orchestration tools :
        - Docker Swarn
        - Kubernetes
        - Mesos

## `docker swarm` :

    * combine multiple docker machines in a single cluster (nodes + manager) ,it will take care of distrebuting your application instances into seperate hosts for high availability and for load balancing acroos different hardware
    * one host must be designted as the manager and the others will be workers
        - docker swarm init (on the swarm manager)
        - docker swarm join --token <token> (on the workers)
        - docker service create --replicas=<number> <image name|id> (create multiple instances across multiple nodes "workers" ,this type of commands must run on the manager host)
        - docker create service --network <network name|@> <image name|id> 
       
## `kubernetes` :

    * same as swarm like manager host(master) and the nodes ,but it have more features and its the most used
    * run multiple instances :
        - kuberctl run --replicas=<number> <image name|id> 
    * scale up|down :
        - kuberctl scale --replicas=<number> <image name|id> 
    * it can be configured with autoscaling capabilities (POD Autoscalers ,Cluster Autoscalers) based on user load
    * upgrade all instances in a rolling upgrade method (one at a time) :
        - kuberctl rolling-update <image name|id>
    * roll back capabilities in case of failiure :
        - kuberctl rolling-update <image name|id> --rollback
    * allows testing new features of an application by upgrading a certain percantage of instances
    * support for many network and storge vendors

### `kubernetes components` :

    * API server : CLI ,users ,manegment devices (front-end of kubernetes) talk to the API to interact with the kubernetes cluster
    * etcd : key value store (logs and data about the clusters)
    * schedular : distributing work or containers across multiple nodes
    * controllers : the brain behind orchestration
    that maintaines clusters 
    * container runtime : software used to run containers like docker
    * kubelet : an agent responsible for making sure that the containers are running on the nodes as expected 

### `kubectl` :

    * kubectl is a control tool ,it's the kubernetes CLI wich is used to deploy and manage applications on a kubernetes cluster 
    * deploy an application on the cluster :
        - kubectl run <cluster>
    * show cluster info :
        - kubectl cluster-info
    * list all nodes :
        - kubectl get nodes
    * run mutiple instances of an application on multiple nodes :
        - kubectl run <name> --image=<image name|id> --replicas:<number>
    
