FROM land007/python:latest

MAINTAINER Yiqiu Jia <yiqiujia@hotmail.com>

RUN pip install shadowsocks

RUN echo $(date "+%Y-%m-%d_%H:%M:%S") >> /.image_times
RUN echo $(date "+%Y-%m-%d_%H:%M:%S") > /.image_time
RUN echo "land007/python-shadowsocks" >> /.image_names
RUN echo "land007/python-shadowsocks" > /.image_name


#docker stop python-shadowsocks ; docker rm python-shadowsocks ; docker run -it --privileged --name python-shadowsocks land007/python-shadowsocks:latest
#> docker buildx build --platform linux/amd64,linux/arm64,linux/arm/v7 -t land007/python-shadowsocks --push .
