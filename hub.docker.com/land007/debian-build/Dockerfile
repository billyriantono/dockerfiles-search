FROM land007/debian:latest

MAINTAINER Yiqiu Jia <yiqiujia@hotmail.com>

RUN apt-get install -y build-essential cmake

RUN echo $(date "+%Y-%m-%d_%H:%M:%S") >> /.image_times
RUN echo $(date "+%Y-%m-%d_%H:%M:%S") > /.image_time
RUN echo "land007/debian-build" >> /.image_names
RUN echo "land007/debian-build" > /.image_name

#docker stop debian-build ; docker rm debian-build ; docker run -it --privileged --name debian-build land007/debian-build:latest
