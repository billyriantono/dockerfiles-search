FROM ubuntu:latest
MAINTAINER Andreas H. Kelch <ak@mausbrand.de>

#install
RUN apt-get update && apt-get install -y \
	git \
	wget \
	python \
	python-pip \
	python2.7-dev \
	libjpeg62 \
	libjpeg62-dev \
	zlib1g-dev\
	npm \
	unzip

#update node and npm
RUN apt-get update
RUN apt-get -y install curl gnupg
RUN curl -sL https://deb.nodesource.com/setup_11.x  | bash -
RUN apt-get -y install nodejs

RUN npm install -g less
RUN npm install -g gulp
RUN pip install git+https://github.com/pyjs/pyjs.git#egg=pyjs

# Default to UTF-8 file.encoding
ENV LANG=C.UTF-8 \
    LC_ALL=C.UTF-8 \
    LANGUAGE=C.UTF-8

# Xvfb provide an in-memory X-session for tests that require a GUI
ENV DISPLAY=:99

# Create dirs and users
RUN mkdir -p /opt/atlassian/bitbucketci/agent/build \
    && sed -i '/[ -z \"PS1\" ] && return/a\\ncase $- in\n*i*) ;;\n*) return;;\nesac' /root/.bashrc \
    && useradd --create-home --shell /bin/bash --uid 1000 pipelines



COPY buildvi.sh ./
COPY gulp.sh ./

RUN ["chmod", "+x", "buildvi.sh"]
RUN ["chmod", "+x", "gulp.sh"]

WORKDIR /opt/atlassian/bitbucketci/agent/build

ENTRYPOINT /bin/bash