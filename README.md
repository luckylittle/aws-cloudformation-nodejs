### Synopsis
2016-07-01

This is for interview with Francis Naoum.

CloudFormation JSON template spins up amzn-ami-hvm-2016.03.3.x86_64-gp2 (ami-dc361ebf) on t2.micro instance in Sydney region behind ELB with security group only allowing SSH/22 and HTTP/8080 inbound. As a part of user data, it will perform the following bootstraping:

### Code
```sh
$ sudo yum -y update
$ sudo yum -y install docker                                        #install Docker v1.11.1
$ sudo gpasswd -a ec2-user docker                                   #add ec2-user to the docker group
$ sudo su ec2-user                                                  #workaround for logout/login after user added to the group
$ sudo service docker restart                                       #restarting the service after the workaround
$ docker pull luckylittle/aws-cloudformation-nodejs                 #download image
$ docker run -p 8080:8080 -d luckylittle/aws-cloudformation-nodejs  #run container in the background and map port 8080
```

### Result
```sh
curl http://<ELB-public-IP-address>/
```
will show message 'Hello world and Francis Naoum!'

### Installation
Amazon Web Services console --> CloudFormation --> Create New Stack --> Upload a template to Amazon S3 --> 'interview.json.template' --> Next --> Stack name: [    ] --> InstanceType: t2.micro --> KeyName: [    ] --> Next --> Key: [    ] --> Value: [    ] --> Next --> Create

### Contributors
Lucian Maly <lucian.maly@oracle.com>
