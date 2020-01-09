FROM ubuntu:18.04
LABEL maintainer="kwonghung.yip@gmail.com"

ENV SDKMAN_DIR="/usr/local/sdkman"
ENV SDK_JDK_VER="8.0.191-oracle"

SHELL ["/bin/bash","-c"]

RUN apt-get update && apt-get install -y curl zip unzip 

RUN curl -s "https://get.sdkman.io" | bash
#RUN /bin/bash -c "source ${SDKMAN_DIR}/bin/sdkman-init.sh && sdk version"
#RUN source ${SDKMAN_DIR}/bin/sdkman-init.sh && sdk version

#Change the sdkman setting to enable installation in slient mode
RUN sed -i -e 's/sdkman_auto_answer=false/sdkman_auto_answer=true/' ${SDKMAN_DIR}/etc/config

RUN source ${SDKMAN_DIR}/bin/sdkman-init.sh; \
    sdk install java ${SDK_JDK_VER}; \
    sdk list java; \
    sdk offline; \
    sdk flush archives; \
    sdk flush temp;

ENV JAVA_HOME=${SDKMAN_DIR}/candidates/java/${SDK_JDK_VER}
ENV PATH=${JAVA_HOME}/bin:${PATH}

RUN java -version

CMD ["bash"]