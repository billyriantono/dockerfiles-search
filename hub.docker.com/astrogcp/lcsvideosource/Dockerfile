FROM  ubuntu:16.04
RUN apt-get update -y
RUN apt-get -y install bc curl jq
#Time
ENV TW=Asia/Taipei
RUN ln -snf /usr/share/zoneinfo/$TW /etc/localtime && echo $TW > /etc/timezone
