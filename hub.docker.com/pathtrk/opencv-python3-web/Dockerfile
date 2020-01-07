from pathtrk/opencv-python3-centos7

maintainer Ryosuke Goto <ryosuke.goto@gmail.com>

# Install the dependencies
RUN yum -y update
RUN yum install -y yum-plugin-ovl
RUN rpm -ivh https://kojipkgs.fedoraproject.org//packages/http-parser/2.7.1/3.el7/x86_64/http-parser-2.7.1-3.el7.x86_64.rpm
RUN yum install -y epel-release
RUN yum install -y nodejs npm
RUN yum install -y pandoc
RUN python3.5 -m pip install pypandoc
