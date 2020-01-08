# from centos:7

# RUN yum -y install epel-release wget which; \
#     yum -y update; \

# RUN yum -y install nodejs npm; \
#     yum clean all

# from huashiyiqike/centos-epel

# RUN   yum -y update; \
#      yum -y install epel-release wget which &&  yum clean all;

# RUN yum -y install nodejs npm; && yum clean all

from huashiyiqike/nodejs

RUN npm i yog2 -g  --cache=/tmp/cache && rm -r /tmp/cache
#RUN npm i yog2 -g   --registry=https://registry.npm.taobao.org  --cache=/tmp/cache && rm -r /tmp/cache
RUN mkdir -p /src
ADD src /src
WORKDIR /src/
CMD ["echo ", " yog"]