FROM centos:6.8
# Î¬»¤ÕßÐÅÏ¢
MAINTAINER hylexus "hylexus@163.com"
# ½«DockerfileÉÏÏÂÎÄÖÐµÄnginx.repo¸´ÖÆµ½ÈÝÆ÷ÖÐµÄyumÔ´Î»ÖÃ
COPY ./nginx.repo /etc/yum.repos.d/nginx.repo
RUN yum makecache
# °²×°nginx
RUN yum install -y nginx
# ÐÞ¸ÄnginxÊ×Ò³ÐÅÏ¢
RUN echo "home page of container niginx server" > /usr/share/nginx/html/index.html
# ±©Â¶80¶Ë¿Ú
EXPOSE 80