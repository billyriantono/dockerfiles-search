FROM alpine:latest

# add repositories
RUN echo -e "https://mirror.tuna.tsinghua.edu.cn/alpine/latest-stable/main\n\
https://mirror.tuna.tsinghua.edu.cn/alpine/latest-stable/community" > /etc/apk/repositories

#install curl bash openjdk8 iproute2（ss） drill（dns）
RUN apk --update add bash openjdk8-jre curl iproute2 drill && \
      rm -rf /var/cache/apk/*

# Set environment
ENV JAVA_HOME /usr/lib/jvm/default-jvm/jre
ENV PATH ${PATH}:${JAVA_HOME}/bin
