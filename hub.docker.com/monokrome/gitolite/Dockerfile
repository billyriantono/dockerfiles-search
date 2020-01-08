FROM monokrome/sshd
MAINTAINER Brandon R. Stoner <monokrome@monokro.me>

RUN useradd -m -s /bin/bash git

ADD . /home/git/gitolite

RUN apt-get install -y git-core && mkdir /home/git/bin
RUN chmod +x /home/git/gitolite/install && chmod +x /home/git/gitolite/src/gitolite*
RUN /home/git/gitolite/install -to /home/git/bin
RUN chown -R git:git /home/git
