aws-distro-rpm-comparison
=========================

Compare available RPMs (RPM provides) in different Linux distros on AWS.

Example usage (for eu-west-1):
```
./aws-distro-rpm-comparison.py --verbose vpc-123456 root@ami-30ff5c47 ami-6e7bd919 ami-9cfd53eb
```

Please use your own VPC or send me pull request for VPC autodetection (or auto-creation)

*Notes:*
* Your VPC must automatically associate public IPs to new instances.
* Sometimes an instance is not accessible. Probably because our SSH connection comes too soon (e.g. before cloud-init could install the keys).

Installation
------------

1. Install the dependencies (Ubuntu: `sudo apt-get install fabric python-boto python-docopt`)
1. Checkout this github repo
1. Run the script with a VPC ID and one or several AMI IDs

Usage
-----

```
$ ./aws-distro-rpm-comparison.py -h
Create EC2 instances with different Linux distros and compare
the available RPMs on them.

Usage:
  aws-distro-rpm-comparions.py [options] VPC_ID USER@AMI_ID...

Arguments:
  VPC_ID        VPC_ID to use
  USER@AMI_ID   AMI IDs to use with their respective SSH user

Options:
  -h --help            show this help message and exit
  --version            show version and exit
  --region=REGION      use this region [default: eu-west-1]
  --type=TYPE          EC2 instance type [default: t2.micro]
  --defaultuser=USER   Default user to use for USER@AMI_ID [default: ec2-user]
  --verbose            Verbose logging
  --debug              Debug logging
  --interactive        Dump SSH Key and IPs and wait for before removing EC2 instances

Notes:

* The AMI_IDs and the EC2 instance type must match (HVM or PV)
```

Results
------

The result(s) are text files containing an RPM provides list from all packages that are available in the default YUM repos. The list is sorted and uniqed. The text files are named with the AMI name and description.

See the results folder for sample results.
