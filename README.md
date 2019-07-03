# packer-drachtio-server

A [packer](https://www.packer.io/) template to build an AMI for drachtio server

## Installing 

First:
```
$ git clone git@github.com:davehorton/packer-drachtio-server.git
$ cd packer-drachtio-server
$ git submodule update --init --recursive
```

then..

to build a simple drachtio server AMI on Ubuntu 18.04:
```
$  packer build  -var 'aws_access_key=XXXXX' \
-var 'aws_secret_key=YYYYY' \
template.json
```

to build a drachtio server AMI that includes node.js:
```
$  packer build  -var 'aws_access_key=XXXXX' \
-var 'aws_secret_key=YYYYY' \
-var 'install_nodejs=true' \
template.json
```

to also include rtpengine:
```
$  packer build  -var 'aws_access_key=XXXXX' \
-var 'aws_secret_key=YYYYY' \
-var 'install_nodejs=true' \
-var 'install_rtpengine=true' \
template.json
```
to build an AMI with freeswitch only for use with [drachtio-fsmrf](https://www.npmjs.com/package/drachtio-fsmrf)
```
$  packer build  -var 'aws_access_key=XXXXX' \
-var 'aws_secret_key=YYYYY' \
-var 'install_drachtio=false' \
-var 'install_freeswitch=true' \
template.json
```

to build an all-one server (drachtio, node, rtpengine, freeswitch) on Debian stretch:
```
$ git clone git@github.com:davehorton/packer-drachtio-server.git
$ cd packer-drachtio-server
$ git submodule update --init --recursive
$  packer build  -var 'aws_access_key=XXXXX' \
-var 'aws_secret_key=YYYYY' \
-var 'install_nodejs=true' \
-var 'install_freeswitch=true' \
-var 'install_rtpengine=true' \
-var 'source_ami=ami-0cac821e8b3cd5318' \
-var 'ssh_username=admin'  \
-var 'ami_description=drachtio-rtpengine-freeswitch-nodejs on Debian 9' \
-var 'remove_source=false' \
-var 'mod_audio_fork_subprotocol=audio.asapp.com' \
-var 'freeswitch_sip_port=5080' \
-var 'freeswitch_dtls_sip_port=5081' \
-color=false \
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
"install_drachtio": "true"
```
whether to install drachtio

```
"install_nodejs": "false",
```
whether to install Node.js

```
"install_rtpengine": "false",
```
whether to install rtpengine

```
"install_freeswitch": "false",
```
whether to install freeswitch

```
"install_drachtio_fail2ban": "false",
```
whether to install fail2ban with drachtio filter

```
"drachtio_version": "v0.8.2
```
drachtio tag or branch to build

```
"nodejs_version": "v10.16.0",
```
Node.js version to install

```
"freeswitch_bind_cloud_ip": "true"
```
If freeswitch is enabled, and cloud_provider is not none then this variable dictates whether freeswitch should bind its sip and rtp ports to the cloud public address (versus the local ipv4 address).

```
"mod_audio_fork_subprotocol": "audio.drachtio.org"
```
websocket subprotocol name used by freeswitch module mod_audio_fork

```
"mod_audio_fork_service_threads": "3",
```
number of libwebsocket service threads used by freeswitch module mod_audio_fork

``
"mod_audio_fork_buffer_secs": "2",
```
max number of seconds of audio to buffer by freeswitch module mod_audio_fork

```
"remove_source": "true"
```
whether to remove source build directories, or leave them on the instance

```
"cloud_provider": "aws"
```
Cloud provider the AMI will be built on.
