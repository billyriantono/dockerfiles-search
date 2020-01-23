FROM ubuntu
LABEL author="Patrik Williams <patrik@patrikwilliams.com>"

ADD  ixia8.4.tar.gz /

# Set the env variable DEBIAN_FRONTEND to noninteractive to get
# apt-get working without error output.
# AND
# Make sure code put into the special tcl volume can lazily be filled
# with packages
ENV DEBIAN_FRONTEND=noninteractive \
    TCL8_6_TM_PATH="/git/TclLib/.make.install" \
    TCLLIBPATH="/git/TclLib/.make.install/TclLibPath ./lib" \
    WORKDIR="/opt/data"

# Update underlying ubuntu image and all necessary packages.
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y \
            itcl3 \
            xotcl \
            tdom \
            tcl-expect \
            tcl-memchan \
            tcl-tclreadline \
            tcl-thread \
            tcl-tls \
            tcl-trf \
            tcl-udp \
            tcl-vfs \
            tcl8.6 \
            tcllib \
            tclxml \
            tclodbc \
            tclx8.4 \
            net-tools \
            iproute2 \
            openssh-client \
            && \
    apt-get clean && rm -rf /var/lib/apt/lists/*
            #tcl8.6-doc \
            #itcl3-doc \
            #tcl-trf-doc \
            #tcl8.6-dev \
            #tcl8.6-doc \
            #tclx8.4-doc \

# Export two volumes, one for tcl code and one for data, just in case.
VOLUME ["/git","/opt/data"]

# Arrange for a decent tclreadline prompt in interactive mode
COPY tclshrc /root/.tclshrc
COPY bashrc /root/.bashrc
COPY entrypoint.sh /usr/local/bin/entrypoint.sh

WORKDIR ["/opt/data"]

# located in /usr/bin/tclsh8.6
ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]
