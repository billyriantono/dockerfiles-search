#
# GitLab CI react-native-android v0.1.1
#
# https://hub.docker.com/r/shoorkaii/gitlab-ci-react/
# https://github.com/shoorkaii/gitlab-ci-react


FROM ubuntu:18.04
MAINTAINER Reza Ranjkesh Shoorkaii <shoorkaii@gmail.com>

RUN echo "Installing Dependencies" \
	&& apt-get -qq update \
    && apt-get install -qqy --no-install-recommends\
    curl\
    bzip2 \
    apt-utils\
    git-core\
    docker.io \
    npm\
    gnupg \
    zlib1g \
    unzip \
    wget \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN echo "Installing Node.JS" \
	&& curl -sL https://deb.nodesource.com/setup_10.x | bash -

RUN echo "Installing Yarn Deb Source" \
	&& curl -sS http://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
	&& echo "deb http://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list