# aws-codedeploy-springboot
Example project showing how to deploy a Spring Boot app to AWS with Amazon CodeDeploy


## What do we want to do?

Assume we have a Spring Boot app that we want to deploy to AWS with the help of TravisCI and an fully automated Infrastructure-as-Code style. What options do we have?

### Amazon CodeDeploy

+ directly suitable for AWS
- vendor lockin

https://docs.aws.amazon.com/codedeploy/latest/userguide/welcome.html

#### Prerequisites

https://docs.aws.amazon.com/codedeploy/latest/userguide/getting-started-codedeploy.html

###### Create a IAM User (don´t use your AWS root account)

First create a new Policy `awscodedeploy` at https://console.aws.amazon.com/iam/home#/policies with the following JSON (for more info, see https://docs.aws.amazon.com/codedeploy/latest/userguide/getting-started-provision-user.html):

```
{
  "Version": "2012-10-17",
  "Statement" : [
    {
      "Effect" : "Allow",
      "Action" : [
        "autoscaling:*",
        "cloudformation:*",
        "codedeploy:*",
        "ec2:*",
        "lambda:*",
        "elasticloadbalancing:*",
        "iam:AddRoleToInstanceProfile",
        "iam:CreateInstanceProfile",
        "iam:CreateRole",
        "iam:DeleteInstanceProfile",
        "iam:DeleteRole",
        "iam:DeleteRolePolicy",
        "iam:GetInstanceProfile",
        "iam:GetRole",
        "iam:GetRolePolicy",
        "iam:ListInstanceProfilesForRole",
        "iam:ListRolePolicies",
        "iam:ListRoles",
        "iam:PassRole",
        "iam:PutRolePolicy",
        "iam:RemoveRoleFromInstanceProfile", 
        "s3:*"
      ],
      "Resource" : "*"
    }    
  ]
}
```

Go to https://console.aws.amazon.com/iam/ and add a new User - here `aws-codedeploy-springboot` with programatic access enabled. Go next and add the new User to the group `codedeploy` with the formerly created policy type `awscodedeploy`.

###### Install & configure AWS CLI 

* `brew install awscli`

* open new console and then type `aws configure`

* get the access key ID and secret access key for an IAM user from the formerly created IAM user at the console https://console.aws.amazon.com/iam/

* choose a appropriate the CodeDeploy supported regions (https://docs.aws.amazon.com/general/latest/gr/rande.html#codedeploy_region) - I wanted to go with Frankfurt/EU, so I chose `eu-central-1`

* select the default output format with typing `json`



* TravisCI CodeDeploy integration: https://docs.travis-ci.com/user/deployment/codedeploy/



### EC2 Container Service

https://aws.amazon.com/de/blogs/compute/deploying-java-microservices-on-amazon-ec2-container-service/