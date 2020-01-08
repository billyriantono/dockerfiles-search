FROM nginx:stable

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y git
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone && \
apt-get install tzdata && \
dpkg-reconfigure --frontend noninteractive tzdata
CMD ['nginx', '-g', 'daemon off;']