FROM google/debian:wheezy

MAINTAINER Brian W Bush <root@bwbush.io>

WORKDIR /root/tmp

RUN apt-get update                                \
 && apt-get install --no-install-recommends --yes \
      apt-utils                                   \
      aptitude                                    \
      atop                                        \
      attr                                        \
      bc                                          \
      bvi                                         \
      bzip2                                       \
      cabextract                                  \
      csh                                         \
      curl                                        \
      cvs                                         \
      dc                                          \
      diffstat                                    \
      dos2unix                                    \
      gawk                                        \
      git                                         \
      gnupg                                       \
      gnupg-agent                                 \
      locales                                     \
      lsof                                        \
      man-db                                      \
      md5deep                                     \
      mercurial                                   \
      mscompress                                  \
      openssh-client                              \
      openssh-server                              \
      par2                                        \
      pbzip2                                      \
      procps                                      \
      psmisc                                      \
      pv                                          \
      pwgen                                       \
      rsync                                       \
      screen                                      \
      ssh                                         \
      subversion                                  \
      sudo                                        \
      tcsh                                        \
      time                                        \
      tmux                                        \
      tofrodos                                    \
      unzip                                       \
      vim                                         \
      wget                                        \
      wput                                        \
      zip                                         \
 && apt-get clean autoclean                       \
 && apt-get autoremove --yes

ENV NOTVISIBLE "in users profile"

RUN export                                                                                             \
      RPASS=the-password                                                                               \
 && mkdir /var/run/sshd                                                                                \
 && echo "root:$RPASS" | chpasswd                                                                      \
 && sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config              \
 && sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd \
 && echo "export VISIBLE=now" >> /etc/profile

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]

RUN chsh -s /bin/bash                                  \
 && localedef -v -c -i en_US -f UTF-8 en_US.UTF-8 || :

RUN export                                                        \
      NUSER=1999                                                  \
      TUSER=the-user                                              \
      TPASS=the-password                                          \
      NGRP=1999                                                   \
      TGRP=the-group                                              \
 && groupadd -g $NGRP $TGRP                                       \
 && useradd -g $NGRP -u $NUSER -G ssh,sudo -m -s /bin/bash $TUSER \
 && echo "$TUSER:$TPASS" | chpasswd                               \
 && echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

VOLUME /data
