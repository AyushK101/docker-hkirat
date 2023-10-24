https://docs.docker.com/reference/

## why containerization ?
- everyone has different OS , steps to run a project can vary based on OS 
- extremely hard to keep track of dependencies as project grows 
- what if there was a way to describe your projects configuration in a single file ? DOCKERFILE 
- what if that could be run in an isolated environment ?
- makes local setup of open source projects a breeze 
- makes installing auxiliary services easy like kakfa , node.js etc 

## what is containerization ?
- containerization is building self-sufficient software packages that perform consistently , regardless of the machines they run on.
- it's basically taking the snapshot fo a machine , the filesystem and letting you use and deploy it as a construct .

## history of DOCKER 
- introduced in 2014 , caught fire in 2015 onwards 
- most open source projects have docker files (rightfully so)
- makes your life easy when you're setting up the project locally 
- makes it easier to deploy containers 
- __allows for containers orchestration which makes deployment a breeze .__

## inside docker 
1. cli : run command : `docker`
2. engine 
3. registry (ducker hub)(like github)


## images vs containers 
- a docker "image" behaves like a template from which consistent (will give same output on all machine ex: linux , windows etc) containers can be created . If docker was a traditional virtual machine , the image could be likened to the ISO used to install your VM.
This isn't a robust comparison , as docker differs from VMs in terms of both concept and implementation , but it's a useful starting point nonetheless.

- images define the initial filesystem state of new containers . They bundle your application's source code and its dependencies into a self-contained package that's ready to use with a container runtime . Within the image , filesystem content is represented as multiple independent layers. 

>  image in execution is called container .
> when we open our project on local like `localhost.342342.443.jhg` but when you expose things on internet , it starts with `https:` etc and if we want to deploy we have to create a http server .


## download docker images from docker-hub
- `docker pull <file-name>` or simply copy from that particular image webpage.
- `docker images` : to see total images 
- `docker ps ` :
- `docker login` 

## creating image 
- `docker build . -t <image-tag-name>` __inside project folder in cli__ | will bring the node.js base image locally to my machine , copy code , npm  , expose (1,2,3,4)

# create a container (image to container)
- `docker run <tag-name>` > not recommended 
- OR `docker run -p 3000:3000 <image-tag-name>` 3000(host machine port) from my machine should point to 3000(container port) on the container .


## pushing to docker-hub
- `docker push <image-tag-name>`

## cashing and layers 
- why layers ?
1. caching 
2. re-using layers 
3. faster build times 

> for majority of things you can find alpine version of them , which are much more light-weight 

## volumes and networks 
- another use case of docker : docker is used to run DBs / Redis / Auxiliary services locally.
- this is useful so we don't pollute our filesystem with unnecessary dependencies .
- we can bring up and down DBs / Redis / kafka and clean out our machine .

### there are problem  
- we want local database to retain information across restarts (`volumes`) 
- we want to allow one docker container to talk to another docker container (`networks`)

## volumes 
- a volume is a logical place inside docker , where you can put a data of the container 
- used for persisting data across starts 
- Specifically useful for things like databases 

> how?
- `docker volume create volume_database`way to create volume .
- `docker run -v volume_database:/data/db -p 27017:27017 mongo `  command to start mongoDB container but with its data mounted to this volume .
- `-p 27017:27017 mongo` mapping local host 
- `-v volume_database:/data/db` volume_database  mapping-on   /data/db
-`/data/db` is where mongo dumps its data inside that container , {will be different for different DBs} and it is under mongo container . 
> `mongoDB compass`: a powerful GUI for querying, aggregating, and analyzing your MongoDB data in a visual environment. help in practice volumes 


## networks 
- what we are gonna do is , start the backend application inside a container and make one database container and make them talk to each other .
- 