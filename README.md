### Synopsis:
__2016-07-02__
__Latest version: 1.5__
This was created for an interview with Francis Naoum from AMP.

### Task:
Compose the Amazon Web Services CloudFormation template that will create a stack running one Elastic Compute Cloud instance behind one Elastic Load Balancer. Simple Node.js "Hello World" container running in Docker will be listening on this instance. The stack must be also highly secure with no unnecessary ports open to the world.

### Solution:
1. Download raw **interview.json** from here.
2. Go to Amazon Web Services console --> CloudFormation --> Create New Stack --> Upload a template to Amazon S3 --> **interview.json** --> Next --> Stack name: [ XXX ] --> KeyName: [ XXX ] --> Next --> Key: [ XXX ] --> Value: [ XXX ] --> Next --> Create.
3. Wait 186 seconds for the following resources to be completed:
   * AWS::ElasticLoadBalancing::LoadBalancer
   * AWS::EC2::SecurityGroup
   * AWS::AutoScaling::LaunchConfiguration
   * AWS::AutoScaling::AutoScalingGroup
4. Click on Outputs --> WebsiteURL value to obtain ELB's DNS name.

### Bootstraping code:
```sh
$ sudo yum update -y aws-cfn-bootstrap                              # update AWS CloudFormation Helper Scripts
$ sudo yum -y install docker                                        # install Docker (currently v1.11.1)
$ sudo gpasswd -a ec2-user docker                                   # add ec2-user to the docker group
$ sudo su ec2-user                                                  # workaround for logout/login after ec2-user added to the group
$ sudo service docker restart                                       # restarting the Docker service after the previous workaround
$ docker pull luckylittle/aws-cloudformation-nodejs                 # download Node.js image from my Docker Hub repo
$ docker run -p 8080:8080 -d luckylittle/aws-cloudformation-nodejs  # run container in the background and map port 8080
```

### Testing:
```sh
$ curl http://<ELB-public-IP-address>/
```
This will show message **Hello world and Francis Naoum!**

### Contributors
Lucian Maly <<lucian.maly@oracle.com>>
