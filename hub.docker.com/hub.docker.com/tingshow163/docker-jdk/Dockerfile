FROM alpine:3.9
  
LABEL maintainer="bubble"
LABEL jdkversion="1.8.0_211"

ADD jdk-8u211-linux-x64.tar.gz /usr/local
# Alpine glic, see more https://github.com/sgerrand/alpine-pkg-glibc
RUN set -eux ;\
        apk --no-cache add ca-certificates wget fontconfig ttf-dejavu && \
        wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub && \
        wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.29-r0/glibc-2.29-r0.apk && \
        wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.29-r0/glibc-bin-2.29-r0.apk && \
        apk add glibc-2.29-r0.apk; \
        apk add glibc-bin-2.29-r0.apk ;\
        rm -rf glibc-2.29-r0.apk glibc-bin-2.29-r0.apk

ENV JAVA_HOME=/usr/local/jdk1.8.0_211
ENV JRE_HOME=${JAVA_HOME}/jre
ENV CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib:$CLASSPATH
ENV JAVA_PATH=${JAVA_HOME}/bin:${JRE_HOME}/bin
ENV PATH=$PATH:${JAVA_PATH}

CMD ["java","-version"]
