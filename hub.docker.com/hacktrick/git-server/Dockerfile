# hacktrick/git-server:alpine-3.6

FROM alpine:3.6

MAINTAINER Patrick Hackbarth (patrick.hackbarth@gmx.de)

ENV SCRIPTS_DIR=scripts \
        REPO_DIR=/repos \
        GIT_HOME=/home/git

RUN apk add --no-cache \
        curl \
        gettext \
        git \
        openssh

# add scripts
COPY $SCRIPTS_DIR/create-repo \
    $SCRIPTS_DIR/create-auth \
    $SCRIPTS_DIR/create-hook \
    /usr/bin/
RUN chmod +x \
    /usr/bin/create-repo \
    /usr/bin/create-auth \
    /usr/bin/create-hook

# create user, prepare shh access
RUN adduser -D -s /usr/bin/git-shell git \
    && echo git:disabled | chpasswd \
    && mkdir $GIT_HOME/.ssh \
        $REPO_DIR \
    && chown -R git: $GIT_HOME/ \
        $REPO_DIR \
    && chmod 700 $GIT_HOME/.ssh \
    && ssh-keygen -A

# configure sshd
RUN sed -i \
    -e 's/.*LogLevel.*/LogLevel VERBOSE/' \
    -e 's/#PubkeyAuthentication.*/PubkeyAuthentication yes/' \
    -e 's/#PermitRootLogin.*/PermitRootLogin no/' \
    -e 's/#PasswordAuthentication.*/PasswordAuthentication no/' \
    -e 's/#PrintMotd.*/PrintMotd no/' \
    /etc/ssh/sshd_config

VOLUME ["$REPO_DIR"]

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]
