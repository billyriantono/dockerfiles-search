from ubuntu:disco

ENV DOWNLOAD_URL http://mirrors.syringanetworks.net/eclipse/technology/epp/downloads/release/2018-12/R/eclipse-cpp-2018-12-R-linux-gtk-x86_64.tar.gz
ENV eclipse_SHA512 a7fff7774d7d95a5469de07d5bb59e3bc272136cdd6226c04aa8c24a56dabde9de0bcbe050d25d9b91acca238e9387171c216d84633d090cf1487ef3ec645f5c
ENV INSTALLATION_DIR /usr/local

RUN DEBIAN_FRONTEND=noninteractive apt-get -yqq update \
 && DEBIAN_FRONTEND=noninteractive apt-get -yqq install openssh-server xorg libgtk2.0-0 default-jre \
    build-essential scons valgrind cmake gcc-multilib ccache quilt libncurses5-dev zlib1g-dev \
    sudo vim curl wget unzip python python-pip gawk flex gettext locales \
    subversion git-core \
 && mkdir /var/run/sshd \
 && useradd -m eclipse -s /bin/bash -u 1001 \
 && echo 'eclipse ALL=NOPASSWD: ALL' > /etc/sudoers.d/eclipse \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN locale-gen en_US.UTF-8
ENV LANG='en_US.UTF-8' LANGUAGE='en_US:en' LC_ALL='en_US.UTF-8'

RUN echo "X11UseLocalhost no" >> /etc/ssh/sshd_config 
RUN curl -s -L "$DOWNLOAD_URL" | tar xz -C $INSTALLATION_DIR/ \
 && ln -s $INSTALLATION_DIR/eclipse/eclipse /usr/bin/ 

RUN chown -R eclipse:eclipse $INSTALLATION_DIR/eclipse &&\
  chmod -R 775 $INSTALLATION_DIR/eclipse
CMD ["/usr/sbin/sshd", "-D"]
