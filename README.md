# micro-service-sandbox
A repository designed to facilitate local development of micro service applications

### Disclaimer

This project is in its very early stages and will undoubtedly change over time. Once an iteration of the project feels stable, we will move to proper versioning, etc, but for now use at your own risk. It is currently set up to simulate an environment to run through the [Docker Swarm Tutorial](https://docs.docker.com/engine/swarm/swarm-tutorial/)

### Setup

You will need [Vagrant](https://www.vagrantup.com/) and [Virtualbox](https://www.virtualbox.org/wiki/Downloads)

The provided vagrant file will spin up three VM's running [CoreOS](https://coreos.com/). The project in its current state is designed to test and develop with containers provisioned within nodes in a cluster. 

1. `cd` into the root of this project
2. With Vagrant and Virtual box installed, run `vagrant up`
3. run `vagrant status` to check on your newly provisioned vms. 
4. run `vagrant ssh <vm name>` and have fun!

