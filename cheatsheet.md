## This was done from an ec2 instance cloned from an EC2 instance in a ECS cluster

A) How to pull a docker image manually from the AWS repository

$ aws configure
   // Enter value only for region:  eu-west-1  **We had AWS SAML Onelogin authenticated via AD

$ eval $(aws ecr get-login --no-include-email | sed 's|https://||')   // From https://forums.docker.com/t/docker-push-to-ecr-failing-with-no-basic-auth-credentials/17358/7

$ aws ecr describe-repositories    // If all is good list of repositories will be displayed

$ aws ecr describe-images --repository-name <name-of-repository-from-the-above-output> --output text

$ aws ecr list-images --repository-name name-of-repository

$ docker pull <aws-account>.dkr.ecr.eu-west-1.amazonaws.com/<name-of-repository->:<tag>

   // The image name format should be registry/repository[:tag]
 
$ docker images


## To achive the same results using a normal EC2 (amzn2-ami-hvm-2.0.20190313-x86_64-gp2 (ami-07683a44e80cd32c5) ) :

Add the following Roles to the EC2

AmazonECSTaskExecutionRolePolicy      AWS managed policy
AirflowAllowCloudwatchLogs            Inline policy
AirflowAllowECRECS                    Inline policy
AirflowAllowS3BucketAccess            Inline policy
AirflowAllowSecrets                   Inline policy
AirflowAllowSSMGetParameter           Inline policy

