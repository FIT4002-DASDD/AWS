# CloudFormation Configuration

This directory contains CF templates used to configure the DASDD environment, both for production and development. There
are currently two stacks in use:

1. **Core stack**: this includes resources such as:
    1. RDS Postgres database (prod)
    2. S3 bucket (for storing ad images)
    3. Necessary security groups

2. **Dev stack**: this includes

## Deploying the Core stack

Example:

`aws cloudformation create-stack --stack-name DASDD-core-stack --template-body file:///home/akshay/Desktop/Uni/FIT4002/FIT4002-DASDD-AWS/cloudformation/core-stack.yaml --profile educate --region us-east-1 --parameters ParameterKey=DBUsername,ParameterValue=postgres ParameterKey=DBPassword,ParameterValue=postgres
`

## Deploying the Dev stack

Example:
`aws cloudformation create-stack --stack-name DASDD-dev-stack --template-body file:///home/akshay/Desktop/Uni/FIT4002/FIT4002-DASDD-AWS/cloudformation/dev-stack.yaml --profile educate --region us-east-1 --parameters ParameterKey=DBUsername,ParameterValue=postgres ParameterKey=DBPassword,ParameterValue=postgres
`

## References

- https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-rds-database-instance.html#aws-properties-rds-database-instance--examples
- https://docs.aws.amazon.com/cli/latest/reference/cloudformation/create-stack.html
- https://github.com/awslabs/aws-cloudformation-templates/blob/master/aws/services/RDS/RDS_MySQL_With_Read_Replica.yaml