#Infrastructure Setup for Pi

Pi-1: 192.168.1.8/24<br />
Pi-2: 192.168.1.4/24<br />

#Installing Docker 

$curl -sSL https://get.docker.com/ | sh<br />

#Verify the docker version:
<pre>
pi@raspberrypi:~ $ sudo docker version
Client:
 Version:      1.12.1
 API version:  1.24
 Go version:   go1.6.3
 Git commit:   23cf638
 Built:        Thu Aug 18 05:31:15 2016
 OS/Arch:      linux/arm

Server:
 Version:      1.12.1
 API version:  1.24
 Go version:   go1.6.3
 Git commit:   23cf638
 Built:        Thu Aug 18 05:31:15 2016
 OS/Arch:      linux/arm
pi@raspberrypi:~ $
</pre>
#Let's search for CentOS ARM container which I created and is available under Dockerhub.

pi@raspberrypi:~/Desktop $ sudo docker search ajeetraina
NAME                             DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
ajeetraina/nagios                Docker container for Monitoring Dell Physi...   0
ajeetraina/dell-oob-monitoring   Out-of-Band Monitoring System for Dell Har...   0
ajeetraina/dell-syscfg           Running Dell SYSCFG inside Docker container     0
ajeetraina/centos7-arm                                                           0
ajeetraina/nagios-docker         Docker container for Monitoring Dell Physi...   0
ajeetraina/syscfg-minimal        Running Dell SYSCFG inside Docker containe...   0

#Running Your First Docker container:

pi@raspberrypi:~/Desktop $ sudo docker run -it ajeetraina/centos7-arm cat /etc/os-release
Unable to find image 'ajeetraina/centos7-arm:latest' locally
latest: Pulling from ajeetraina/centos7-arm

5584ea4c92c5: Pull complete
a3ed95caeb02: Pull complete
Digest: sha256:10989b1b7a3bdf826857ba5b3348956d495b9be1ced644a3aa7321cfbd705b04
Status: Downloaded newer image for ajeetraina/centos7-arm:latest
NAME="CentOS Linux"
VERSION="7 (Core)"
ID="centos"
ID_LIKE="rhel fedora"
VERSION_ID="7"
PRETTY_NAME="CentOS Linux 7 (Core)"
ANSI_COLOR="0;31"
CPE_NAME="cpe:/o:centos:centos:7"
HOME_URL="https://www.centos.org/"
BUG_REPORT_URL="https://bugs.centos.org/"

CENTOS_MANTISBT_PROJECT="CentOS-7"
CENTOS_MANTISBT_PROJECT_VERSION="7"
REDHAT_SUPPORT_PRODUCT="centos"
REDHAT_SUPPORT_PRODUCT_VERSION="7"

pi@raspberrypi:~/Desktop $

#Listing the Docker Image:

pi@raspberrypi:~ $ sudo docker images
REPOSITORY               TAG                 IMAGE ID            CREATED             SIZE
ajeetraina/centos7-arm   latest              495db0a341d8        20 hours ago        210.6 MB
pi@raspberrypi:~ $

#You can verify the information:

pi@raspberrypi:~ $ sudo docker info
Containers: 1
 Running: 0
 Paused: 0
 Stopped: 1
Images: 1
Server Version: 1.12.1
Storage Driver: overlay
 Backing Filesystem: extfs
Logging Driver: json-file
Cgroup Driver: cgroupfs
Plugins:
 Volume: local
 Network: overlay bridge null host
Swarm: inactive
Runtimes: runc
Default Runtime: runc
Security Options:
Kernel Version: 4.4.11-v7+
Operating System: Raspbian GNU/Linux 8 (jessie)
OSType: linux
Architecture: armv7l
CPUs: 4
Total Memory: 925.5 MiB
Name: raspberrypi
ID: FBMQ:EYQC:36ZV:L5OS:PQMB:HQ3X:OZM4:DIAU:N7T7:2B2D:SZRR:Q3DB
Docker Root Dir: /var/lib/docker
Debug Mode (client): false
Debug Mode (server): false
Registry: https://index.docker.io/v1/
WARNING: No swap limit support
WARNING: No kernel memory limit support
WARNING: No cpu cfs quota support
WARNING: No cpu cfs period support
WARNING: No cpuset support
Insecure Registries:
 127.0.0.0/8
pi@raspberrypi:~ $

#Starting the container:

pi@raspberrypi:~ $ sudo docker run -dit ajeetraina/centos7-arm /bin/bash
f0641cd68756ef2a0ab337ac06cfef6ce49010a5e3a538374c8b3473c87d1447

#Verifying container has started or not:

pi@raspberrypi:~ $ sudo docker ps
CONTAINER ID        IMAGE                    COMMAND             CREATED             STATUS              PORTS               NAMES
f0641cd68756        ajeetraina/centos7-arm   "/bin/bash"         5 seconds ago       Up 4 seconds                            drunk_meitner
pi@raspberrypi:~ $

#Entering into into the container?

pi@raspberrypi:~ $ sudo docker attach f064
[root@f0641cd68756 /]#
[root@f0641cd68756 /]#

You just need first few snippet of Container ID to enter into the container.

Let's check the kernel version of the container:

[root@f0641cd68756 /]# uname -arn
Linux f0641cd68756 4.4.11-v7+ #888 SMP Mon May 23 20:10:33 BST 2016 armv7l armv7l armv7l GNU/Linux
[root@f0641cd68756 /]#




===============================================

pi@raspberrypi:~/Desktop $ sudo git clone https://github.com/ajeetraina/Docker-Workshop
Cloning into 'Docker-Workshop'...
remote: Counting objects: 18, done.
remote: Compressing objects: 100% (15/15), done.
remote: Total 18 (delta 3), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (18/18), done.
Checking connectivity... done.
pi@raspberrypi:~/Desktop $
