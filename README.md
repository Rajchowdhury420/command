# [nealalan.github.io](https://nealalan.github.io)/[command](https://nealalan.github.io/command)

TOC: 
- [COMMANDS 101](https://github.com/nealalan/command/blob/master/README.md#commands-101) 
- [ACCOUNTS / SYS ADMINISTRATION](https://github.com/nealalan/command/blob/master/README.md#accounts--sys-administration),  
- [AUDIO / VIDEO](https://github.com/nealalan/command/blob/master/README.md#audio--video)
- [AWS](https://github.com/nealalan/command/blob/master/README.md#aws)
- [CONFIGURATIONS](https://github.com/nealalan/command/blob/master/README.md#configurations) (systems)
- [CTF / DEVSEC / PENTEST](https://github.com/nealalan/command/blob/master/README.md#ctf--devsec--pentest)
- [DEV TOOLS](https://github.com/nealalan/command/blob/master/README.md#dev-tools-code--scripting)
- [DOCKER](https://github.com/nealalan/command/blob/master/README.md#docker)
- [ENCRYPTION](https://github.com/nealalan/command/blob/master/README.md#encryption)
- [FILES](https://github.com/nealalan/command/blob/master/README.md#files) - zip, transfer
- [FONTS](https://github.com/nealalan/command/blob/master/README.md#fonts)
- [GIT](https://github.com/nealalan/command/blob/master/README.md#git)
- [IMAGES & GRAPHICS](https://github.com/nealalan/command/blob/master/README.md#images--graphics)
- [MONITORING](https://github.com/nealalan/command/blob/master/README.md#monitoring)
- [NETWORKING](https://github.com/nealalan/command/blob/master/README.md#networking)
- [PACKAGE MANAGERS](https://github.com/nealalan/command/blob/master/README.md#package-managers)
- [PM2](https://github.com/nealalan/command/blob/master/README.md#pm2---advanced-production-process-manager-for-nodejs-wikipedia-git)
- POSTGRES
- [SEARCHING](https://github.com/nealalan/command/blob/master/README.md#searching)
- [TOOLS & SOFTWARE](https://github.com/nealalan/command/blob/master/README.md#tools--software) (aka other)
- [WEB SERVER](https://github.com/nealalan/command/blob/master/README.md#web-servers)
- [WORDPRESS](https://github.com/nealalan/command/blob/master/README.md#wordpress)


## COMMANDS 101 
- [An A-Z Index of the Apple macOS command line (OS X)](https://ss64.com/osx/)

FIRST
Change the command line to something civil and meaningful.
Regarding editing... I started using [PICO editor](https://en.wikipedia.org/wiki/Pico_(text_editor)) in 1992 or 1993. It's now deprecated to [NANO editor](https://en.wikipedia.org/wiki/Pico_(text_editor)) - something REALLY FANCY is you can add -m to use the MOUSE!!!
```bash
# see what the prompt is set to, if nothing then we can add one... if something, you can search 
#  how to set all sorts of things including flashing text.
$ cat ~/.bashrc | grep PS1
# edit...
$ nano ~/.bashrc
# Add this line....
```
This line found in [this gist](https://gist.github.com/nealalan/1159f6ffd341ebc885aa8006749bd8fd). I can't put it in this document because Jekyll markdown freaks out!

# AWS-CLI
## <span style="color:red">STS</span>
#### Assume a Role
```
aws sts assume-role --role-arn <arn:aws:iam::account-id:role/role-name> --role-session-name <session-name>
```

#### Get Caller Identity (Shows the current IAM role or user)
```
aws sts get-caller-identity
```

#### Assume a Role with MFA
```
aws sts assume-role --role-arn <arn:aws:iam::account-id:role/role-name> --role-session-name <session-name> --serial-number <arn-of-mfa-device> --token-code <mfa-token>
```

#### Decode Authorization Message (Decode an encoded message returned by STS)
```
aws sts decode-authorization-message --encoded-message <encoded-message>
```

#### Get Session Token
```
aws sts get-session-token --duration-seconds <seconds> --serial-number <mfa-arn> --token-code <mfa-token>
```

#### Assume Role with Web Identity
```
aws sts assume-role-with-web-identity --role-arn <arn:aws:iam::account-id:role/role-name> --role-session-name <session-name> --web-identity-token <token>
```

#### Assume Role with SAML
```
aws sts assume-role-with-saml --role-arn <arn:aws:iam::account-id:role/role-name> --principal-arn <arn-of-saml-provider> --saml-assertion <base64-saml-assertion>
```

#### Get Federation Token
```
aws sts get-federation-token --name <federation-name> --policy <json-policy> --duration-seconds <seconds>
```

#### Get Access Key Last Used
```
aws iam get-access-key-last-used --access-key-id <access-key-id>
```

#### List Access Keys
```
aws iam list-access-keys --user-name <username>
```

#### Create Access Key for a User
```
aws iam create-access-key --user-name <username>
```

#### Delete Access Key for a User
```
aws iam delete-access-key --user-name <username> --access-key-id <access-key-id>
```

#### Update Access Key Status (Enable/Disable)
```
aws iam update-access-key --user-name <username> --access-key-id <access-key-id> --status <Active|Inactive>
```

#### Create Service-Linked Role
```
aws iam create-service-linked-role --aws-service-name <service-name>
```

#### Simulate Principal Policy (Check Permissions)
```
aws iam simulate-principal-policy --policy-source-arn <arn-of-user-or-role> --action-names <action> --resource-arns <resource-arn>
```

# <span style="color:red">IdP</span>
#### Create a New SAML Identity Provider
```
aws iam create-saml-provider --saml-metadata-document <file://saml-metadata.xml> --name <provider-name>
```

#### List SAML Identity Providers
```
aws iam list-saml-providers
```

#### Get SAML Identity Provider Information
```
aws iam get-saml-provider --saml-provider-arn <saml-provider-arn>
```

#### Update SAML Identity Provider
```
aws iam update-saml-provider --saml-metadata-document <file://saml-metadata.xml> --saml-provider-arn <saml-provider-arn>
```

#### Delete SAML Identity Provider
```
aws iam delete-saml-provider --saml-provider-arn <saml-provider-arn>
```

#### Create an OIDC Identity Provider
```
aws iam create-open-id-connect-provider --url <oidc-provider-url> --client-id-list <client-id-1> <client-id-2> --thumbprint-list <thumbprint>
```

#### List OIDC Identity Providers
```
aws iam list-open-id-connect-providers
```

#### Get OIDC Identity Provider Information
```
aws iam get-open-id-connect-provider --open-id-connect-provider-arn <oidc-provider-arn>
```

#### Delete OIDC Identity Provider
```
aws iam delete-open-id-connect-provider --open-id-connect-provider-arn <oidc-provider-arn>
```


# <span style="color:red">IAM</span>
#### Create a New IAM User
```
aws iam create-user --user-name <username>
```
#### Delete an IAM User
```
aws iam delete-user --user-name <username>
```
#### List All IAM Users
```
aws iam list-users
```
#### Add a User to a Group
```
aws iam add-user-to-group --user-name <username> --group-name <groupname>
```
#### Remove a User from a Group
```
aws iam remove-user-from-group --user-name <username> --group-name <groupname>
```
#### Create a New IAM Group
```
aws iam create-group --group-name <groupname>
```
#### Delete an IAM Group
```
aws iam delete-group --group-name <groupname>
```
#### List IAM Groups
```
aws iam list-groups
```
#### Attach a Policy to a User
```
aws iam attach-user-policy --user-name <username> --policy-arn <arn:aws:iam::policyname>
```
#### Detach a Policy from a User
```
aws iam detach-user-policy --user-name <username> --policy-arn <arn:aws:iam::policyname>
```
#### Create an IAM Role
```
aws iam create-role --role-name <rolename> --assume-role-policy-document file://trust-policy.json
```
#### Attach a Policy to a Role
```
aws iam attach-role-policy --role-name <rolename> --policy-arn <arn:aws:iam::policyname>
```
#### List Attached Policies for a Role
```
aws iam list-attached-role-policies --role-name <rolename>
```
#### Delete an IAM Role
```
aws iam delete-role --role-name <rolename>
```
#### Create an Access Key for a User
```
aws iam create-access-key --user-name <username>
```
#### Delete an Access Key
```
aws iam delete-access-key --user-name <username> --access-key-id <access_key_id>
```
#### List All Access Keys for a User
```
aws iam list-access-keys --user-name <username>
```
#### Update an IAM User
```
aws iam update-user --user-name <current-username> --new-user-name <new-username>
```
#### List IAM Policies
```
aws iam list-policies
```
#### Get Account Summary
```
aws iam get-account-summary
```
#### Create a Policy
```
aws iam create-policy --policy-name <policyname> --policy-document file://policy.json
```
#### Delete a Policy
```
aws iam delete-policy --policy-arn <arn:aws:iam::policyname>
```
#### Add Tags to a Role (Using Role Name)
```
aws iam tag-role --role-name <role-name> --tags Key=<key>,Value=<value>
```
#### Add Tags to a Role (Using Role ARN)
```
aws iam tag-role --role-name <role-arn> --tags Key=<key>,Value=<value>
```

#### Remove Tags from a Role (Using Role Name)
```
aws iam untag-role --role-name <role-name> --tag-keys <key1> <key2> ...
```

#### Remove Tags from a Role (Using Role ARN)
```
aws iam untag-role --role-name <role-arn> --tag-keys <key1> <key2> ...
```

#### Create a Policy Version
```
aws iam create-policy-version --policy-arn <arn:aws:iam::policyname> --policy-document file://new_policy.json --set-as-default
```

#### List All Versions of a Policy
```
aws iam list-policy-versions --policy-arn <arn:aws:iam::policyname>
```

#### Delete a Policy Version
```
aws iam delete-policy-version --policy-arn <arn:aws:iam::policyname> --version-id <version_id>
```

#### Create an Inline Policy for a User
```
aws iam put-user-policy --user-name <username> --policy-name <policyname> --policy-document file://policy.json
```

#### List Inline Policies for a User
```
aws iam list-user-policies --user-name <username>
```

#### Delete an Inline Policy from a User
```
aws iam delete-user-policy --user-name <username> --policy-name <policyname>
```

#### Create an Inline Policy for a Group
```
aws iam put-group-policy --group-name <groupname> --policy-name <policyname> --policy-document file://policy.json
```

#### List Inline Policies for a Group
```
aws iam list-group-policies --group-name <groupname>
```

#### Delete an Inline Policy from a Group
```
aws iam delete-group-policy --group-name <groupname> --policy-name <policyname>
```

#### Create an Inline Policy for a Role
```
aws iam put-role-policy --role-name <rolename> --policy-name <policyname> --policy-document file://policy.json
```

#### List Inline Policies for a Role
```
aws iam list-role-policies --role-name <rolename>
```

#### Delete an Inline Policy from a Role
```
aws iam delete-role-policy --role-name <rolename> --policy-name <policyname>
```

#### Enable MFA for a User
```
aws iam enable-mfa-device --user-name <username> --serial-number <mfa_device_arn> --authentication-code-1 <code1> --authentication-code-2 <code2>
```

#### Deactivate MFA for a User
```
aws iam deactivate-mfa-device --user-name <username> --serial-number <mfa_device_arn>
```

#### Get User Information
```
aws iam get-user --user-name <username>
```

#### Get Group Information
```
aws iam get-group --group-name <groupname>
```

#### Get Role Information
```
aws iam get-role --role-name <rolename>
```

#### Get Policy Information
```
aws iam get-policy --policy-arn <arn:aws:iam::policyname>
```

#### Get Policy Version Information
```
aws iam get-policy-version --policy-arn <arn:aws:iam::policyname> --version-id <version_id>
```

#### Create a Signing Certificate for a User
```
aws iam upload-signing-certificate --user-name <username> --certificate-body file://public_key.pem
```

#### List Signing Certificates for a User
```
aws iam list-signing-certificates --user-name <username>
```

#### Delete a Signing Certificate
```
aws iam delete-signing-certificate --user-name <username> --certificate-id <cert_id>
```

#### List Account Alias
```
aws iam list-account-aliases
```

#### Create an Account Alias
```
aws iam create-account-alias --account-alias <alias>
```

#### Delete an Account Alias
```
aws iam delete-account-alias --account-alias <alias>
```

# Access Analyzer
#### Create an Analyzer
```
aws accessanalyzer create-analyzer --analyzer-name <analyzer-name> --type ACCOUNT
```

#### List Analyzers
```
aws accessanalyzer list-analyzers
```

#### Delete an Analyzer
```
aws accessanalyzer delete-analyzer --analyzer-name <analyzer-name>
```

#### Get Analyzer Details
```
aws accessanalyzer get-analyzer --analyzer-name <analyzer-name>
```

#### List Findings
```
aws accessanalyzer list-findings --analyzer-name <analyzer-name>
```

#### Get Finding Details
```
aws accessanalyzer get-finding --id <finding-id>
```

#### Archive a Finding
```
aws accessanalyzer archive-finding --analyzer-name <analyzer-name> --id <finding-id>
```

#### Update a Finding
```
aws accessanalyzer update-findings --analyzer-name <analyzer-name> --status <status>
```

#### Validate a Policy
```
aws accessanalyzer validate-policy --policy-type <type> --policy-document <json-policy>
```

#### List Archive Rules
```
aws accessanalyzer list-archive-rules --analyzer-name <analyzer-name>
```

#### Create an Archive Rule
```
aws accessanalyzer create-archive-rule --analyzer-name <analyzer-name> --filter <filter-key>=<filter-value> --rule-name <rule-name>
```

#### Get Archive Rule
```
aws accessanalyzer get-archive-rule --analyzer-name <analyzer-name> --rule-name <rule-name>
```

#### Delete an Archive Rule
```
aws accessanalyzer delete-archive-rule --analyzer-name <analyzer-name> --rule-name <rule-name>
```

#### Update an Archive Rule
```
aws accessanalyzer update-archive-rule --analyzer-name <analyzer-name> --rule-name <rule-name> --filter <filter-key>=<filter-value>
```


# <span style="color:red">Cloudformation</span>
#### Create a Stack
```
aws cloudformation create-stack --stack-name <stack-name> --template-body <file://template-file.json> --parameters ParameterKey=<key>,ParameterValue=<value>
```

#### Delete a Stack
```
aws cloudformation delete-stack --stack-name <stack-name>
```

#### Update a Stack
```
aws cloudformation update-stack --stack-name <stack-name> --template-body <file://template-file.json> --parameters ParameterKey=<key>,ParameterValue=<value>
```

#### Describe a Stack
```
aws cloudformation describe-stacks --stack-name <stack-name>
```

#### List Stacks
```
aws cloudformation list-stacks
```

#### Describe Stack Events
```
aws cloudformation describe-stack-events --stack-name <stack-name>
```

#### Describe Stack Resources
```
aws cloudformation describe-stack-resources --stack-name <stack-name>
```

#### Describe a Specific Stack Resource
```
aws cloudformation describe-stack-resource --stack-name <stack-name> --logical-resource-id <resource-id>
```

#### Validate a Template
```
aws cloudformation validate-template --template-body <file://template-file.json>
```

#### Estimate Stack Cost
```
aws cloudformation estimate-template-cost --template-body <file://template-file.json>
```

#### List Stack Resources
```
aws cloudformation list-stack-resources --stack-name <stack-name>
```

#### Cancel Stack Update
```
aws cloudformation cancel-update-stack --stack-name <stack-name>
```

#### Get Stack Policy
```
aws cloudformation get-stack-policy --stack-name <stack-name>
```

#### Set Stack Policy
```
aws cloudformation set-stack-policy --stack-name <stack-name> --stack-policy-body <file://policy.json>
```

#### List Stack Sets
```
aws cloudformation list-stack-sets
```

#### Describe Stack Set
```
aws cloudformation describe-stack-set --stack-set-name <stack-set-name>
```

#### Create Stack Set
```
aws cloudformation create-stack-set --stack-set-name <stack-set-name> --template-body <file://template-file.json>
```

#### Delete Stack Set
```
aws cloudformation delete-stack-set --stack-set-name <stack-set-name>
```

#### Update Stack Set
```
aws cloudformation update-stack-set --stack-set-name <stack-set-name> --template-body <file://template-file.json>
```

#### List Change Sets
```
aws cloudformation list-change-sets --stack-name <stack-name>
```

#### Create a Change Set
```
aws cloudformation create-change-set --stack-name <stack-name> --change-set-name <change-set-name> --template-body <file://template-file.json>
```

#### Delete a Change Set
```
aws cloudformation delete-change-set --change-set-name <change-set-name> --stack-name <stack-name>
```

#### Describe a Change Set
```
aws cloudformation describe-change-set --change-set-name <change-set-name> --stack-name <stack-name>
```

#### Execute a Change Set
```
aws cloudformation execute-change-set --change-set-name <change-set-name> --stack-name <stack-name>
```

#### List Exports
```
aws cloudformation list-exports
```

#### List Imports
```
aws cloudformation list-imports --export-name <export-name>
```

#### Detect Stack Drift
```
aws cloudformation detect-stack-drift --stack-name <stack-name>
```

#### Describe Stack Drift Detection Status
```
aws cloudformation describe-stack-drift-detection-status --stack-drift-detection-id <drift-detection-id>
```

#### Describe Stack Resource Drift
```
aws cloudformation describe-stack-resource-drifts --stack-name <stack-name>
```

#### List Stack Instances
```
aws cloudformation list-stack-instances --stack-set-name <stack-set-name>
```

#### Describe Stack Instance
```
aws cloudformation describe-stack-instance --stack-set-name <stack-set-name> --stack-instance-account <account-id> --stack-instance-region <region>
```

# <span style="color:red">S3</span>
#### List Buckets
```
aws s3 ls
```

#### Create a Bucket
```
aws s3 mb s3://<bucket-name>
```

#### Delete a Bucket
```
aws s3 rb s3://<bucket-name>
```

#### List Objects in a Bucket
```
aws s3 ls s3://<bucket-name>
```

#### Upload a File to a Bucket
```
aws s3 cp <file-path> s3://<bucket-name>/<key>
```

#### Download a File from a Bucket
```
aws s3 cp s3://<bucket-name>/<key> <local-file-path>
```

#### Delete an Object from a Bucket
```
aws s3 rm s3://<bucket-name>/<key>
```

#### Sync Local Directory to a Bucket
```
aws s3 sync <local-directory-path> s3://<bucket-name>
```

#### Sync Bucket to Local Directory
```
aws s3 sync s3://<bucket-name> <local-directory-path>
```

#### Enable Versioning on a Bucket
```
aws s3api put-bucket-versioning --bucket <bucket-name> --versioning-configuration Status=Enabled
```

#### Suspend Versioning on a Bucket
```
aws s3api put-bucket-versioning --bucket <bucket-name> --versioning-configuration Status=Suspended
```

#### List Object Versions in a Bucket
```
aws s3api list-object-versions --bucket <bucket-name>
```

#### Enable Server-Side Encryption on a Bucket
```
aws s3api put-bucket-encryption --bucket <bucket-name> --server-side-encryption-configuration '{"Rules":[{"ApplyServerSideEncryptionByDefault":{"SSEAlgorithm":"AES256"}}]}'
```

#### Get Bucket Encryption Status
```
aws s3api get-bucket-encryption --bucket <bucket-name>
```

#### Remove Bucket Encryption
```
aws s3api delete-bucket-encryption --bucket <bucket-name>
```

#### Set Bucket Policy
```
aws s3api put-bucket-policy --bucket <bucket-name> --policy <file://policy.json>
```

#### Get Bucket Policy
```
aws s3api get-bucket-policy --bucket <bucket-name>
```

#### Delete Bucket Policy
```
aws s3api delete-bucket-policy --bucket <bucket-name>
```

#### Set CORS Configuration on a Bucket
```
aws s3api put-bucket-cors --bucket <bucket-name> --cors-configuration <file://cors.json>
```

#### Get CORS Configuration of a Bucket
```
aws s3api get-bucket-cors --bucket <bucket-name>
```

#### Delete CORS Configuration of a Bucket
```
aws s3api delete-bucket-cors --bucket <bucket-name>
```

#### Enable Logging on a Bucket
```
aws s3api put-bucket-logging --bucket <bucket-name> --bucket-logging-status file://logging.json
```

#### Get Logging Status of a Bucket
```
aws s3api get-bucket-logging --bucket <bucket-name>
```

#### Enable Lifecycle Configuration on a Bucket
```
aws s3api put-bucket-lifecycle-configuration --bucket <bucket-name> --lifecycle-configuration <file://lifecycle.json>
```

#### Get Lifecycle Configuration of a Bucket
```
aws s3api get-bucket-lifecycle-configuration --bucket <bucket-name>
```

#### Delete Lifecycle Configuration of a Bucket
```
aws s3api delete-bucket-lifecycle --bucket <bucket-name>
```

#### Enable Public Access Block on a Bucket
```
aws s3api put-public-access-block --bucket <bucket-name> --public-access-block-configuration BlockPublicAcls=true,IgnorePublicAcls=true,BlockPublicPolicy=true,RestrictPublicBuckets=true
```

#### Get Public Access Block Status of a Bucket
```
aws s3api get-public-access-block --bucket <bucket-name>
```

#### Delete Public Access Block Configuration of a Bucket
```
aws s3api delete-public-access-block --bucket <bucket-name>
```

#### Copy an Object Between Buckets
```
aws s3 cp s3://<source-bucket>/<source-key> s3://<destination-bucket>/<destination-key>
```

# <span style="color:red">EC2</span>
#### Describe EC2 Instances
```
aws ec2 describe-instances
```

#### Start an EC2 Instance
```
aws ec2 start-instances --instance-ids <instance-id>
```

#### Stop an EC2 Instance
```
aws ec2 stop-instances --instance-ids <instance-id>
```

#### Reboot an EC2 Instance
```
aws ec2 reboot-instances --instance-ids <instance-id>
```

#### Terminate an EC2 Instance
```
aws ec2 terminate-instances --instance-ids <instance-id>
```

#### Describe EC2 Instance Status
```
aws ec2 describe-instance-status --instance-ids <instance-id>
```

#### Create a New EC2 Key Pair
```
aws ec2 create-key-pair --key-name <key-name>
```

#### Delete an EC2 Key Pair
```
aws ec2 delete-key-pair --key-name <key-name>
```

#### Create a Security Group
```
aws ec2 create-security-group --group-name <group-name> --description <description> --vpc-id <vpc-id>
```

#### Describe Security Groups
```
aws ec2 describe-security-groups
```

#### Authorize Inbound Traffic for a Security Group
```
aws ec2 authorize-security-group-ingress --group-id <security-group-id> --protocol <tcp|udp> --port <port> --cidr <cidr-block>
```

#### Revoke Inbound Traffic for a Security Group
```
aws ec2 revoke-security-group-ingress --group-id <security-group-id> --protocol <tcp|udp> --port <port> --cidr <cidr-block>
```

#### Create an EC2 Instance
```
aws ec2 run-instances --image-id <ami-id> --count <number-of-instances> --instance-type <instance-type> --key-name <key-name> --security-group-ids <security-group-id>
```

#### Describe EC2 AMIs
```
aws ec2 describe-images --owners <self|amazon|aws-marketplace>
```

#### Deregister an AMI
```
aws ec2 deregister-image --image-id <ami-id>
```

#### Create an EBS Volume
```
aws ec2 create-volume --availability-zone <az> --size <size-in-gb>
```

#### Describe EBS Volumes
```
aws ec2 describe-volumes
```

#### Attach an EBS Volume to an EC2 Instance
```
aws ec2 attach-volume --volume-id <volume-id> --instance-id <instance-id> --device <device-name>
```

#### Detach an EBS Volume from an EC2 Instance
```
aws ec2 detach-volume --volume-id <volume-id>
```

#### Delete an EBS Volume
```
aws ec2 delete-volume --volume-id <volume-id>
```

#### Create a Snapshot of an EBS Volume
```
aws ec2 create-snapshot --volume-id <volume-id> --description <description>
```

#### Describe EBS Snapshots
```
aws ec2 describe-snapshots --owner-ids <self|aws-account-id>
```

#### Delete an EBS Snapshot
```
aws ec2 delete-snapshot --snapshot-id <snapshot-id>
```

#### Create an AMI from an EC2 Instance
```
aws ec2 create-image --instance-id <instance-id> --name <ami-name>
```

#### Create a New Elastic IP Address
```
aws ec2 allocate-address
```

#### Associate an Elastic IP with an EC2 Instance
```
aws ec2 associate-address --instance-id <instance-id> --allocation-id <allocation-id>
```

#### Disassociate an Elastic IP from an EC2 Instance
```
aws ec2 disassociate-address --association-id <association-id>
```

#### Release an Elastic IP Address
```
aws ec2 release-address --allocation-id <allocation-id>
```

#### Create a VPC
```
aws ec2 create-vpc --cidr-block <cidr-block>
```

#### Describe VPCs
```
aws ec2 describe-vpcs
```

#### Delete a VPC
```
aws ec2 delete-vpc --vpc-id <vpc-id>
```

#### Create a Subnet in a VPC
```
aws ec2 create-subnet --vpc-id <vpc-id> --cidr-block <cidr-block>
```

#### Describe Subnets
```
aws ec2 describe-subnets
```

#### Delete a Subnet
```
aws ec2 delete-subnet --subnet-id <subnet-id>
```

#### Create an Internet Gateway
```
aws ec2 create-internet-gateway
```

#### Attach an Internet Gateway to a VPC
```
aws ec2 attach-internet-gateway --vpc-id <vpc-id> --internet-gateway-id <igw-id>
```

#### Describe Internet Gateways
```
aws ec2 describe-internet-gateways
```

#### Delete an Internet Gateway
```
aws ec2 delete-internet-gateway --internet-gateway-id <igw-id>
```

#### Create a Route Table for a VPC
```
aws ec2 create-route-table --vpc-id <vpc-id>
```

#### Describe Route Tables
```
aws ec2 describe-route-tables
```

#### Create a Route in a Route Table
```
aws ec2 create-route --route-table-id <route-table-id> --destination-cidr-block <cidr-block> --gateway-id <igw-id>
```

#### Associate a Route Table with a Subnet
```
aws ec2 associate-route-table --route-table-id <route-table-id> --subnet-id <subnet-id>
```

#### Disassociate a Route Table from a Subnet
```
aws ec2 disassociate-route-table --association-id <association-id>
```

#### Delete a Route Table
```
aws ec2 delete-route-table --route-table-id <route-table-id>
```

#### Delete a Route in a Route Table
```
aws ec2 delete-route --route-table-id <route-table-id> --destination-cidr-block <cidr-block>
```

# <span style="color:red">CloudTrail</span>

#### Create a New CloudTrail
```
aws cloudtrail create-trail --name <trail-name> --s3-bucket-name <s3-bucket-name>
```

#### Start Logging for a CloudTrail
```
aws cloudtrail start-logging --name <trail-name>
```

#### Stop Logging for a CloudTrail
```
aws cloudtrail stop-logging --name <trail-name>
```

#### Delete a CloudTrail
```
aws cloudtrail delete-trail --name <trail-name>
```

#### Describe a CloudTrail
```
aws cloudtrail describe-trails --trail-name-list <trail-name>
```

#### List all CloudTrails
```
aws cloudtrail list-trails
```

#### Get CloudTrail Status
```
aws cloudtrail get-trail-status --name <trail-name>
```

#### Lookup CloudTrail Events
```
aws cloudtrail lookup-events --lookup-attributes AttributeKey=<key>,AttributeValue=<value>
```

#### Update CloudTrail
```
aws cloudtrail update-trail --name <trail-name> --s3-bucket-name <new-s3-bucket-name>
```

#### Add Tags to CloudTrail
```
aws cloudtrail add-tags --resource-id <trail-arn> --tags-list Key=<key>,Value=<value>
```

#### Remove Tags from CloudTrail
```
aws cloudtrail remove-tags --resource-id <trail-arn> --tags-list Key=<key>
```

#### Create CloudTrail Insight
```
aws cloudtrail start-insight-selector --trail-name <trail-name> --insight-selectors '[{"InsightType": "ApiCallRateInsight"}]'
```

#### Stop CloudTrail Insight
```
aws cloudtrail stop-insight-selector --trail-name <trail-name> --insight-selectors '[{"InsightType": "ApiCallRateInsight"}]'
```

#### Get Insight Results
```
aws cloudtrail get-insight-results --insight-selector-arn <insight-arn>
```

# <span style="color:red">Lambda  </span>

#### Create a Lambda Function
```
aws lambda create-function --function-name <function-name> --runtime <runtime> --role <role-arn> --handler <handler> --zip-file fileb://<path-to-zip>
```

#### List Lambda Functions
```
aws lambda list-functions
```

#### Invoke a Lambda Function
```
aws lambda invoke --function-name <function-name> <output-file>
```

#### Update Lambda Function Code
```
aws lambda update-function-code --function-name <function-name> --zip-file fileb://<path-to-zip>
```

#### Update Lambda Function Configuration
```
aws lambda update-function-configuration --function-name <function-name> --handler <handler> --memory-size <size> --timeout <timeout>
```

#### Delete a Lambda Function
```
aws lambda delete-function --function-name <function-name>
```

#### Get Lambda Function Details
```
aws lambda get-function --function-name <function-name>
```

#### List Versions of a Lambda Function
```
aws lambda list-versions-by-function --function-name <function-name>
```

#### Publish a Lambda Version
```
aws lambda publish-version --function-name <function-name>
```

#### List Lambda Function Aliases
```
aws lambda list-aliases --function-name <function-name>
```

#### Create a Lambda Alias
```
aws lambda create-alias --function-name <function-name> --name <alias-name> --function-version <version>
```

#### Update a Lambda Alias
```
aws lambda update-alias --function-name <function-name> --name <alias-name> --function-version <version>
```

#### Delete a Lambda Alias
```
aws lambda delete-alias --function-name <function-name> --name <alias-name>
```

#### List Event Source Mappings
```
aws lambda list-event-source-mappings
```

#### Create Event Source Mapping
```
aws lambda create-event-source-mapping --function-name <function-name> --event-source-arn <arn> --batch-size <batch-size> --starting-position <position>
```

#### Update Event Source Mapping
```
aws lambda update-event-source-mapping --uuid <mapping-uuid> --function-name <function-name>
```

#### Delete Event Source Mapping
```
aws lambda delete-event-source-mapping --uuid <mapping-uuid>
```

#### Add Permission to Lambda Function
```
aws lambda add-permission --function-name <function-name> --statement-id <statement-id> --action <action> --principal <service>
```

#### Remove Permission from Lambda Function
```
aws lambda remove-permission --function-name <function-name> --statement-id <statement-id>
```

#### Get Lambda Function Policy
```
aws lambda get-policy --function-name <function-name>
```

#### List Layer Versions
```
aws lambda list-layer-versions --layer-name <layer-name>
```

#### Publish a Lambda Layer
```
aws lambda publish-layer-version --layer-name <layer-name> --zip-file fileb://<path-to-zip>
```

#### Delete a Lambda Layer Version
```
aws lambda delete-layer-version --layer-name <layer-name> --version-number <version-number>
```

#### Get Lambda Layer Details
```
aws lambda get-layer-version --layer-name <layer-name> --version-number <version-number>
```

#### Create Lambda Function URL Config
```
aws lambda create-function-url-config --function-name <function-name> --auth-type <auth-type>
```

#### Get Lambda Function URL Config
```
aws lambda get-function-url-config --function-name <function-name>
```

#### Update Lambda Function URL Config
```
aws lambda update-function-url-config --function-name <function-name> --auth-type <auth-type>
```

#### Delete Lambda Function URL Config
```
aws lambda delete-function-url-config --function-name <function-name>
```

Basic commands to navigate use the command line
ECHO - write arguments to the standard output
```bash
$ echo "cat" > cat.txt
$ echo $PATH
$ echo $(date)
```
CAT - concatenate and print files
```bash
#  -n number the output lines starting a            
#  -s squeeze out blank lines
#  -t -v display non-printable characters
$ cat cat.txt
$ cat cat.txt cat.txt > 2cats.txt
# On a linux distro besides Mac / Darwin, try
$ cat /etc/os-release
```
DATE = GENERATE A 16 CHAR RANDOM PASSWORD
```
$ date | md5 | tail -c16
# if pwgen installed
$ pwgen 16 -ncy
```
HEAD (display the first lines of a file) & TAIL (display the last part of a file)
```bash
# head [-n count | -c bytes] [file ...]
$ head -n1 file
# tail [-F | -f | -r] [-q] [-b number | -c number | -n number] [file ...]
# continue to print out an open file such as a log, while it is written to
$ tail -f /var/log/wifi.log
```
PS - process status
AWK [ -F fs ] [ -v var=value ] [ 'prog' | -f progfile ] [ file ...  ]
```bash
$ ps aux
$ ps -u root
```
DISK USAGE
```bash
$ df -ah
# DISK USAGE by folder
$ du -sh
```
LOCATE
```bash
```
EXPORT
```bash
$ export PATH=$PATH:$HOME/.local/bin
```
JQ - Command Line JSON PARSER
```
$ echo '{"foo": 0}' | jq .
```
LINK, LN, See also: [ln command](https://www.computerhope.com/unix/uln.htm)
```bash
# LN - link
#  -s is a symbolic link
$ sudo ln -s /home/ubuntu/sites-available sites-available
$ sudo ln -s /var/www/nealalan.com/html/ nealalan.com

# On my MacBookPro I wanted a folder called ~/Projects/ to point to my ~/Google Drive/DEV folder
$ ln -s '/Users/neal/Google Drive/DEV/' Projects
# And my ~/Pictures/ to point to ~/Google Drive/PHOTOS/
$ ln -s '/Users/neal/Google Drive/PHOTOS/' Pictures
# And my ~/Desktop/Screenshots/ to point to ~/Google Drive/PHOTOS/Screenshots/
$ ln -s '/Users/neal/Google Drive/PHOTOS/Screenshots/' Screenshots
```

SED / STREAM EDITOR - Stream editing data, useful with Regex to change contents of a file from the command line
```bash
# Install GNU `sed`, overwriting the built-in `sed` on MacOS
$ brew install gnu-sed --with-default-names
```

```bash
$ sed -f <text-commands>
# deleted 1 and 3
$ seq 10 | sed -e 1d -e 3d
$ seq 10 | sed -e '1d;3d'
# replace sour char with dest char in order
$ sed y/source-chars/dest-chars/
# replaces all numbers in format of 999-99-9999 or 9 numbers in a row
$ sed "y/123/abc/"
$ sed -ri ':1
         s/(^|[^-0-9])[0-9]{3}-[0-9]{2}-[0-9]{4}([^-0-9]|$)/\1XXX-XX-XXXX\2/g
         s/(^|[^-0-9])[0-9]{9}([^-0-9]|$)/\1XXXXXXXXX\2/g
         t1' <ssn.txt>
```

TEE - add / append input to a file
```bash
$ echo dog | tee -a text.txt
$ echo cat | tee -a text.txt
$ curl https://raw.githubusercontent.com/hashicorp/vagrant/master/keys/vagrant.pub | tee -a text.txt
```

![](https://github.com/nealalan/command/blob/master/images/Screen%20Shot%202019-01-18%20at%208.49.35%20PM.jpg?raw=true)


## ACCOUNTS / SYS ADMINISTRATION
OS Version
```bash
$ ubuntu@nealalan:~$ uname -a
Linux nealalan 4.4.0-1060-#69-Ubuntu SMP Sun May 20 13:42:07 UTC 2018 x86_64 x86_64 x86_64 GNU/Linux
```
OS Release Version (centos)
```
$ cat /etc/centos-release
```
Change to root
```bash
$ sudo -u root bash
```

### remote connections
```bash
$ ssh -i <pem> <user>@<ip>
$ scp -i <pem> <local> <dest>
```

### users & accounts
```bash
$ adduser
$ addgroup
$ chown

# FILE ACCESS CONTROL LIST
$ getfacl <file>
$ setfacl -m u:user2:rwx example/
$ setfacl -m g:group1:rwx ./

# ADDING A NEW USER
$ sudo adduser neal
$ sudo su neal (either way)
$ cd /home/neal
$ sudo mkdir .ssh
$ sudo ssh-keygen
$ sudo usermod -aG sudo neal   // add to group sudo
$ sudo cat nealkey.pub > authorized_keys
$ sudo nano /etc/ssh/sshd_config
#     UsePAM yes
#     allowAllowUsers neal

```
CHGRP - Group Ownership

```bash
# CHGRP - change group ownership
# Change the group of /u and subfiles to "admin".
$ chgrp -hR admin /u
# Change the current folder, all subfolders and files to the group "nealalan.com"
$ chgrp -hR nealalan.com .
              
```
## AUDIO / VIDEO
MP3 Audio and MP4 Video downloader
- I recommend not installing youtube-dl using pip... if you did use `pip uninstall youtube-dl` to remove it

```bash
# INSTALL:
$ brew install youtube-dl

# USE:
# to download video file
$ youtube-dl <https://link>

# to download videos with the best combination of audio and video, use:
$ youtube-dl -f best <https://link>
```

- With the war between youtube and youtube-dl... I found Homebrew didn't always install the latest. To install directly from youtube-dl (Note: this won't use a package manager!!!)

```bash
$ sudo curl -L https://yt-dl.org/downloads/latest/youtube-dl -o /usr/local/bin/youtube-dl
$ sudo chmod a+rx /usr/local/bin/youtube-dl
```
![](https://github.com/nealalan/command/blob/master/images/Screen%20Shot%202018-10-17%20at%2001.46.35.jpg?raw=true)

```bash
# to download audio file as mp3 and 320K bitrate
$ youtube-dl --extract-audio --audio-format mp3 --audio-quality 320K <https://link>
```
![](https://github.com/nealalan/command/blob/master/images/Screen%20Shot%202018-10-17%20at%2001.52.49.jpg?raw=true)

Audio / Video player install

```bash
# Install MPV https://mpv.io/installation/
$ brew install mpv
```
![](https://github.com/nealalan/command/blob/master/images/Screen%20Shot%202018-10-17%20at%2001.54.31.jpg?raw=true)

Audio Player
```bash
# from the command line you can use the arrow keys to control the playback of the audio
$ mpv <file.mp3>
```
![](https://github.com/nealalan/command/blob/master/images/Screen%20Shot%202018-10-17%20at%2001.55.27.jpg?raw=true)

Video Player
```bash
# interact with the video player that is spawned from the command line
$ mpv <file.mp4>
```
![](https://github.com/nealalan/command/blob/master/images/Screen%20Shot%202018-10-17%20at%2001.53.47.jpg?raw=true)
![](https://github.com/nealalan/command/blob/master/images/Screen%20Shot%202018-10-17%20at%2001.47.36.jpg?raw=true)

### Compress video - .mkv
I started with a 57 minute show that was 3814 meg and compressed to 280 meg in 12 minutes.
```bash
ffmpeg -n -i input.mkv -vcodec libx264 -crf 28 -preset faster -tune film output.mkv
```

## AWS
AWS & [LOCALSTACK](https://github.com/localstack/localstack)
```bash
# INSTALL:
$ brew install aws-cli
$ pip install localstack
# USE:
```

```
# Using prowler for security checks and debugging
# - this command will search for all SGs in an account and output bash debug
$ bash -x ./prowler -c extra75 -m 200 > debug.log 2>&1

```


## CONFIGURATIONS 
### MacOS / Darwin Specific
APPLE XCODE COMMAND LINE DEVELOPMENT
```bash
# INSTALL: 
$ xcode-select --install
```
Show all files in Mac OS Finder and on desktop (Note this will show annoying OS files)
```bash
$ defaults write com.apple.finder AppleShowAllFiles NO && killall Finder
$ defaults write com.apple.finder AppleShowAllFiles YES && killall Finder
```
Hide everythign on the Desktop and stop files from being drug to it
```bash
$ defaults write com.apple.finder CreateDesktop -bool false && killall Finder
```
Set where screenshots from PNG to JPG and location they are saved to
```bash
$ defaults write com.apple.screencapture location ~/Desktop/Screenshots
$ defaults write com.apple.screencapture type jpg && killall SystemUIServer
```
Always show the ~/Library folder 
```bash
$ chflags nohidden ~/Library/
```
Show the ~/.ssh folder as ~/ssh
```bash
$ ln -s ~/.ssh ~/ssh
```
Speed up TimeMachine Backups [link](https://www.defaults-write.com/speed-up-time-machine-backups/#more-1371)
```bash
# only persists until a reboot
$ sudo sysctl debug.lowpri_throttle_enabled=0
# slow back down without a reboot
$ sudo sysctl debug.lowpri_throttle_enabled=1
```
Expand the Save Panel by default
```bash
$ defaults write NSGlobalDomain NSNavPanelExpandedStateForSaveMode -bool true
$ defaults write NSGlobalDomain NSNavPanelExpandedStateForSaveMode2 -bool true
# use false to turn this off
```
Force text edit to default to plain text vs RTF format
```bash
$ defaults write com.apple.TextEdit RichText -int 0
# Undo using:
$ defaults delete com.apple.TextEdit RichText
```
Add a blank icon to the dock, move it around and add another...
```bash
$ defaults write com.apple.dock persistent-apps -array-add '{tile-data={}; tile-type="spacer-tile";}' && killall Dock
```
Set the max size to a time machine backup to 250GB (useful when multiple machines backup to the same drive)
```bash
$ sudo defaults write /Library/Preferences/com.apple.TimeMachine MaxSize -integer 256000
# To reset to no limit
$ sudo defaults write /Library/Preferences/com.apple.TimeMachine MaxSize
```
## Mojave Update Issues
I started seeing errors using homebrew after upgrading to macOS Mojave 10.14. It appears paths were removed.
```bash
$ brew upgrade
```
Resulted in:
```bash
xcrun: error: invalid active developer path (/Library/Developer/CommandLineTools), missing xcrun at: /Library/Developer/CommandLineTools/usr/bin/xcrun
```
To fix this [[article]](https://apple.stackexchange.com/questions/254380/macos-mojave-invalid-active-developer-path):
```bash
$ xcode-select --install
# RESULTS IN:
xcode-select: note: install requested for command line developer tools
```
### LAUNCHCTL
I used *launchctl* to clean up all the automatically launched items on a [clean install](https://nealalan.github.io/mac/setup/).   
```bash
Usage: launchctl <subcommand> ...
Subcommands:
	bootstrap       Bootstraps a domain or a service into a domain.
	bootout         Tears down a domain or removes a service from a domain.
	enable          Enables an existing service.
	disable         Disables an existing service.
	uncache         Removes the specified service name from the service cache.
	kickstart       Forces an existing service to start.
	attach          Attach the system's debugger to a service.
	debug           Configures the next invocation of a service for debugging.
	kill            Sends a signal to the service instance.
	blame           Prints the reason a service is running.
	print           Prints a description of a domain or service.
	print-cache     Prints information about the service cache.
	print-disabled  Prints which services are disabled.
	plist           Prints a property list embedded in a binary (targets the Info.plist by default).
	procinfo        Prints port information about a process.
	hostinfo        Prints port information about the host.
	resolveport     Resolves a port name from a process to an endpoint in launchd.
	limit           Reads or modifies launchd's resource limits.
	runstats        Prints performance statistics for a service.
	examine         Runs the specified analysis tool against launchd in a non-reentrant manner.
	config          Modifies persistent configuration parameters for launchd domains.
	dumpstate       Dumps launchd state to stdout.
	reboot          Initiates a system reboot of the specified type.
	bootshell       Brings the system up from single-user mode with a console shell.
	load            Bootstraps a service or directory of services.
	unload          Unloads a service or directory of services.
	remove          Unloads the specified service name.
	list            Lists information about services.
	start           Starts the specified service.
	stop            Stops the specified service if it is running.
	setenv          Sets the specified environment variables for all services within the domain.
	unsetenv        Unsets the specified environment variables for all services within the domain.
	getenv          Gets the value of an environment variable from within launchd.
	bsexec          Execute a program in another process' bootstrap context.
	asuser          Execute a program in the bootstrap context of a given user.
	submit          Submit a basic job from the command line.
	managerpid      Prints the PID of the launchd controlling the session.
	manageruid      Prints the UID of the current launchd session.
	managername     Prints the name of the current launchd session.
	error           Prints a description of an error.
	variant         Prints the launchd variant.
	version         Prints the launchd version.
	help            Prints the usage for a given subcommand.
```

## CTF / DEVSEC / PENTEST

```bash
# Install some CTF tools; see https://github.com/ctfs/write-ups.
brew install aircrack-ng
brew install bfg
brew install binutils
brew install binwalk
brew install cifer
brew install dex2jar
brew install dns2tcp
brew install fcrackzip
brew install foremost
brew install hashpump
brew install hydra
brew install john
brew install knock
brew install netpbm
brew install nmap
brew install pngcheck
brew install socat
brew install sqlmap
brew install tcpflow
brew install tcpreplay
brew install tcptrace
brew install ucspi-tcp # `tcpserver` etc.
brew install xpdf
brew install xz
```

### [Burp Suite](https://portswigger.net/burp#essential-manual-tools)
Not a command line tool, but here's info:
- Burp Proxy allows manual testers to intercept all requests and responses between the browser and the target application, even when HTTPS is being used.
- You can view, edit or drop individual messages to manipulate the server-side or client-side components of the application.
- The target site map shows all of the content that has been discovered in sites being tested.

### CURL - use to find internet IP address
```bash
$ curl http://169.254.169.254/
```
Also you can curl ifconfig.co and it will return your IPv4 or IPv6 IP address
```bash
$ curl -4 ifconfig.co
$ curl -6 ifconfig.co
```
Or for cool output, install "TOIlet"
```bash
# INSTALL LINUX:
$ sudo apt install -y toilet
# INSTALL MAC:
$ brew install toilet
# use
$ curl -s4 ifconfig.co | toilet -w 140 -f mono12
```
![](https://github.com/nealalan/command/blob/master/images/Screen%20Shot%202018-12-15%20at%205.56.32%20PM.jpg?raw=true)

### NETSTAT - show network status, network connections, routing tables, interface statistics, masquerade connections, and multicast memberships
```bash
#  -r show the routing tables
#  -s Show per-protocol statistics
#  -tu tcp & udp
$ netstat
$ netstat -a | more
# List active internet connections
$ netstat -plnt
```
### SS
```bash
# SS
$ ss -l
$ ss -ntp
$ ss -tupl
```
### NSLOOKUP - QUERY INTERNET NAME SERVERS INTERACTIVELY
```bash
# returns the domain name server the IP to domain resolution came from
# -type=SOA : find out the server of authority = might not work
$ nslookup neonaluminum.com
```

### DIG - DOMAIN INFORMATION GATHERING
```bash
# primarily used for DNS queries of A, TXT, MX, SOA, NS record sets
$ dig neonaluminum.com
# trace trace the domain server of authority (SOA)
$ dig +trace neonaluminum.com
# pull the DNS records (use A, TXT, MX, SOA, NS, ANY)
$ dig neonaluminum.com ANY +noall +answer
# from google, expanded lines
$ dig @8.8.8.8 +nocmd neonaluminum.com any +multiline +noall +answer
```

### WHOIS - QUERY IANA.ORG FOR DOMAIN INFO
```bash
$ whois neonaluminum.com
```

### [SHODAN](https://www.shodan.io/)
The search engine ([API](https://developer.shodan.io/api)) for security.


```bash
# INSTALL (Mac):
$ easy_install shodan
$ shodan init YOUR_API_KEY

# Reverse lookup for an IP address 
#   In browser: https://api.shodan.io/dns/reverse?ips=8.8.8.8&key={YOUR_API_KEY}
$ shodan host 8.8.8.8

# Search shodan
$ shodan search --fields ip_str,port,org,hostnames microsoft iis 6.0
```

### DIRB
```bash
$ dirb 10.10.50.2
```
### METASPLOIT
```bash
# metaspolit console
$ msfconsole
$4search shellshock
$ show options
# LOAD PARMS
$ set RHOST 10.10.50.2
$ set TARGETURI /cgi-bin/test-cgi
```
### SOCIAL ENGINEERING
```bash
# Discovery
# Harvester

```

## DEV TOOLS, CODE & SCRIPTING
- [Bash Scripting Cheatsheet](https://devhints.io/bash)
- [Wikibooks: Bash Shell Scripting](https://en.wikibooks.org/wiki/Bash_Shell_Scripting)


### SCRIPTING
```bash
# Don't forget:
$ chmod +x script.sh
```

### maven
apache maven will build your jar files from java source packages. 
```bach
# from your project-dir/pom.xml folder
$ mvn package
# you should end up with BUILD SUCCESSFUL and a folder project-dir/target/
```

### NODE, NPM, N

n is a node version manager: https://github.com/tj/n

```bash
$ brew install node npm n
$ sudo n lts
```
Check them:
```bash
$ node -v
$ n
$ npm -v
```

### TESTEM
```bash
$ npm install testem -g
```

### LINTER
```bash
$ npm install -g eslint eslint-config-fullstack eslint-plugin-react babel-eslint
# ADD ESLint extension to VSCode
```

### PYTHON
PACKAGE MANAGER FOR PYTHON
```bash
# INSTALL:
$ sudo easy_install pip
```

### RUBY & JEKYLL
[Jekyll Doc Site](https://jekyllrb.com/)

### SQL
- sqlmap

## DOCKER
First, download and start Docker GUI (Mac). Once started you can use `$ docker` from the terminal.

Pull and Launch CentOS to CLI
```
$ docker pull centos
$ docker run -it centos
```
If you try and run centos without a TTY, it will launch and quit.



## ENCRYPTION

### CHECKSUMS / MD5
```bash
# MD5 - calculate a message-digest fingerprint (checksum) for a file
# syntax: md5 [-pqrtx] [-s string] [file ...]
```

### PGP
```bash
# Install GnuPG to enable PGP-signing commits.
$ brew install gnupg
# I ran into some conflicts and had to perform a 
$ brew reinstall gnupg
$ gpg --version
$ gpg -K
```
Generate a Public key from a Private key
```bash
# extract the public key and store
openssl rsa -in mykey.pem -pubout > mykey.pub
```

## FILES
```bash
# DIRECTORY/FILE COLLAPSE
# find all files in this directory and its sub-directories 
# and execute mv with target directory . for each file found 
# to move them to current directory.
# Note: I tried adding mv --backup=numbered but this doesn't work
#  so I added -n to keep from overwriting files with the same name
$ find . -mindepth 2 -type f -print -exec mv -n {} . \;
```
```bash
# ARCHIVE/ZIP 
# -r recursively through dirs
# -dc a nice output
# -9 max compression (no reason not to if storing on the cloud?!)
# can use REGEX with it also :D
$ zip -r -dc -9 archive_name *
```
I use this to sync photos from the source to my iMac
```bash
# SYNC FILES ACROSS COMPUTERS
# --dry-run is obviously removed for the real xfer
$ rsync --dry-run --recursive --compress --progress --delete --itemize-changes ~/Pictures/ neal@192.168.1.42:/Users/Neal/Pictures/All_Photos > ~/Desktop/pic_bkp_$(date +"%Y%m%d_%H%M%S").txt
```
I use this to sync music to backups and other computers
```bash
# SYNCH FILES ACROSS COMPUTER, DISPLAY DELETED FILES ONLY
$ rsync -azP --delete -n ./ /Volumes/USB20FD/Music | grep 'deleting'
```


## FONTS
```bash
# Install font tools.
brew tap bramstein/webfonttools
brew install sfnt2woff
brew install sfnt2woff-zopfli
brew install woff2
```

## GIT

Regular daily use
```bash
$ git status
$ git pull
$ git push
$ git clone git@github.com:nealalan/command.git
```

a trick i found on stackoverflow when .git/index.lock gives Permission Denied
```bash
$ sudo chown -R : .git  # change group
$ sudo chmod -R 775 .git  # change permission
```

### git setup
https://help.github.com/en/articles/connecting-to-github-with-ssh

#### 1) Install on Ubuntu 18.04:
```bash
$ sudo apt install git git-gui git-doc
$ git version
# setup git
$ sudo git config --global --edit
```
#### 2) Create Keypair
Tips:
- create the keypair using the @users.noreply.github.com found in [Github: Settings: Emails](https://github.com/settings/emails). 
- it's smart to be in the ~/.ssh folder and name the keypair github_keypair
```bash
$ ssh-keygen -t rsa -b 4096 -C "neal@users.noreply.github.com"
```
Check the ssh-agent is running and add the key identity
```bash
$ eval "$(ssh-agent -s)"
$ ssh-add -k ~/.ssh/id_rsa
```
#### 3) Add the Keypair to [GitHub SSH and GPG Keys](https://github.com/settings/keys)
Print out the PRIVATE key to copy and paste into GitHub. I name it something like "Ubuntu 2019-12-31" to I know what it is and if it's current.
```bash
cat ~/.ssh/id_rsa.pub
```
Verify the keypair is added to github:
```bash
$ ssh -T git@github.com
```
You should see a message "Hi x! You've successfully authenticated, but GitHub does not provide shell access.
#### 4) If you cloned a repo already, you need ot set it to the correct repo using SSH
```bash
$ git remote set-url origin git@github.com:nealalan/nealalan.com.git
```

#### 5) If you only created a new repo on github
*First time using a repo… or create a new repository on the command line:*
```bash
# create a file and add the remote repo
echo "# nealalan.com" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin git@github.com:nealalan/nealalan.com.git
git push -u origin master
```
#### 6) When you make changes to the repo
*…or push an existing repository from the command line*
```bash
git remote add origin git@github.com:nealalan/nealalan.com.git
git push -u origin master
```
NOTE: If you have problems with permission denied, it could have to do with the ownership of the local files. Set the ownership to:

```
$ sudo chown -R ubuntu:ubuntu /var/www/
```

### hub
hub is a github utility that lets you *create a repo remotely* 
- [https://hub.github.com/](https://hub.github.com/)
- to use it you'll need to also install [Go](https://medium.com/@patdhlk/how-to-install-go-1-9-1-on-ubuntu-16-04-ee64c073cd79) 
```bash
These GitHub commands are provided by hub:

   browse         Open a GitHub page in the default browser
   ci-status      Show the status of GitHub checks for a commit
   compare        Open a compare page on GitHub
   create         Create this repository on GitHub and add GitHub as origin
   delete         Delete a repository on GitHub
   fork           Make a fork of a remote repository on GitHub and add as remote
   issue          List or create GitHub issues
   pr             List or checkout GitHub pull requests
   pull-request   Open a pull request on GitHub
   release        List or create GitHub releases
   sync           Fetch git objects from upstream and update branches
```
## IMAGES & GRAPHICS
### ExifTool
Here's a list of all the [EXIF meta-data tags](https://www.sno.phy.queensu.ca/~phil/exiftool/TagNames/EXIF.html)
And an [exiftool cheatsheet by rjames86](https://gist.github.com/rjames86/33b9af12548adf091a26)
```bash
# ExifTool - Read, Write and Edit Meta Info 
# Info: https://www.sno.phy.queensu.ca/~phil/exiftool/
# [Installing](https://www.sno.phy.queensu.ca/~phil/exiftool/install.html) exiftool:
$ brew install exiftool
# To show all metadata stored on a file AND THE FILE INFO (some info comes from the OS)
$ exiftool photo.jpg
$ exiftool photo.jpg | grep -E 'File Name|Create Date'
```
Manually manipulate metadata fields
```bash
# Quick and dirty way for a while directory
$ exiftool "-AllDates=1986:11:05 12:00:00" -if '$filetype eq "JPEG"' .
# Field at a time
$ exiftool '-datetimeoriginal=2015:01:18 12:00:00' .
```
A useful command to [rename all your files](https://www.sno.phy.queensu.ca/~phil/exiftool/#filename) based on the date. See [advanced features](https://www.sno.phy.queensu.ca/~phil/exiftool/filename.html) also.
```bash
# this will rename Ex: IMG_0001.JPG to 20180704_113201.JPG
#  Note: filtering out PNG and MP4 files. 
$ exiftool "-testname<CreateDate" -d %Y%m%d_%H%M%S-%%f.%%e ./*.JPG
$ exiftool "-FileName<CreateDate" -d %Y%m%d_%H%M%S-%%f.%%e ./*.JPG
# this will rename Ex:
$ exiftool '-testname<%f-$imagesize.%e' ./*.JPG
$ exiftool '-FileName<%f-$imagesize.%e' ./*.JPG
```
Note: to rename a file using the date for an iOS PNG that doesn't stote the CreateDate, we can use the -FileCreateDate. It is possible to use an exiftool command to update the exif CreateDate using the FileCreateDate info, but I'm choosing not to do that since the scope for me is just to rename the files.
```bash
$ exiftool "-testname<FileCreateDate" -d %Y%m%d_%H%M%S-%%f.%%e ./*.PNG
$ exiftool "-FileName<FileCreateDate" -d %Y%m%d_%H%M%S-%%f.%%e ./*.PNG
$ exiftool '-testname<%f-$imagesize.%e' ./*.PNG
$ exiftool '-FileName<%f-$imagesize.%e' ./*.PNG
```
Moving files
```bash
# move from DIR into folders by image date
$ exiftool "-Directory<DateTimeOriginal" -d "%Y/%m/%d" ./
```
Incase you do want to update PNG metadata CreateDate you can do it like this

![](https://raw.githubusercontent.com/nealalan/command/master/images/Screen%20Shot%202018-07-09%20at%2013.48.47.png)

### Imagemagic 
My first need was to convert all PNG files to JPG. The iPhone creates PNGs out of screenshots and they take up too much room!!!

```bash
# INSTALL
$ brew install imagemagick
```

```bash
$ convert
```

```bash
$ mogrify
# To see output and compress
$ for i in *.PNG; do mogrify -resize 75% -format jpg "$i"; echo "$i converted to ${i%.*}.jpg"; done
# To see output and compress and remove the PNG files
$ for i in *.PNG; do mogrify -resize 75% -format jpg "$i" && rm "$i"; echo "$i converted to ${i%.*}.jpg"; done
```

Install the ghostscript package will allow for converting PDF's to JPG's
```bash
$ brew install ghostscript
```

## MONITORING

```bash
# SHOW STATUS OF WHAT'S CURRENTLY RUNNING
# service <servicename> status
$ service --status-all
```
SYSTEM IO MONITORING LOOP
```bash
# writes out the activity  on the system every 3 seconts
$ while true ; do iostat -w 3 ; done
```
TOP -- display and update sorted information about processes
```bash
$ top -o cpu -O +rsize -s 3
```
IFTOP -- Interface top in a refreshing screen with cum view
```bash
$ sudo iftop -i en0
```
SYSTEMCTL & JOURNALCTL
```bash
$ systemctl start
$ systemctl stop
$ systemctl status <servicename>
# journalctl - Log file for the system to help debug when a server doesn’t start
$ journalctl -xe
```
- note-to-self: need to check out mytop, mtop, innotop, mysqladmin

## MySQL / MariaDB
- [mysql](https://dev.mysql.com/doc/refman/8.0/en/mysql.html) - command line client
- [mysqlshow](https://dev.mysql.com/doc/refman/8.0/en/mysqlshow.html) — Display Database, Table, and Column Information
- [mysqladmin](https://dev.mysql.com/doc/refman/8.0/en/mysqladmin.html) - Client for Administering a MySQL Server 
- [mysqlcheck](https://dev.mysql.com/doc/refman/8.0/en/mysqlcheck.html) — A Table Maintenance Program (checks, repairs, optimizes, or analyzes tables.)
- 
```bash]
$ mysql -u root -p
> exit;
> select version();
> show databases;
> use mysql
> show tables;
```
#### [Backup and Recovery](https://dev.mysql.com/doc/refman/8.0/en/backup-and-recovery.html)
- [mysqldump](https://dev.mysql.com/doc/refman/8.0/en/mysqldump.html) - A Database Backup Program
  - dumps one or more MySQL databases for backup or transfer to another SQL server
  - generate output in CSV, other delimited text, or XML format
- [mysqlpump](https://dev.mysql.com/doc/refman/8.0/en/mysqlpump.html) — A Database Backup Program
  - performs logical backups, producing a set of SQL statements that can be executed to reproduce the original database object definitions and table data. 
  - dumps one or more MySQL databases for backup or transfer to another SQL server
- [mysqlimport](https://dev.mysql.com/doc/refman/8.0/en/mysqlimport.html) — A Data Import Program
  - command-line interface to the LOAD DATA INFILE SQL statement
  


#### So I forgot my password to access MySQL. To reset it:
```bash
# Stop the MySQL Server:
$ sudo /etc/init.d/mysql stop
# Start the mysqld configuration:
$ sudo mysqld --skip-grant-tables &
# Login to MySQL as root:
$ mysql -u root mysql
# Replace YOURNEWPASSWORD with your new password:
> UPDATE
  mysql.user
SET
  Password = PASSWORD('YOURNEWPASSWORD')
WHERE
  User = 'root';
FLUSH PRIVILEGES;
exit;
```


## NETWORKING
NETWORK MONITORING
```bash
# INSTALL:
$ brew install iftop
```
SPEEDTEST
```bash
# DARWIN:
$ brew install speedtest-cli
# UBUNTU:
$ apt install speedtest-cli
```
![](https://github.com/nealalan/command/blob/master/images/Screen%20Shot%202018-08-30%20at%209.05.35%20PM.jpg?raw=true)

IFCONFIG - network interface configuration & routing for the computer ports
```bash
$ ifconfig en0
$ ifconfig | grep 'inet'
```

- [iptables essentials](https://nocsma.wordpress.com/2016/10/21/iptables-essentials-common-firewall-rules-and-commands/)

### nc / netcat 
TCP & UDP connections and listener
```bash
# NC - PULL A WEBPAGE
$ nc localhost 80
# NC - PORT SCANNING
$ nc -v -w 1 server2.example.com -z 1-1000
# NC - LISTEN FOR A CONNECTION ON PORT 42
#  -v add verbosity
$ nc -v -l 42
# CONNECT TO PORT 42 VIA THE LOOPBACK IP FROM ANOTHER TERM
$ nc -v 127.0.0.1 42
# either side can type and it will echo back
# terminate the connection with ^D (EOF)
```
```bash
# NC - SEND FILES
$ nc -lp 1234 > stuff_to_send.txt
$ nc -w 1 server 1234 < stuff.txt

# LISTEN INTO A FILE
$ nc -v -l 43 > filename.receive
# SEND A FILE TO PORT 43 VIA THE LOOPBACK IP FROM ANOTHER TERM
$ nc -v 127.0.0.1 43 < filename.send
```

### nethogs
```bash
# NETHOGS -- monitor process socket connections 
```

### nmap
nmap can be super noisy and really irritate anyone you run it against recommend you only run it again computers within your internal network or scanme.nmap.org
```bash
# FIND OUT WHAT'S THERE BRUTELY, RECURSIVELY
# this will give you a nice idea of how to hit a server that's poorly configured and open
# -A : enable OS detection and version detection, script scanning and tracert
# -T4 : faster execution (about 1 min for me usually)
# -r : scan ports consecutively
# -p : port range
$ nmap -A -T4 -r -p [1-9999] <address>
#
$ nmap -sC

$ nmap localhost
$ scutil --proxy
$ scutil --dns
$ scutil --get ComputerName
``` 
## PACKAGE MANAGERS
### BREW (HOMEBREW) PACKAGE MANAGER
```bash
# INSTALL:
$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
# CHECK STATUS:
$ brew doctor
```
OTHER BREW COMMANDS
```bash
# SEE WHAT'S INSTALLED:
$ brew list && brew cask list
$ system_profiler -detailLevel full SPApplicationsDataType >> installed_software_$(date "+%Y%m%d_%H%M%S").txt
$ brew ls --full-name --versions >>  installed_software_$(date +"%Y%m%d_%H%M%S").txt

# CREATE 'Brewfile' LIST OF INSTALLS & INSTALL LIST IN 'Brewfile'
$ brew bundle dump
$ brew Brewfile

# SEARCHING FOR INSTALLABLE PACKAGES
$ brew search

# REMOVE OUTDATES VERSIONS (from the cellar):
brew cleanup

# CHECK FOR UPDATES:
$ brew update
$ brew upgrade
```

### APT PACKAGE MANAGER - native in Ubuntu
```bash
# APT / APT-GET -provides a high-level command line interface for the package management system
#  -y default yes
#  update = d/l package info from all configured sources
#  upgrade = install avai upgrades of all packages 
# USE:
$ apt update
$ apt upgrade
$ apt install <package>
$ apt list --installed
# apt-cache - queries apt data 
#  currently installed on the system from the sources configured via sources.list
$ apt-cache search <package>
$ apt-cache 

# NOTE: You can install this on a Mac, but I choose not to at this point.

# CREATE A LIST OF INSTALLED PACKAGES 
$ sudo apt list --installed >> installed_software_$(date +"%Y%m%d_%H%M%S").txt
```

## [PM2 - Advanced, production process manager for Node.js](http://pm2.keymetrics.io/) ([wikipedia](https://en.wikipedia.org/wiki/PM2_(software))) ([git](https://github.com/unitech/pm2))
PM2 is a production process manager for Node.js applications with a built-in load balancer. It allows you to keep applications alive forever, to reload them without downtime and to facilitate common system admin tasks.

#### Start, Stop, Restart an Application
```bash
$ pm2 start app_name_or_id
$ pm2 stop app_name_or_id
$ pm2 restart app_name_or_id
```
- PM2 will automatically assign an app name of the prefix

#### Status of PM2 Processes
```bash
$ pm2 list
$ pm2 info app_name_or_id
```

For a realtime monitor of processes:
```bash
$ app_name_or_id
```

#### Add PM2 as a Process
```bash
$ pm2 startup systemd
$ sudo env PATH=$PATH:/usr/bin /usr/lib/node_modules/pm2/bin/pm2 startup systemd -u ubuntu --hp /home/ubuntu
$ systemctl status pm2-ubuntu
```

## POSTGRES
- lab: [how-to-install-and-use-postgresql-on-ubuntu-18-04](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-postgresql-on-ubuntu-18-04)

#### Switching Over to the postgres Account
Switch over to the postgres account and access a Postgres prompt immediately by typing:

```bash
$ sudo -i -u postgres
$ psql
```
Exit out of the PostgreSQL prompt by typing: `\q`


## SEARCHING
particularly useful when searching for a file or searching for content in a file, such as something suspecious in a log file
```bash
# SEARCH A FILE FOR SPECIFIC CONTENT
# -H : print the filename of each match
# --max-count=#
# -c : suppress output and count matching lines
# -v : inverse matching
# -E : regex pattern search (or text search)
$ cat access.log | grep -E 'php|POST|HEAD|DNS'
```
![](https://raw.githubusercontent.com/nealalan/command/master/images/grep-E.png)

```bash
# LSOF -- list open files
# huge man file and particularly useful, note security issues with it
$ lsof > ~/open_files.txt
```

## TOOLS & SOFTWARE
WEBTORRENT
```bash
# DARWIN:
$ brew install webtorrent-cli
# UBUNTU:
$ apt install webtorrent-cli
```
![](https://github.com/nealalan/command/blob/master/images/Screen%20Shot%202018-09-29%20at%2013.35.28.jpg?raw=true)
```bash
# USE: 
$ webtorrent download https://images.offensive-security.com/kali-linux-2018.3a-amd64.iso.torrent -o ~/Downloads/
```
![](https://github.com/nealalan/command/blob/master/images/Screen%20Shot%202018-09-29%20at%2013.45.24.jpg?raw=true)

COREUTILS, MOREUTILS, FILEUTILS
```bash
# [GNU CoreUtils](https://www.gnu.org/software/coreutils/coreutils.html) - Basic file, shell and text manipulation utilities of the GNU operating system. These are the core utilities which are expected to exist on every operating system.
$ brew install coreutils
$ info coreutils

# [moreUtils](https://joeyh.name/code/moreutils/) - some other useful utilities like `sponge`
$ brew install moreutils
$ info sponge

# GNU fileUtils - some utils like `find`, `locate`, `updatedb`, and `xargs`, `g`-prefixed.
$ brew install findutils
$ info find

# Install Bash 4.
# Note: don’t forget to add `/usr/local/bin/bash` to `/etc/shells` before running `chsh`.
$ brew install bash
$ sudo nano /etc/shells
   # add `/usr/local/bin/bash` to `/etc/shells`

# Install bash-completion
$ brew install bash-completion2
$ sudo nano ~/.bash_profile
   # add the following to your ~/.bash_profile:
  if [ -f /usr/local/share/bash-completion/bash_completion ]; then
    . /usr/local/share/bash-completion/bash_completion
  fi
$ bash --version

# Updated from BSD grep 2.5.1 to GNU grep 3.1
$ brew install grep --with-default-names
```
EDITORS
```bash
# VI - I hate 'VIM' and will always just install NANO (command line) or ATOM (GUI)
$ brew install vim --with-override-system-vi
$ brew install nano
```
SCREEN - MULTITASKING TOOL

A tool that allows you to have multiple screens within a single session using "[regions](https://www.gnu.org/software/screen/manual/screen.html#Regions)"
```bash
# INSTALL:
$ brew install screen
# Note: when I upgraded I went from v4.00.03 23-Oct-06 to v4.06.02 23-Oct-17
# USE:
#   you can see what's open using the `w` command
#   see key-bindings ^a-?
#   see all screens: ^a-*
#   new screen: ^a-c
#   jump between: ^a-" and scroll to select
#   spilt screen: ^a-S 
```
DOWNLOADING UTIL
```bash
# INSTALL:
$ brew install wget --with-iri
# USE:
$ wget -P ~/Downloads/ https://download.virtualbox.org/virtualbox/5.2.18/VirtualBox-5.2.18-124319-OSX.dmg
```
![](https://github.com/nealalan/command/blob/master/images/Screen%20Shot%202018-09-29%20at%2014.48.24.jpg?raw=true)




Text Based Web Browser - This is what I started using in 1994 on Freenets when I started writing HTML
```bash
# INSTALL:
$ brew install lynx
# USE:
$ lynx nealalan.github.io
```
![](https://github.com/nealalan/command/blob/master/images/Screen%20Shot%202018-10-19%20at%2012.26.04.jpg?raw=true)

..... Other things I haven't documented yet
```bash
brew install openssh
brew install homebrew/php/php56 --with-gmp

# Install other useful binaries.
brew install ack
#brew install exiv2
brew install git-lfs
brew install imagemagick --with-webp
brew install lua

brew install p7zip
brew install pigz
brew install pv
brew install rename
brew install rlwrap
brew install ssh-copy-id
brew install tree
brew install vbindiff
brew install zopfli
```

## Web Servers

### CertBot
See what certs we have and expiry:
```bash
$ sudo certbot certificates
```

To update email with certbot:
```bash
$ sudo certbot update_account --update-registration --email thenew@email.address
```

Updating with wildcards proved to be a challenge. I ended up having many certificates and NGINX confused the certs in the config file because domain.com and \*.domain.com had different cert. I cleaned them and ended up needing to add a new TXT DNS record called "\_acme-challenge.neonaluminum.com" to verify I owned the domain.

```bash
$ sudo certbot --server https://acme-v02.api.letsencrypt.org/directory -d neonaluminum.com,*.neonaluminum.com,*.fire.neonaluminum.com --manual --preferred-challenges dns-01 certonly
```

### NGINX
![](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQQj3EFXE48c5ZLwr23GFqzHvJ827UnmVpXhvj5P2YjpYyrTY8CzA&s)

View status
```bash
$ sudo service status nginx
$ sudo systemctl status nginx
$ sudo systemctl status nginx.service
$ sudo journalctl -xe
# error messages... testing (or testing with a specific config file
$ nginx -t
$ nginx -c /etc/nginx/nginx.conf -t
```

Viewing the logs
```bash
$ sudo tail -f /var/log/nginx/error.log 
```

Reload nginx server after you made changes to the config file such as nginx.conf:
```bash
$ sudo nginx -s reload
$ sudo systemctl reload nginx
$ sudo service nginx reload
```

Stopping and starting... some options
```bash
$ sudo systemctl start nginx 
$ sudo systemctl stop nginx 
$ sudo systemctl restart nginx
$ sudo service nginx start
$ sudo service nginx stop
$ sudo service nginx restart
$ sudo /etc/init.d/nginx start
$ sudo /etc/init.d/nginx stop
$ sudo /etc/init.d/nginx restart
```

#### More Useful CLI tools
- xmodulo.com/useful-cli-tools-linux-system-admins.html

## WORDPRESS
- wordpress-online-vulnerabilitty-scanners
<br><br>



[[edit](https://github.com/nealalan/command/edit/master/README.md)]
