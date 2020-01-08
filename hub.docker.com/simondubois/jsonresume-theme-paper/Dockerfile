FROM node

MAINTAINER Simon Dubois <simon@dubandubois.com>

RUN apt-get update \
    && apt-get install -y locales \
    && echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen \
    && echo "fr_FR.UTF-8 UTF-8" >> /etc/locale.gen \
    && echo "sv_SE.UTF-8 UTF-8" >> /etc/locale.gen \
    && locale-gen \
    && /usr/sbin/update-locale LANG=en_US.UTF-8

RUN apt-get install -y bash-completion

RUN apt-get install -y nano

RUN apt-get install -y git

ADD https://raw.githubusercontent.com/jamesob/desk/master/desk /usr/local/bin/desk
RUN chmod a+rx /usr/local/bin/desk

ADD https://raw.githubusercontent.com/jamesob/desk/master/shell_plugins/bash/desk /usr/share/bash-completion/completions/desk
RUN chmod a+r /usr/share/bash-completion/completions/desk

RUN groupmod -g 1001 node \
    && usermod -u 1001 -g 1001 node

RUN groupadd -r -g 1000 docker \
    && useradd -r -u 1000 -g 1000 -d /home/docker -s /bin/bash docker \
    && mkdir /home/docker \
    && chmod 755 /home/docker \
    && chown 1000:1000 /home/docker

ADD https://raw.githubusercontent.com/git/git/master/contrib/completion/git-prompt.sh /home/docker/.bash_gitprompt
RUN chmod a+r /home/docker/.bash_gitprompt
