FROM gentoo/stage3-amd64
MAINTAINER Kyle Sferrazza <kyle.sferrazza@gmail.com>

RUN emerge --sync

RUN echo -e "en_US.UTF-8 UTF-8\nen_US ISO-8859-1" >> /etc/locale.gen
RUN locale-gen
RUN eselect locale set en_US.utf8

RUN emerge dev-vcs/git app-editors/vim app-admin/sudo

RUN echo '%wheel ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers

RUN useradd -m -g wheel kyle
RUN echo -e "kyle\nkyle" | passwd kyle

RUN su kyle -c "git clone https://github.com/kylesferrazza/dot.git /home/kyle/dot"

USER kyle
WORKDIR /home/kyle
CMD /bin/bash
