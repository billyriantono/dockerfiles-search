FROM centos:7
MAINTAINER Bryan Dixon <bcdixon@csuchico.edu>

#ADD resolv.conf /etc/resolv.conf

RUN yum -y update

RUN yum install -y openmpi openmpi-devel
RUN yum install -y mpitests-openmpi
RUN yum install -y atlas-devel
RUN yum install -y which



#Add MPI binaries to global system path
RUN echo "export PATH=$PATH:/usr/lib64/openmpi/bin/" >> /etc/profile.d/openmpi.sh
RUN echo "export LD_LIBRARY_PATH=/usr/lib64/openmpi/lib/:$LD_LIBRARY_PATH" >> /etc/profile.d/openmpi.sh
RUN chmod 0755 /etc/profile.d/openmpi.sh

#### ADD DEFAULT USER ####
ARG USER=mpi
ENV USER ${USER}
RUN adduser  ${USER}
RUN echo "${USER}   ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

ENV USER_HOME /home/${USER}
RUN chown -R ${USER}:${USER} ${USER_HOME}

#### CREATE WORKING DIRECTORY FOR USER ####
ARG WORKDIR=/project
ENV WORKDIR ${WORKDIR}
RUN mkdir ${WORKDIR}
RUN chown -R ${USER}:${USER} ${WORKDIR}

ENV MPIR_CVAR_CH3_PORT_RANGE=10000:10100

WORKDIR ${WORKDIR}

# # ------------------------------------------------------------
# # Get Libfabric 1.4.2
# # ------------------------------------------------------------

RUN yum install -y wget
RUN yum install -y make
RUN wget https://github.com/ofiwg/libfabric/releases/download/v1.4.2/libfabric-1.4.2.tar.gz
RUN tar -xvf libfabric-1.4.2.tar.gz
RUN cd libfabric-1.4.2 && ./configure && make && make install

# # ------------------------------------------------------------
# # Set up SSH Server
# # ------------------------------------------------------------

#Install SSH Server
RUN yum -y install openssh-server openssh-clients


# Add host keys
RUN cd /etc/ssh/ && ssh-keygen -A -N ''

# Config SSH Daemon
RUN  sed -i "s/#PasswordAuthentication.*/PasswordAuthentication no/g" /etc/ssh/sshd_config
RUN sed -i "s/#PermitRootLogin.*/PermitRootLogin no/g" /etc/ssh/sshd_config
RUN sed -i "s/#AuthorizedKeysFile/AuthorizedKeysFile/g" /etc/ssh/sshd_config

# Unlock non-password USER to enable SSH login
RUN passwd -fu ${USER}

# Set up user's public and private keys
ENV SSHDIR ${USER_HOME}/.ssh
RUN mkdir -p ${SSHDIR}
RUN mkdir -p ${USER_HOME}/temp
RUN mkdir -p ${USER_HOME}/hosts

# Default ssh config file that skips (yes/no) question when first login to the host
# Now done in the secret volume hopefully
# RUN echo "StrictHostKeyChecking no" > ${USER_HOME}/config


# This file can be overwritten by the following onbuild step if ssh/ directory has config file

RUN chown -R ${USER}:${USER} ${SSHDIR}
RUN chown -R ${USER}:${USER} ${USER_HOME}/temp

# # ------------------------------------------------------------
# # Install Network Utilities
# # ------------------------------------------------------------

RUN yum -y install net-tools


# # ------------------------------------------------------------
# # Utility shell scripts
# # ------------------------------------------------------------

COPY get_hosts /usr/local/bin/get_hosts
RUN chmod +x /usr/local/bin/get_hosts

COPY auto_update_hosts.py /usr/local/bin/auto_update_hosts
RUN chmod +x /usr/local/bin/auto_update_hosts

ADD start.py ${WORKDIR}
RUN chmod +x ${WORKDIR}/start.py

# Switch back to default user
#USER ${USER}

# # ------------------------------------------------------------
# # Install Linpack
# # ------------------------------------------------------------

RUN wget http://www.netlib.org/benchmark/hpl/hpl-2.2.tar.gz
RUN tar -zxvf hpl-2.2.tar.gz
ADD HPL/Make.Linux ${WORKDIR}/hpl-2.2/Make.Linux
ADD HPL/Makefile ${WORKDIR}/hpl-2.2/Makefile
RUN cd hpl-2.2 && make arch=Linux
ADD HPL/HPL.dat ${WORKDIR}/hpl-2.2/testing/ptest/HPL.dat
ADD HPL/HPL.dat ${WORKDIR}/hpl-2.2/bin/Linux/HPL.dat


ENTRYPOINT ./start.py
