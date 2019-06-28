# packer-drachtio-server

A [packer](https://www.packer.io/) template to build an AMI for drachtio server

## Installing 

```
$ git clone git@github.com:davehorton/packer-drachtio-server.git
$ cd packer-drachtio-server
$ git submodule update --init --recursive
$  packer build  \
-var 'aws_access_key=YOUR-ACCESS-KEY'  \
-var 'aws_secret_key=YOUR-SECRET-KEY' \
template.json
```

### variables
These variables can be specified on the `packer build` command line.  Defaults are listed below, where provided.
```
"aws_access_key": ""
```
Your aws access key.
```
"aws_secret_key": ""
```
Your aws secret key.

```
"region": "us-east-1"
```
The region to create the AMI in

```
"source_ami": "ami-024a64a6685d05041"
```
Source AMI to use.

```
ssh_username": "ubuntu"
```
ssh username to use when connecting to instance for provisioning

```
"ami_description": "EC2 AMI drachtio server v0.8.2 Ubuntu 18.04"
```
AMI description.

```
"instance_type": "t2.medium"
```
EC2 Instance type to use when building the AMI.

```
"drachtio_version": "v0.8.2
```
drachtio tag or branch to build

```
"install_nodejs": "false",
```
whether to install Node.js

```
"nodejs_version": "v10.16.0",
```
Node.js version to install

```
"remove_source": "true"
```
whether to remove source build directories, or leave them on the instance

```
"cloud_provider": "aws"
```
Cloud provider the AMI will be built on.
