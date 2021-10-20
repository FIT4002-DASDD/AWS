# CloudFormation Configuration

This directory contains CF templates used to configure the DASDD environment, both for production and development. There
are currently two stacks in use:

1. **Core stack**: this stack is used for prod and includes resources such as:
    1. RDS Postgres database
        1. Associated [DB Security Group](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Overview.RDSSecurityGroups.html)
    2. S3 bucket (for storing ad images)
    3. CodeDeploy agent-configured Ubuntu Server EC2 instance (for running bots and push service)
       1. Associated Instance Profile, to give the instance access to the application bundle on S3
       2. Role attached to the Instance Profile
       3. Associated [Security Group](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-security-groups.html)
          that opens up the SSH port
    4. A CodeDeploy Application, and a [DeploymentGroup](https://docs.aws.amazon.com/codedeploy/latest/userguide/deployment-groups.html#deployment-group-server)
       1. Associated [Service Role](https://docs.aws.amazon.com/codedeploy/latest/userguide/getting-started-create-service-role.html) to give the CodeDeploy service access to EC2

2. **Dev stack**: this includes some resources in the core stack.

## Deploying the Core stack

**Ensure that you pass in a valid EC2 Key Pair name when creating the stack so that SSH access is possible.**

Example:

`aws cloudformation create-stack --stack-name DASDD-core-stack --template-body file:///home/akshay/Desktop/Uni/FIT4002/FIT4002-DASDD-AWS/cloudformation/core-stack.yaml --profile mark --region ap-southeast-2 --parameters ParameterKey=DBUsername,ParameterValue=postgres ParameterKey=DBPassword,ParameterValue=postgres ParameterKey=BotServerKPName,ParameterValue=bot_server_kp --capabilities=CAPABILITY_IAM
`

To update the stack, replace `create-stack` with `update-stack`.

## Deploying the Dev stack (OUTDATED)

Example:
`aws cloudformation create-stack --stack-name DASDD-dev-stack --template-body file:///home/akshay/Desktop/Uni/FIT4002/FIT4002-DASDD-AWS/cloudformation/dev-stack.yaml --profile educate --region us-east-1 --parameters ParameterKey=DBUsername,ParameterValue=postgres ParameterKey=DBPassword,ParameterValue=postgres --capabilities=CAPABILITY_IAM
`

## References

- https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-rds-database-instance.html#aws-properties-rds-database-instance--examples
- https://docs.aws.amazon.com/cli/latest/reference/cloudformation/create-stack.html
- https://github.com/awslabs/aws-cloudformation-templates/blob/master/aws/services/RDS/RDS_MySQL_With_Read_Replica.yaml
