FROM land007/debian-codemeter:latest

MAINTAINER Yiqiu Jia <yiqiujia@hotmail.com>

RUN apt-get install -y build-essential cmake

RUN echo $(date "+%Y-%m-%d_%H:%M:%S") >> /.image_times
RUN echo $(date "+%Y-%m-%d_%H:%M:%S") > /.image_time
RUN echo "land007/debain-build-codemeter" >> /.image_names
RUN echo "land007/debain-build-codemeter" > /.image_name


#docker stop debain-build-codemeter ; docker rm debain-build-codemeter ; docker run -it --privileged --name debain-build-codemeter land007/debain-build-codemeter:latest
