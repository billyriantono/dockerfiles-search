# Version: 0.0.1
FROM easyzlj/test:ubuntu
MAINTAINER easyzlj "easyzlj@gmail.com"
#RUN apt-get update
RUN apt-get install -y curl
RUN rm -rf /var/lib/apt/lists/*
ENTRYPOINT [ "curl", "-s", "http://ip.cn" ]

