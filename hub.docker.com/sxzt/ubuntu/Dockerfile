# ubuntu 18.04 with tzdata

FROM ubuntu:18.04
MAINTAINER sxzt "sjzt2513@163.com"

#setting timezone
RUN apt -y update && \
	apt -y upgrade && \
	apt -y install tzdata && \
	apt -y install wget && \
	apt -y clean && \
    apt -y autoclean && \
    apt -y autoremove 
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone 





