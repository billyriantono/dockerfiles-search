FROM centos:7

LABEL maintainer="oatkrittin@gmail.com"

COPY init_nbt_nxf /root/

ENV LMOD_VERSION=8.0

# Install dependencies
RUN yum -y update && \
    yum -y install epel-release && \
    yum -y install \
      which \
      wget \
      bzip2 \
      gcc \
      make \
      rsync \
      tcl \
      tcl-devel \
      libreadline-dev \
      readline-devel \
      lua \
      lua-devel \
      lua-posix \
      python-setuptools \
      fish \
      perl \
      unzip \
      jq && \
      yum clean all && \
      rm -rf /var/cache/yum/*

# Install Minio Client(mc)
RUN mkdir -p /usr/local/bin && \
  wget https://dl.min.io/client/mc/release/linux-amd64/mc && \
  chmod +x mc && \
  mv ./mc /usr/local/bin/.

# Install Lmod
RUN cd ~ && \
   wget https://jaist.dl.sourceforge.net/project/lmod/Lmod-${LMOD_VERSION}.tar.bz2 && \
   tar -xjvf Lmod-${LMOD_VERSION}.tar.bz2 && \
   cd Lmod-${LMOD_VERSION} && \
   ./configure --prefix=/opt/apps && \
   make && \
   make install && \
   ln -s /opt/apps/lmod/lmod/init/profile /etc/profile.d/z00_lmod.sh && \
   ln -s /opt/apps/lmod/lmod/init/cshrc /etc/profile.d/z00_lmod.csh && \
   rm -f ~/Lmod-${LMOD_VERSION}.tar.bz2

# Initiallization
RUN chmod u+x /root/init_nbt_nxf && \
  printf "\nsource /root/init_nbt_nxf\n" >> ~/.bashrc