FROM debian:sid
MAINTAINER Amane Katagiri <amane@ama.ne.jp>

ENV REDPEN_HOME /redpen
ENV REDPEN_TMP /tmp/redpen
ENV REDPEN_REPO_TMP /tmp/redpen/repo
RUN mkdir $REDPEN_HOME \
    && apt-get update && apt-get install -y --no-install-recommends maven curl unzip \
    && mkdir $REDPEN_TMP \
    && mkdir $REDPEN_REPO_TMP \
    && curl -Ss -L https://github.com/redpen-cc/redpen/releases/download/redpen-1.10.1/redpen-1.10.1.tar.gz | tar zx -C $REDPEN_HOME --strip-components 1 \
    && curl -Ss -L https://github.com/glabra/redpen-japanese-novel-style/archive/master.zip > $REDPEN_TMP/redpen-japanese-novel-style.zip \
    && curl -Ss -L https://github.com/glabra/redpen-hankaku-alphabet/archive/master.zip > $REDPEN_TMP/redpen-hankaku-alphabet.zip \
    && unzip $REDPEN_TMP/redpen-japanese-novel-style.zip -d $REDPEN_REPO_TMP/redpen-japanese-novel-style \
    && unzip $REDPEN_TMP/redpen-hankaku-alphabet.zip -d $REDPEN_REPO_TMP/redpen-hankaku-alphabet \
    && mv $REDPEN_REPO_TMP/redpen-japanese-novel-style/* $REDPEN_TMP/redpen-japanese-novel-style \
    && mv $REDPEN_REPO_TMP/redpen-hankaku-alphabet/* $REDPEN_TMP/redpen-hankaku-alphabet \
    && cd $REDPEN_TMP/redpen-japanese-novel-style \
    && ln -s $REDPEN_HOME/lib . && mvn install && cp target/*.jar $REDPEN_HOME/lib/ \
    && cd $REDPEN_TMP/redpen-hankaku-alphabet \
    && ln -s $REDPEN_HOME/lib . && mvn install && cp target/*.jar $REDPEN_HOME/lib/ \
    && apt-get autoclean -y \
    && apt-get clean -y \
    && rm -rf $REDPEN_TMP /var/lib/apt/lists/*
COPY data/dict $REDPEN_HOME/dict
COPY data/conf.xml $REDPEN_HOME/redpen-conf.xml
COPY data/redpen-runner /bin/redpen-runner
WORKDIR /data
CMD ["/bin/bash"]
