FROM centos:7
ENV LANG C.UTF-8
LABEL author=Formattoday email=616099456@qq.com site=https://zhangqin56.cn
WORKDIR /opt/hexo
RUN yum install -y  epel-release && \
yum install -y nodejs \
&& npm install hexo-cli -g  && hexo init Formattoday && cd Formattoday && npm install
WORKDIR Formattoday
EXPOSE 4000
ENTRYPOINT ["hexo","server"]
