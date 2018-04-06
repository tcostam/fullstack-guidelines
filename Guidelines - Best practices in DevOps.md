# Guidelines: Best practices in DevOps

## Configuring EC2 instances

## Configuring a Load Balancer

## Configuring Cloudformation

## Amazon ECR Cleanup

There is a limit of images in ECR.
https://github.com/awslabs/ecr-cleanup-lambda

## Debugging an Amazon Environment

When using a t2.large instance, the amount of resources available is
8GB memory and 2 computing units (equivalent to 2048 mhz cpu).

Pay attention to the health check configuration, because when considered unhealthy, an instance is removed from a load balancer.

Inside an EC2 instance, run:

`docker stats`

to see the amount of resources the docker containers are using.
When maxed, the use of this resources can stop a service and make amazon kill an instance.

`docker ps -a` will give you the images created in docker

if you need to enter an exited container for debugging, commit it with:

`docker commit $CONTAINER_ID $NAME`

and enter it using:

`docker run -it $NAME bash`
