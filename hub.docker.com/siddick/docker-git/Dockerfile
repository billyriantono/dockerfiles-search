FROM ubuntu:14.04

RUN apt-get update && \
    apt-get install language-pack-en curl git openssh-server -y && \
    apt-get clean && \
    mkdir /var/run/sshd && \
    adduser --system --group --shell /bin/sh git && \
    adduser git sudo && \
    echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

ENV GITOLITE_COMMIT 2417156

RUN curl https://codeload.github.com/sitaramc/gitolite/tar.gz/$GITOLITE_COMMIT | tar -xzf - && \
    ./gitolite-$GITOLITE_COMMIT/install -ln /usr/local/bin && \
    sed  's/^    ENABLE => \[$/    LOCAL_CODE => "\/scripts\/local\/",\n\0/' ./gitolite-$GITOLITE_COMMIT/src/lib/Gitolite/Rc.pm -i

WORKDIR /home/git
VOLUME /home/git
EXPOSE 22

ADD scripts /scripts

USER git

CMD ["bash", "/scripts/init.sh"]
