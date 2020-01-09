FROM nereus/gs-sdkman:latest

ENV SDK_JDK_VER="10.0.0-openjdk"

SHELL ["/bin/bash","-c"]

RUN source ${SDKMAN_DIR}/bin/sdkman-init.sh; \
sdk install java ${SDK_JDK_VER}; \
sdk list java; \
sdk offline; \
sdk flush archives; \
sdk flush temp;

ENV JAVA_HOME=${SDKMAN_DIR}/candidates/java/${SDK_JDK_VER}
ENV PATH=${JAVA_HOME}/bin:${PATH}

CMD ["bash"]