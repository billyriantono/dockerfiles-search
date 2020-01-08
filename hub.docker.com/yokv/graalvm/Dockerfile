FROM oracle/graalvm-ce:19.2.0

RUN yum update -y
RUN gu install native-image

ENV JAVA_HOME=/opt/graalvm-ce-19.2.0
ENV PATH=${JAVA_HOME}/bin:${PATH}
