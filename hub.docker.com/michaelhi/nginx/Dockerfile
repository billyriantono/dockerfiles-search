FROM centos

MAINTAINER michaelhe<mching.08@gmail.com>

RUN echo '[nginx]' >>  /etc/yum.repos.d/nginx.repo \
	&& echo 'name=nginx repo' >> /etc/yum.repos.d/nginx.repo \
	&& echo 'baseurl=http://nginx.org/packages/centos/7/$basearch/' >> /etc/yum.repos.d/nginx.repo \
	&& echo 'gpgcheck=0' >> /etc/yum.repos.d/nginx.repo \
  	&& echo 'enabled=1' >> /etc/yum.repos.d/nginx.repo \
	&& yum -y install nginx \
	&& echo '<h1>Hello, In My Docker!</h1>' > /usr/share/nginx/html/index.html

# 对外暴露80端口
EXPOSE 80

# 包装一层启动命令
CMD ["nginx", "-g", "daemon off;"]
