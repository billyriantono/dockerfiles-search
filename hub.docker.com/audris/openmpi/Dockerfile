FROM ubuntu

RUN apt-get update && apt-get install -y \
    git \
	wget \
    libxml2-dev \
    python \
    build-essential \
    make \
    gcc \
    python-dev \
    locales \
    python-pip \
	vim \
    sssd \
	openssh-server \
	openssh-client \
	libpam-sss \
	sssd-tools \
	openmpi-bin \
	libopenmpi-dev \
	libboost-all-dev

#RUN dpkg-reconfigure locales && \
#    locale-gen C.UTF-8 && \
#    /usr/sbin/update-locale LANG=C.UTF-8


#RUN wget https://www.open-mpi.org/software/ompi/v1.10/downloads/openmpi-1.10.2.tar.bz2
#RUN bunzip2 < openmpi-1.10.2.tar.bz2 | tar xvf -
#RUN cd openmpi-1.10.2 && ./configure --prefix=/usr/local && make all install
ENV LC_ALL C.UTF-8

#install ldap authentication to use utk's ldap
COPY eecsCA_v3.crt /etc/ssl/
COPY sssd.conf /etc/sssd/
COPY common* /etc/pam.d/
RUN chmod 0600 /etc/sssd/sssd.conf /etc/pam.d/common*
RUN mkdir -p /var/run/sshd 
RUN chmod 0755 /var/run/sshd

COPY init.sh /bin/
