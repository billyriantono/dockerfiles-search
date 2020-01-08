FROM land007/ubuntu-codemeter:latest

MAINTAINER Yiqiu Jia <yiqiujia@hotmail.com>

RUN apt-get install -y build-essential cmake

RUN echo $(date "+%Y-%m-%d_%H:%M:%S") >> /.image_times
RUN echo $(date "+%Y-%m-%d_%H:%M:%S") > /.image_time
RUN echo "land007/ubuntu-build-codemeter" >> /.image_names
RUN echo "land007/ubuntu-build-codemeter" > /.image_name

#docker stop ubuntu-build-codemeter ; docker rm ubuntu-build-codemeter ; docker run -it --privileged --name ubuntu-build-codemeter land007/ubuntu-build-codemeter:latest
