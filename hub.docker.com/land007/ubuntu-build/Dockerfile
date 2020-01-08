FROM land007/ubuntu:latest

MAINTAINER Yiqiu Jia <yiqiujia@hotmail.com>

RUN apt-get install -y build-essential cmake

RUN echo $(date "+%Y-%m-%d_%H:%M:%S") >> /.image_times && \
	echo $(date "+%Y-%m-%d_%H:%M:%S") > /.image_time && \
	echo "land007/ubuntu-build" >> /.image_names && \
	echo "land007/ubuntu-build" > /.image_name

#docker stop ubuntu-build ; docker rm ubuntu-build ; docker run -it --privileged --name ubuntu-build land007/ubuntu-build:latest
