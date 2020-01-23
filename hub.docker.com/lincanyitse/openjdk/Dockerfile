FROM lincanyitse/glibc
ARG OPENJDK_URL='https://github.com/alibaba/dragonwell8/releases/download/v8.2.2-GA/Alibaba_Dragonwell_8.2.2-GA_Linux_x64.tar.gz'
ENV JAVA_HOME '/usr/local/openjdk'
ENV PATH "${PATH}:${JAVA_HOME}/bin"
RUN set -x \
    && curl -fsSLo /tmp/openjdk.tar.gz ${OPENJDK_URL} \
    && tar zxf /tmp/openjdk.tar.gz -C /usr/local/ \
    && mv /usr/local/j2sdk-image ${JAVA_HOME} \
    && rm -rf /tmp/*
ENV LANG zh_CN.UTF-8
CMD ["java","-version"]