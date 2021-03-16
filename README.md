# Capstone

### Project Overview
The project deploys three replicas of a docker container image in a AWS Kubernetes Cluster

### Project Tasks

* Code lint [not working](files/lint_error.pdf) and [working](files/lint_success.pdf ) 
* [Docker image](https://hub.docker.com/r/fabioj/capstone-project) pushed by the Jenkins pipeline
* [Complete Jenkins pipeline](files/complete_pipeline.pdf) with docker image deployed using rolling update
* [EC2 instances](files/eks_instances.png) created using the command
``` eksctl create cluster --region us-east-2 --name capstone-project --nodes-min 3 --nodes-max 3 --node-type t2.micro ``` 
