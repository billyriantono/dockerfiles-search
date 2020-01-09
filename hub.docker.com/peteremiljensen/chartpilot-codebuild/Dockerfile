FROM peteremiljensen/chartpilot-codebuild-base

RUN set -ex && apt-get update && apt-get install -y apt-transport-https

RUN set -ex && apt-get install -y git-core && apt-get install -y jq

RUN echo "deb https://dl.bintray.com/sbt/debian /" | sudo tee -a /etc/apt/sources.list.d/sbt.list
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2EE0EA64E40A89B84B2DF73499E82A75642AC823
RUN set -ex \
    && apt-get update \
    && apt-get install -y sbt