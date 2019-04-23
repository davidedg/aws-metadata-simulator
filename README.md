# AWS Instance Metadata Simulator

This project provides an incomplete capability of simulating AWS EC2 [instance metadata](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-metadata.html). It was created to allow for testing of applications that utilize EC2 instance metadata in non-AWS environments or for testing applications in AWS against different metadata values.

## Quick Install

```
wget https://raw.githubusercontent.com/mtnfog/aws-metadata-simulator/master/install.sh && chmod +x install.sh && ./install.sh
```

## Manual Install Steps

`go get -u github.com/mtnfog/aws-metadata-simulator`

To run:

If specific values for the instance metadata are desired set those values in `metadata.toml` then run it:

`go run main.go`

To use a different file as the configuration give the filename as a command line argument:

`go run main.go other.toml`


## Metadata Service Binding

In Windows, you can simply add secondary IP address 169.254.169.254 and bind port 80
In Linux, to redirect traffic from port 80 to port 8080:

`sudo iptables -t nat -A OUTPUT -p tcp -d 169.254.169.254 --dport 80 -j DNAT --to-destination 127.0.0.1:8080`


## Using

Now when applications make requests to the EC2 instance metadata the simulator will answer. You can test it:

```
Invoke-RestMethod -Method Get -Uri http://169.254.169.254/2009-04-04/meta-data/instance-id
curl http://169.254.169.254/latest/meta-data/hostname`
```
