FROM ubuntu:18.04

# Install all the Linux packages required for Yocto builds. Note that the packages python3,
# tar, locales and cpio are not listed in the official Yocto documentation. The build, however,
# without them.
RUN apt-get update && apt-get -y install gawk wget git-core diffstat unzip texinfo gcc-multilib \
     build-essential chrpath socat cpio python python3 python3-pip python3-pexpect \
     python3-testtools python3-subunit \
     xz-utils debianutils iputils-ping libsdl1.2-dev xterm tar locales vim python3-pip virtualenv enchant npm supervisor iproute2 wine-stable && apt-get clean && \
     rm -rf /var/lib/apt/lists/*

RUN pip3 install buildbot buildbot-www buildbot-waterfall-view buildbot-console-view buildbot-grid-view buildbot-worker
# By default, Ubuntu uses dash as an alias for sh. Dash does not support the source command
# needed for setting up the build environment in CMD. Use bash as an alias for sh.
RUN rm /bin/sh && ln -s bash /bin/sh && mkdir -p /var/log/supervisor && \
  mkdir -p /etc/supervisor/conf.d
# Set the locale to en_US.UTF-8, because the Yocto build fails without any locale set.
RUN locale-gen en_US.UTF-8 && update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LC_ALL en_US.UTF-8

ENV USER_NAME autobuilder
ENV PROJECT ds-os

# The running container writes all the build artefacts to a host directory (outside the container).
# The container can only write files to host directories, if it uses the same user ID and
# group ID owning the host directories. The host_uid and group_uid are passed to the docker build
# command with the --build-arg option. By default, they are both 1001. The docker image creates
# a group with host_gid and a user with host_uid and adds the user to the group. The symbolic
# name of the group and user is cuteradio.
ARG host_uid=1001
ARG host_gid=1001
RUN groupadd -g $host_gid $USER_NAME && useradd -g $host_gid -m -s /bin/bash -u $host_uid $USER_NAME

# Perform the Yocto build as user cuteradio (not as root).
# NOTE: The USER command does not set the environment variable HOME.

# By default, docker runs as root. However, Yocto builds should not be run as root, but as a 
# normal user. Hence, we switch to the newly created user cuteradio.
USER $USER_NAME

# Create the directory structure for the Yocto build in the container. The lowest two directory
# levels must be the same as on the host.
ENV BUILD_INPUT_DIR /home/$USER_NAME/yocto/input
ENV BUILD_OUTPUT_DIR /home/$USER_NAME/yocto/output
RUN mkdir -p $BUILD_INPUT_DIR $BUILD_OUTPUT_DIR
RUN mkdir -p /home/${USER_NAME}/.ssh

# Clone the repositories of the meta layers into the directory $BUILD_INPUT_DIR/sources/cuteradio.
WORKDIR $BUILD_INPUT_DIR
RUN ssh-keyscan -t rsa bitbucket.org > /home/${USER_NAME}/.ssh/known_hosts
#RUN true
#RUN git clone --recurse-submodules ssh://git@bitbucket.org/deepseaiot/$PROJECT.git

#USER $USER_NAME
RUN mkdir -p /home/${USER_NAME}/pokybuild3
WORKDIR /home/${USER_NAME}/pokybuild3
RUN buildbot create-master -r yocto-controller
RUN cd yocto-controller && git clone https://git.yoctoproject.org/git/yocto-autobuilder2 yoctoabb \ 
     && ln -rs yoctoabb/master.cfg master.cfg 

RUN buildbot-worker create-worker -r --umask=0o22 yocto-worker localhost ubuntu1804-ty-1 pass
RUN mkdir -p /home/${USER_NAME}/pokybuild3/git/trash

#COPY buildbot.tac /home/${USER_NAME}/pokybuild3/yocto-worker/
USER root
RUN cd /root && git clone https://git.yoctoproject.org/git/yocto-autobuilder-helper
#RUN cd /root && git clone git@bitbucket.org:deepseaiot/yocto-autobuilder-helper.git 
RUN mkdir -p /srv/autobuilder/autobuilder.deepseaai.ddns.net
RUN mkdir -p /srv/autobuilder/downloads.deepseaai.ddns.net
RUN mkdir -p /srv/www/vhosts
RUN chown -R ${USER_NAME} /srv/www/vhosts
RUN chown -R ${USER_NAME} /srv/autobuilder
RUN chown -R ${USER_NAME} /home/${USER_NAME}/pokybuild3

VOLUME /srv/autobuilder/autobuilder.deepseaai.ddns.net
VOLUME /srv/autobuilder/downloads.deepseaai.ddns.net
VOLUME /srv/www/vhosts
VOLUME /home/autobuilder/pokybuild3/git

COPY supervisor.conf /etc/supervisor.conf
USER ${USER_NAME}
COPY master.cfg /home/${USER_NAME}/pokybuild3/yocto-controller/yoctoabb/
COPY config.py /home/${USER_NAME}/pokybuild3/yocto-controller/yoctoabb/
USER root
COPY config.json /root/yocto-autobuilder-helper/
RUN chmod a+rx /root
CMD ["supervisord", "-c", "/etc/supervisor.conf"]
# Prepare Yocto's build environment. If TEMPLATECONF is set, the script oe-init-build-env will
# install the customised files bblayers.conf and local.conf. This script initialises the Yocto
# build environment. The bitbake command builds the rootfs for our embedded device.
#WORKDIR $BUILD_OUTPUT_DIR
#ENV TEMPLATECONF=$BUILD_INPUT_DIR/$PROJECT/sources/meta-ds/conf
#CMD source $BUILD_INPUT_DIR/$PROJECT/sources/poky/oe-init-build-env build \
#    && bitbake core-image-base-ds
#COPY dskey /home/${USER_NAME}/.ssh/id_rsa
#USER root
#RUN chown ${USER_NAME} /home/${USER_NAME}/.ssh/id_rsa
#USER $USER_NAME
EXPOSE 8010
EXPOSE 9989



