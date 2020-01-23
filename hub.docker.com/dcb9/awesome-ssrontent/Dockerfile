FROM nginx:latest
RUN apt-get update \
    && apt-get -y upgrade \
    && apt-get -y install vim bash wget curl less psmisc python-setuptools tcpdump \
    && easy_install pip==9.0.1 \
    && apt-get clean \
    && ln -sf /bin/bash /bin/sh
    
ADD ["https://gist.githubusercontent.com/dblackdblack/8ee26ab2216cabe411143c349150e6b3/raw", "/etc/nginx/conf.d/default.conf"]
