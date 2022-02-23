## Docker Threat Modeling

>Given Docker's system components and the STRIDE framework, identify five potential threats that may arise.

S - Spoofing:
T - Tampering: An attacker may get control of the docker client.  They could then tamper with with Dockerfiles or the way images are built from Dockerfiles.
R - Repudiation: Similar to above, a client exposure could lead to make illigitmate changes to the system which would be very difficult to observe without special tracking systems.
I - Information Disclosure: A client could expose secrets or environment variables used to generate images.
D - Denial of Service: Traffic could get out of control to the daemon which could crash it and lead to various other compromises.
E - Elevation of Privilege: A Dockerfile that doesn't specify a user might allow someone to execute with root privileges.

## Kubernetes Threat Modeling

>Given Kubernetes' system components and the STRIDE framework, identify five potential threats that may arise.

S - Spoofing: Someone could use a man-in-the-middle attack between a kubelet and the apiserver
T - Tampering:  If etcd is compromised due to insufficient permissions, various configuration parameters could be modified leading to the ability to modify dangerous settings.
R - Repudiation:
I - Information Disclosure: An attacker with privileged access to the cluster could gain access to secrets in the cluster which may provide additional access.
D - Denial of Service: Too much traffic can overwhelm the api server endpoint causing problems with the kube-scheduler.
E - Elevation of Privilege: The privileged flag could be used allowing unauthorized access to the kube-apiserver.

## Docker-bench Run Results and Analysis

>From the failed findings, select and document 3 findings from the Docker-bench results that you want to harden based on the 5 attack surface areas you identified in Step 1. At least 1 of the 3 hardened findings should be different from the ones mentioned in the exercise (i.e. 5.10, 5.14, and 5.22).

2.2  - Ensure network traffic is restricted between containers on the default bridge (Automated)

Add `"icc": false` to `/etc/docker/daemon.json`

2.14 - Ensure containers are restricted from acquiring new privileges (Automated)

Add `"no-new-privileges": true` to `/etc/docker/daemon.json`

2.15 - Ensure live restore is Enabled (Automated)

Add `"live-restore": true` to `/etc/docker/daemon.json`

Failures before hardening: 38, Failures after Hardening: 35
