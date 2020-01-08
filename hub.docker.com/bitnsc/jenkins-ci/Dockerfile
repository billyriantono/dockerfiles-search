FROM jenkins
MAINTAINER liling@bit.edu.cn

USER root

# Setup timezone
RUN echo Asia/Shanghai > /etc/timezone && dpkg-reconfigure --frontend noninteractive tzdata

# Setup locale
ENV LC_ALL C.UTF-8

# Change mirror
# RUN sed -i -e 's/httpredir.debian.org/mirror.bit.edu.cn/' -e 's/security.debian.org/mirror.bit.edu.cn\/debian-security/' /etc/apt/sources.list

# Install jdk 7 and python
RUN apt-get update; apt-get install -y openjdk-7-jdk python python-dev python-pip rsync

# Install VIM
RUN apt-get install -y vim

# Install sphinx
RUN pip install sphinx sphinx_rtd_theme

# Install TexLive and Fonts
RUN apt-get install -y texlive-lang-cjk texlive-xetex fontconfig
RUN cd /usr/share/fonts/truetype; \
    wget https://github.com/royguo/jianliku/raw/master/conf/fonts/simsun.ttf; \
    wget https://github.com/royguo/jianliku/raw/master/conf/fonts/simhei.ttf; \
    wget https://cs.fit.edu/code/projects/ndworld/repository/revisions/13/raw/Resources/Fonts/simfang.ttf; \
    wget https://cs.fit.edu/code/projects/ndworld/repository/revisions/13/raw/Resources/Fonts/simkai.ttf; \
    fc-cache -fsv
RUN rm /usr/share/texlive/texmf-dist/tex/latex/ctex/fontset/ctex-xecjk-winfonts.def
ADD ctex-xecjk-winfonts.def /usr/share/texlive/texmf-dist/tex/latex/ctex/fontset/ctex-xecjk-winfonts.def
RUN mktexlsr

# Install rancher compose
RUN wget -O - https://github.com/rancher/rancher-compose/releases/download/v0.12.0/rancher-compose-linux-amd64-v0.12.0.tar.gz | tar zxf - ; \
    mv rancher-compose*/* /usr/local/bin ; \
    chmod +x /usr/local/bin/rancher-compose ; \
    rm -rf rancher-compose*

# Add group docker
RUN groupadd -g 602 deploy ; adduser jenkins deploy

USER jenkins
