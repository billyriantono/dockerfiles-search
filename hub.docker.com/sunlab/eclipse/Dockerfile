FROM nvidia/cuda:9.2-cudnn7-devel

# base infrastructure
RUN apt-get update \
        && apt-get --yes install \
                munge libmunge-dev libmysqld-dev libpam0g-dev \
                curl wget tmux htop vim gcc make git lsof unzip \
                openjdk-8-jdk \
        && rm -rf /var/lib/apt/lists/*




ENV SCALA_VERSION 2.11.8
RUN wget -O scala.deb  https://downloads.lightbend.com/scala/${SCALA_VERSION}/scala-${SCALA_VERSION}.deb \
        && dpkg -i scala.deb \
        && rm -f scala.deb

# SBT
ENV SBT_VERSION 1.1.0
RUN wget https://github.com/sbt/sbt/releases/download/v${SBT_VERSION}/sbt-${SBT_VERSION}.tgz ; \
    tar -xzf sbt-${SBT_VERSION}.tgz ; \
    rm -rf sbt-${SBT_VERSION}.tgz ; \
    mv sbt /usr/lib/ ; \
    ln -sf /usr/lib/sbt/bin/sbt /usr/bin/
