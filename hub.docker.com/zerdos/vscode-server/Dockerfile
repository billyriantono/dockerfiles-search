FROM node:8.15.0

ENV VSCODE_VERSION 1.32.0

RUN apt-get update && apt-get install -y \
	libxkbfile-dev \
	libsecret-1-dev

WORKDIR /src
COPY . .

# This takes ages and always dies in the end. :(
# RUN yarn --frozen-lockfile && yarn task build:server:binary

# Make the debugging easier - and the rebuilds faster
# and our life happier lets break up the build to sequential parts
RUN yarn --frozen-lockfile 
ENV NODE_ENV production

RUN yarn task vscode:install
RUN yarn task build:bootstrap-fork
RUN yarn task build:web
RUN yarn task build:server:bundle
RUN yarn task build:app:browser
RUN yarn task build:server:binary:package

# We deploy with ubuntu so that devs have a familiar environment.
FROM ubuntu:18.10
WORKDIR /root/project

COPY --from=0 /src/packages/server/cli-linux-x64 /usr/local/bin/code-server
EXPOSE 8443

RUN apt-get update && apt-get install -y \
	openssl \
	net-tools \
	git \
	locales \
	sudo \
	dumb-init

RUN locale-gen en_US.UTF-8
# We unfortunately cannot use update-locale because docker will not use the env variables
# configured in /etc/default/locale so we need to set it manually.
ENV LC_ALL=en_US.UTF-8

RUN adduser --gecos '' --disabled-password coder
RUN echo "coder ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers.d/nopasswd

USER coder
# We create first instead of just using WORKDIR as when WORKDIR creates, the user is root.
#  RUN mkdir -p /home/coder/project
WORKDIR /home/coder/project

COPY --from=0 /src/packages/server/cli-linux-x64 /usr/local/bin/code-server
EXPOSE 8443

ENTRYPOINT ["dumb-init", "code-server"]
