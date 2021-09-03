# CloudFormation Configuration

This directory contains CF templates used to configure the DASDD environment, both for production and development. There
are currently two stacks in use:

1. **Core stack**: this stack is used for prod and includes resources such as:
    1. RDS Postgres database
    2. S3 bucket (for storing ad images)
    3. Necessary security groups
    4. CodeDeploy-configured EC2 instance via a nested stack (for running bots and push service)

2. **Dev stack**: this includes all resources in the core stack.

## Deploying the Core stack

Example:

`aws cloudformation create-stack --stack-name DASDD-core-stack --template-body file:///home/akshay/Desktop/Uni/FIT4002/FIT4002-DASDD-AWS/cloudformation/core-stack.yaml --profile educate --region us-east-1 --parameters ParameterKey=DBUsername,ParameterValue=postgres ParameterKey=DBPassword,ParameterValue=postgres --capabilities=CAPABILITY_IAM
`

To update the stack, replace `create-stack` with `update-stack`.

## Deploying the Dev stack

Example:
`aws cloudformation create-stack --stack-name DASDD-dev-stack --template-body file:///home/akshay/Desktop/Uni/FIT4002/FIT4002-DASDD-AWS/cloudformation/dev-stack.yaml --profile educate --region us-east-1 --parameters ParameterKey=DBUsername,ParameterValue=postgres ParameterKey=DBPassword,ParameterValue=postgres --capabilities=CAPABILITY_IAM
`

## References

- https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-rds-database-instance.html#aws-properties-rds-database-instance--examples
- https://docs.aws.amazon.com/cli/latest/reference/cloudformation/create-stack.html
- https://github.com/awslabs/aws-cloudformation-templates/blob/master/aws/services/RDS/RDS_MySQL_With_Read_Replica.yaml