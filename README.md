### Synopsis
2016-06-30

This is for interview with Francis Naoum.

CloudFormation JSON template spins up amzn-ami-hvm-2016.03.3.x86_64-gp2 (ami-dc361ebf) on t2.micro instance in Sydney region with security group only allowing SSH/22 and HTTP/8080 inbound. As a part of user data, it will perform the following bootstraping:

### Code
```sh
$ sudo yum -y update
$ sudo yum -y install docker                                    #install docker v1.11.1
$ sudo gpasswd -a ec2-user docker                               #add current user to the docker group
$ su - ec2-user; id                                             #workaround for logout/login after user added to the group
$ sudo service docker restart                                   #restarting the service after the workaround
$ docker pull google/nodejs-hello                               #download image https://hub.docker.com/r/google/nodejs-hello/
$ docker run -p 8080 --restart="always" -d google/nodejs-hello  #run container in the background and expose port 8080
```

### Installation
Amazon Web Services console --> CloudFormation --> Create New Stack --> Upload a template to Amazon S3 --> 'interview.json.template' --> Next --> Stack name: [    ] --> InstanceType: t2.micro --> KeyName: [    ] --> Next --> Key: [    ] --> Value: [    ] --> Next --> Create

### Contributors
Lucian Maly <lucian.maly@oracle.com>
