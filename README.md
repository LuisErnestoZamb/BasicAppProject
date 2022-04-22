# AWS ECS + asp.NET

## aws cli:
```sh
pip install awscli
```

## esc-cli install:
[http://docs.aws.amazon.com/AmazonECS/latest/developerguide/ECS_CLI_installation.html](http://docs.aws.amazon.com/AmazonECS/latest/developerguide/ECS_CLI_installation.html)

## Config cluster:
```sh
ecs-cli configure --cluster pets --region us-east-1
```

## Defining cluster:
```sh
ecs-cli up --keypair ZambranoQ --capability-iam --size 3 --instance-type t2.micro --security-group sg-0adafc6e --subnets subnet-2fbefb58,subnet-3648cb1d,subnet-e2b13987 --vpc vpc-f26d4797
```

## Create repository on aws:
```sh
aws ecr create-repository --repository-name asp-repo --region us-east-1
```

## Login to aws:
```sh
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 093797997223.dkr.ecr.us-east-1.amazonaws.com
```

## Build the container:
```sh
docker build -t asp-repo .
```

## taging the image:
```sh
docker tag asp-repo:latest 093797997223.dkr.ecr.us-east-1.amazonaws.com/asp-repo:latest
docker push 093797997223.dkr.ecr.us-east-1.amazonaws.com/asp-repo:latest
```

## Optional see repositories:
```sh
aws ecr describe-repositories --region us-east-1
```

## run the machine:
```sh
ecs-cli compose --project-name cat --file ecs.docker-compose.yml service create
ecs-cli compose --project-name cat --file ecs.docker-compose.yml up
ecs-cli compose --project-name cat --file ecs.docker-compose.yml service scale 3
```
