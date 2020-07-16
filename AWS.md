Setting up an AWS Virtual Machine

1. Register with AWS and launch an EC2 instance
First, you need to perform several preparatory steps (if you have already done this before, you can skip them):
Sign up for AWS. You will need to specify your credit card details, but for our project we will use Free Tier instances only, so you should not be charged.
Create a key pair for authentication. If you use Windows, you will also need to install PuTTY to use SSH.
Create security group. You must add rules to a security group to allow you to connect to your future instance from your IP address using SSH. You might want to allow SSH access from all IPv4 addresses (set to 0.0.0.0/0), because your IP might change.
Next, you are ready to create your first EC2 instance:
Launch a free tier instance. For Amazon Machine Image (AMI) choose Ubuntu Server 16.04 LTS.
Connect to your instance using SSH. If you have problems connecting to the instance, try following this troubleshooting guide.
Later on you can start and stop your instance when needed, and terminate it in the end.

2. Set up dependencies and run your project
Install Docker container for Ubuntu with course dependencies. Follow our Docker instructions.

To be able to access IPython notebooks running on AWS, you might want to SSH with port tunneling:

ssh -L 8080:localhost:8080 -i path/to/private_key ubuntu@ec2-XX-XXX-X-XX.us-east-2.compute.amazonaws.com
Then you will be able to see the notebooks on localhost:8080 from your browser on the local machine.

If you're using PuTTY, before you start your SSH connection, go to the PuTTY Tunnels panel. Make sure the «Local» and «Auto» radio buttons are set. Enter the local port 8080 number into the «Source port» box. Enter the destination host name and port number into the «Destination» box, separated by a colon ubuntu@ec2-XX-XXX-X-XX.us-east-2.compute.amazonaws.com:8080. For more details see this guide.

Bring code and data to AWS instance, e.g.
scp -i path/to/your_key.pem -r path/to/local_directory ubuntu@ec2-XX-XXX-X-XX.us-east-2.compute.amazonaws.com:path/to/remote_file
You might need to install WinSCP for data transfer if you are using Windows.

It is also a good practice to use tmux to keep your remote session running even if you disconnect from the machine, e.g. by closing your laptop.
Thus, to run your scripts on the machine, we suggest that you run: ssh -> tmux -> Docker -> Python.
