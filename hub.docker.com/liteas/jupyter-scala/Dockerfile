FROM jupyter/base-notebook

LABEL maintainer="Liteas <liteas.sk@gmail.com>"

USER root

RUN mkdir -p /usr/share/man/man1 && \
    apt-get update && \
    apt-get install -y --no-install-recommends openjdk-8-jre && \
    apt-get install -y wget

ENV SCALA_VERSION 2.12.8
RUN wget https://downloads.lightbend.com/scala/$SCALA_VERSION/scala-$SCALA_VERSION.deb && \
    dpkg -i scala-$SCALA_VERSION.deb && \
    rm -f scala-$SCALA_VERSION.deb 

ENV ALMOND_VERSION 0.4.0
RUN  wget -O coursier https://git.io/coursier && \
    chmod +x coursier && \
    ./coursier bootstrap \
    -r jitpack \
    -i user -I user:sh.almond:scala-kernel-api_$SCALA_VERSION:$ALMOND_VERSION \
    sh.almond:scala-kernel_$SCALA_VERSION:$ALMOND_VERSION \
    -o almond && \
    ./almond --install --global && \
    rm -f almond coursier

RUN echo "i am here" > /usr/local/share/jupyter/kernels/scala/foo.txt
ENV ALMOND_GLOBAL true

USER $NB_UID
