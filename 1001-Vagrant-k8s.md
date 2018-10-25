```
cd /Volumes/Macintosh\ HD/Users/Shared/Data/VMs/vagrant/k8s
```

```
vagrant ssh n1
# vagrant
#su root 
sudo yum -y install epel-release telnet vim htop lsof
sudo yum -y update

# master
sudo yum install -y etcd kubernetes-master ntp flannel
# nodes
sudo yum install -y kubernetes-node ntp flannel docker

systemctl start ntpd && systemctl enable ntpd && ntpdate ntp1.aliyun.com && hwclock -w


#sudo yum -y install python-pip
#sudo pip install --upgrade pip
#sudo pip install ansible
#ansible --version
```

*	http://blog.51cto.com/2168836/2106963?utm_source=oschina-app
