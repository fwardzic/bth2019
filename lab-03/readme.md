# LAB 03 - creating docker swarm

### Initiate swarm and deploy simple hello world app

Add 2 more instances in PWD

https://labs.play-with-docker.com/

1. Initiate swarm manager

`docker swarm init --advertise-addr <IP_addr_node1>`

2. On node2 and node3 execute join command to add them to the swarm cluster.

3. Check status of swarm nodes on master

`docker node ls`

4. Use docker service to create new app:

`docker service create --name hi_world --replicas 2 ubuntu /bin/sh -c "while true; do echo hello world; sleep 1;done"`

check status:

`docker service ls`

5. Scale your service

`docker service scale hi_world=3`

check status:

`docker service ls`

`docker sercice ps <container_id>`

### Adding two tier app and scale web service:

1. Create overlay network segment

`docker network create -d overlay overlay-net1`

2. create new service for redis DB and web app:

`docker service create --name redis --network overlay-net1 redis:alpine`
 
`docker service create --name web --network overlay-net1 -p 8080:5000 fwardzic/bth-web-app:v1`

Test output:

`while true; do curl 127.0.0.1:8080; sleep 1; done`

3. You will see output only from one container ID. Scale it to 5.

`docker service scale web=10`

4. open separate terminal and ssh to your docker master node.

`while true; do curl 127.0.0.1:8080; sleep 1; done`

5. perform rolling update:

`docker service update --update-parallelism 1 --update-delay 5s --image fwardzic/bth-web-app:v2 web`

Keep watching responses from web-server in terminal with curl requests