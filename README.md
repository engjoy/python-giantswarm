
# Running Python based service on Giant Swarm

Here we show how [suricate](http://www.github.com/engjoy/suricate) can be run using [giantswarm.io](https://www.giantswarm.io). Giant Swarm is a cool solution to run your containerized app in the cloud. Especially the environment & companies concept makes it a compelling solution to do your devops.

## Setup

Setup [swarm](http://docs.giantswarm.io/reference/installation/#linux) command and log-in:

    $ swarm login

Create a company & switch to a dev environment:

    $ swarm company create engjoy
    $ swarm env engjoy/dev

## The basics - pushing the suricate image

Login, build the image (use [this](https://github.com/engjoy/suricate_docker_compose/blob/master/Dockerfile) Dockerfile) and push it up:

    $ sudo docker login https://registry.giantswarm.io
    $ sudo docker build -t registry.giantswarm.io/engjoy/suricate:1.1 .
    $ sudo docker push registry.giantswarm.io/engjoy/suricate:1.1

## Create the swarm configuration

Pretty straight forward - very similar to how you would write a [docker-compose](https://github.com/engjoy/suricate_docker_compose/blob/master/docker-compose.yml) file. See the [references](http://docs.giantswarm.io/reference/swarm-json/) for all the details.

    $ cat swarm.json
    ...

Note that we have not take into account auto-scaling etc. This is just a single user dev environment. It is recommend to use TLS & sth like oauth2 to make suricate multi-tenant and more secure.

## Run it and check status

    $ swarm up
    $ swarm status suricate
    $ swarm stats <instance id>

Now you can visit the URL provided too you to access [suricate](http://www.github.com/engjoy/suricate).

To tear it down & cleanup:

    $ swarm stop
    $ swarm delete

