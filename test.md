title: Centos7配置软件源
date: 2015-12-05 16:09:06
categories:
- 环境配置
tags:
- caffe
- deep learning
- python
---
刚从ubuntu换到centos7，很多软件需要自己下载，但是centos自带的源经常收不到对应的软件和包。  
配置软件源需要到`/etc/yum.repos.d/`目录下修改repo文件；  
#1. 先备份原来的软件源（需要root权限)

```sh
sudo mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
```

2. 下载第三方的软件源添加进去  
---

	wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo //阿里云的镜像，资源还是比较多的
	yum clean all
	yum makecache    //生成缓存即可
还有一些比较好用的国内源

网易163：[http://mirrors.163.com/.help/centos.html](http://mirrors.163.com/.help/centos.html)

华中科技大学：[http://mirrors.hust.edu.cn/help.html#centos](http://mirrors.hust.edu.cn/help.html#centos)

浙江大学：[http://mirrors.lifetoy.org/](http://mirrors.lifetoy.org/)


3. 添加RHEL源和一些国外源
---
	yum localinstall http://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-6.noarch.rpm -y
	
> 有时候可能出现404错误，这是因为这个有更新了，打开地址[http://dl.fedoraproject.org/pub/epel/7/x86_64/e/](http://dl.fedoraproject.org/pub/epel/7/x86_64/e/)搜索epel-release找到对应的地址替换即可。

	cd /etc/yum.repos.d/
	vim puias-computational.repo 
	输入下面这些：
	[PUIAS_computational]
	name=PUIAS computational Base $releasever - $basearch
	mirrorlist=http://puias.math.ias.edu/data/puias/computational/$releasever/$basearch/mirrorlist
	#baseurl=http://puias.math.ias.edu/data/puias/computational/$releasever/$basearch
	gpgcheck=1
	gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-puias 
导入key：

	rpm --import http://puias.princeton.edu/data/puias/7/x86_64/os/RPM-GPG-KEY-puias
生产缓存：

	yum makecache
	sudo yum update

## Ref ##
1. [http://www.linuxidc.com/Linux/2015-03/114690.htm](http://www.linuxidc.com/Linux/2015-03/114690.htm)
