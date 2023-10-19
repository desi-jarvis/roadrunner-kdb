# AWS EC2

## Describe-instances
```
aws ec2 describe-instances --output json --query 'Reservations[*].Instances[*].[InstanceId,PublicIpAddress,State,SecurityGroups,Tags]'

aws ec2 describe-instances --profile default --region us-east-1 --query 'Reservations[*].Instances[*].[InstanceId,PublicIpAddress,Tags]' --filters "Name=instance-state-name,Values=running"

aws ec2 describe-instances --query 'Reservations[*].Instances[*].[InstanceId,PublicIpAddress,PrivateIpAddress,Tags]' --filters "Name=instance-state-name,Values=running"

aws ec2 describe-instances --profile default

```
## Run-instances
```
 aws ec2 run-instances --image-id <AMI-ID>  --count 1 --instance-type t2.micro --key-name my-ssh-pubkey --security-group-ids <Security-Group-Id> --subnet-id <Subnet-Group-Id>

 aws ec2 run-instances --image-id <AMI-ID>  --count 1 --instance-type t2.micro --key-name my-ssh-pubkey --security-group-ids <Security-Group-Id> --block-device-mappings "[{\"DeviceName\": \"/dev/sda1\",\"Ebs\": {\"Encrypted\": true, \"DeleteOnTermination\": true,\"KmsKeyId\":\"<KMS-Key-Id>\",\"VolumeSize\": 200,\"VolumeType\": \"gp2\"}}]"

 aws ec2 run-instances --image-id <AMI-ID> --count 1 --instance-type t2.micro --key-name my-ssh-pubkey --security-group-ids <Security-Group-Id> --block-device-mappings "[{\"DeviceName\": \"/dev/sda1\",\"Ebs\": {\"Encrypted\": true, \"DeleteOnTermination\": true,\"KmsKeyId\":\"<KMS-Key-Id>\",\"VolumeSize\": 200,\"VolumeType\": \"gp2\"}}]"

 aws ec2 run-instances --image-id <AMI-ID> --count 1 --instance-type t2.micro --key-name my-ssh-pubkey --security-group-ids <Security-Group-Id> --tag-specifications 'ResourceType=instance,Tags=[{Key=Name,Value=ServerName}]'

 aws ec2 run-instances --image-id <AMI-ID> --count 1 --instance-type t2.micro --key-name my-ssh-pubkey  --security-group-ids "<Security-Group-Id>" "<Security-Group-Id>"
```
## Create-image
```
 aws ec2 create-image --instance-id <instance-id> --name "<Template-Name>"
```
## Modify-instance-attribute
```
 aws ec2 modify-instance-attribute --instance-id <instance-id> --groups "<Security-Group-Id>"

 aws ec2 modify-instance-attribute --instance-id <instance-id> --groups "<Security-Group-Id>" "<Security-Group-Id>"
```
## Terminate-instances
```
 aws ec2 terminate-instances --instance-ids <instance-id>
```
## Delete-volume
```
 aws ec2 delete-volume --volume-id <volume-id>
```

## Import key pair
```
 aws ec2 import-key-pair --key-name my-ssh-pubkey --public-key-material fileb://<pub-key-path>
```
## Create security group
```
 aws ec2 create-security-group --group-name <security-group-name> --description "<SG Rules>" --region us-east-1
```
## Authorize security group ingress
```
 aws ec2 authorize-security-group-ingress --group-id <Security-Group-Id> --protocol tcp --cidr <CIDR> --port <port-num>

 aws ec2 authorize-security-group-ingress --group-id <Security-Group-Id> --protocol tcp --cidr <CIDR> --port <port-num>

 aws ec2 authorize-security-group-ingress --group-id <security-group-id> --protocol tcp --port <port-num> --source-group <source-security-group-id>

 aws ec2 authorize-security-group-ingress --group-id <Security-Group-Id> --ip-permissions IpProtocol=tcp,FromPort=<port-num>,ToPort=<port-num>,IpRanges="[{CidrIp=<CIDR>,Description='<DESC>'}]"

 aws ec2 authorize-security-group-ingress --group-id <Security-Group-Id> --ip-permissions IpProtocol=tcp,FromPort=<port-num>,ToPort=<port-num>,IpRanges="[{CidrIp=<CIDR>,Description='<DESC>'}]"

 aws ec2 authorize-security-group-ingress --group-id <Security-Group-Id> --ip-permissions IpProtocol=tcp,FromPort=<port-num>,ToPort=<port-num>,IpRanges="[{CidrIp=<CIDR>,Description='<DESC>'}]" IpProtocol=tcp,FromPort=<port-num>,ToPort=<port-num>,IpRanges="[{CidrIp=<CIDR>,Description='<DESC>'}]"
```
## Revoke security group ingress
```
 aws ec2 revoke-security-group-ingress --group-id <Security-Group-Id> --protocol tcp --cidr <CIDR> --port <port-num>

 aws ec2 revoke-security-group-ingress --group-id <Security-Group-Id> --protocol tcp --cidr <CIDR> --port <port-num>

 aws ec2 revoke-security-group-ingress --group-id <Security-Group-Id> --ip-permissions IpProtocol=tcp,FromPort=<port-num>,ToPort=<port-num>,IpRanges="[{CidrIp=<CIDR>,Description='<DESC>'}]"

 aws ec2 revoke-security-group-ingress --group-id <Security-Group-Id> --ip-permissions IpProtocol=tcp,FromPort=<port-num>,ToPort=<port-num>,IpRanges="[{CidrIp=<CIDR>,Description='<DESC>'}]" IpProtocol=tcp,FromPort=<port-num>,ToPort=<port-num>,IpRanges="[{CidrIp=<CIDR>,Description='<DESC>'}]"

 aws ec2 revoke-security-group-ingress --security-group-rule-ids sgr-XXXXXXXXXXX sgr-YYYYYYYYYYY --group-name <security-group-name>
```
## Describe subnets
```
 aws ec2 describe-subnets
```
## Describe security groups
```
 aws ec2 describe-security-groups

 aws ec2 describe-security-groups --query 'SecurityGroups[*].[GroupName,GroupId]'

 aws ec2 describe-security-groups --group-ids <security-group-id>

 aws ec2 describe-security-groups --group-names <security-group-name>
```
## Create tags
```
 aws ec2 create-tags --resources sg-XXXXXXXXXXX --tags Key=Name,Value=SecGroupName --profile default --region us-east-1
```
# AWS S3

## Create bucket
```
 aws s3api create-bucket --bucket my-unique-bucket-name --region us-east-1 --create-bucket-configuration LocationConstraint=us-east-1
```
## List buckets
```
 aws s3api list-buckets --region us-east-1
```
## List bucket objects
```
 aws s3 ls s3://<bucket-name>  --region us-east-1
```
## Copy bucket objects
```
 aws s3 cp /tmp/a.txt s3://<bucket-name>   --region us-east-1

 aws s3 cp <foldername> s3://<bucket/object-s3path> --recursive --profile
```
## Create folder in bucket
```
 aws s3api put-object --bucket <your-bucket-name> --key <folder-name>/test.txt --body yourfile.txt
```
## Delete bucket
```
 aws s3api delete-bucket --bucket my-unique-bucket-name --region us-east-1
```
