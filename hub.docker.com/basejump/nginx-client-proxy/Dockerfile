### Dockerfile
#
# Basejump NGINX 

FROM basejump/build-base
MAINTAINER Devon Weller <dweller@atlasworks.com>

# nginx repo
ADD nginx-release.repo /etc/yum.repos.d/

# install nginx and PHP packages
RUN yum -y install nginx python-pip

# make nginx run in foreground
RUN echo "" >> /etc/nginx/nginx.conf
RUN echo "daemon off;" >> /etc/nginx/nginx.conf
RUN sed -i "s/http {/http {\n    server_names_hash_bucket_size 128;/g" /etc/nginx/nginx.conf

# install supervisord
# RUN echo "NETWORKING=yes" > /etc/sysconfig/network
RUN pip install "pip>=1.4,<1.5" --upgrade
RUN pip install supervisor

# copy supervisord conf file
ADD supervisord.conf /etc/


# networking
EXPOSE 80

# run supervisord as the command
CMD ["supervisord", "-c", "/etc/supervisord.conf", "-n"]


