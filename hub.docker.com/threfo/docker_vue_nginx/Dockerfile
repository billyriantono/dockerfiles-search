#
# client base image for nginx + vuejs
# 
# version   0.1
# 
FROM  nginx:1.10
MAINTAINER Yang Jun <yangjun@threfo.com>

# Install node6, git
RUN apt update
RUN apt install -y wget
RUN wget -qO- https://deb.nodesource.com/setup_6.x | bash -
RUN apt install -y nodejs git