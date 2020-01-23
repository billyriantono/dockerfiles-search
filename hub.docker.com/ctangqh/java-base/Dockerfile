FROM ctangqh/runtime-base:latest

ENV AppRoot=/app/java   \
    VERSION=1.8.0.222
ENV JAVA_HOME=${AppRoot}
ENV JRE_HOME=$JAVA_HOME/jre
ENV CLASSPATH=.:$JAVA_HOME/jre/lib/rt.jar:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar  
ENV PATH=$JAVA_HOME/bin:${PATH}

ARG BINARY_URL=https://github.com/AdoptOpenJDK/openjdk8-binaries/releases/download/jdk8u222-b10/OpenJDK8U-jdk_x64_linux_hotspot_8u222b10.tar.gz

RUN set -eux; \
    sudo mkdir -p ${AppRoot};  \
    sudo curl -LfsSo ${RunRoot}/openjdk.tar.gz ${BINARY_URL}; \
    sudo tar -xf ${RunRoot}/openjdk.tar.gz --strip-components=1 -C ${AppRoot};  \
    sudo rm -f ${RunRoot}/openjdk.tar.gz;
    
WORKDIR ${RunRoot}

USER ${AppUser}:${AppGroup}

CMD ["/bin/bash"]

