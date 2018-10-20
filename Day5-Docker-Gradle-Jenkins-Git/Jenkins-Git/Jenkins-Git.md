Virtualbox решение проблемы с vboxdrv
https://askubuntu.com/questions/41118/virtualbox-kernel-driver-not-installed

$ sudo apt-get autoremove virtualbox-dkms
$ sudo apt-get install build-essential linux-headers-`uname -r` dkms virtualbox-dkms

$ sudo modprobe vboxdrv
$ sudo modprobe vboxnetflt

The goal is to install Jenkins of 1st machine, which will check Git repo on 2d machine.

* Install Jenkins on 1st machine, use this instructions:
https://pkg.jenkins.io/debian/

or this instructions:
https://wiki.jenkins.io/display/JENKINS/Installing+Jenkins+on+Ubuntu


* Install Git server on 2d machine, use this instruction:
https://git-scm.com/book/ru/v1/Git-на-сервере-Настраиваем-сервер

* Jenkins+Git integration:
http://www.swtestacademy.com/jenkins-git-integration-ubuntu/
https://wiki.jenkins.io/display/JENKINS/Git+Plugin

* Setup and check testing in Jenkins.
For example, use this manual:
https://habrahabr.ru/post/170847/
