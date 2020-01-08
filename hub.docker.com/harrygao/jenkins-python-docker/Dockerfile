FROM jenkins/jenkins
USER root

# 更换 debian 源
# COPY sources.list /etc/apt/sources.list
RUN echo "deb http://mirrors.aliyun.com/debian/ stretch main non-free contrib\n\
deb-src http://mirrors.aliyun.com/debian/ stretch main non-free contrib\n\
deb http://mirrors.aliyun.com/debian-security stretch/updates main\n\
deb-src http://mirrors.aliyun.com/debian-security stretch/updates main\n\
deb http://mirrors.aliyun.com/debian/ stretch-updates main non-free contrib\n\
deb-src http://mirrors.aliyun.com/debian/ stretch-updates main non-free contrib\n\
deb http://mirrors.aliyun.com/debian/ stretch-backports main non-free contrib\n\
deb-src http://mirrors.aliyun.com/debian/ stretch-backports main non-free contrib" > /etc/apt/sources.list

RUN apt-get update
RUN apt-get install -y python

# 更换 pip 源
# COPY pip.conf /root/.pip/pip.conf
RUN mkdir /root/.pip
RUN echo "[global]\n\
trusted-host = mirrors.aliyun.com\n\
index-url = https://mirrors.aliyun.com/pypi/simple" > /root/.pip/pip.conf

RUN curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
RUN python get-pip.py --verbose

RUN pip install virtualenv

USER jenkins

