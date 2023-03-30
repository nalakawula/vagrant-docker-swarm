# What
Vagrantfile to setup docker swarm with 3 manager node and 3 worker node.

# How
## Bring up the virtual machine
1. `vagrant up`
2. `vagrant status`

## Config docker swarm manager01
1. `vagrant ssh manager01`
2. `docker swarm init --advertise-addr 192.168.57.1`
3. `docker swarm join-token manager`
4. Copy the manager join command
5. `docker swarm join-token worker`
6. Copy the worker join command


## Join manager02 and manager03 to swarm
### manager02
1. `vagrant ssh manager02`
2. `docker swarm join --token <random-token> 192.168.57.1:2377`

### manager03
1. `vagrant ssh manager03`
2. `docker swarm join --token <random-token> 192.168.57.1:2377`

## Join worker01, worker02, and worker03 to swarm
### worker01
1. `vagrant ssh worker01`
2. `docker swarm join --token <random-token> 192.168.57.1:2377`

### worker02
1. `vagrant ssh worker02`
2. `docker swarm join --token <random-token> 192.168.57.1:2377`

### worker03
1. `vagrant ssh worker03`
2. `docker swarm join --token <random-token> 192.168.57.1:2377`

## Check node status
1. `vagrant ssh worker01`
2. `docker node ls`