FROM centos:7
# derived from https://bitbucket.org/deardooley/agave-docker.git on 20/05/2019

# Install deps
RUN yum update -y && \
    yum install -y --setopt=tsflags=nodocs --setopt=override_install_langs=en_US.utf8 \
    make \
    openssl-devel \
    libxml2-devel \
    libarchive-devel \
    boost-devel \
    gcc \
    gcc-c++ \
    git \
    libtool \
    java-1.8.0-openjdk-headless \
    which \
    wget && \
    yum clean all -y

WORKDIR /usr/local

# Install torque
RUN git clone https://github.com/adaptivecomputing/torque.git -b 5.0.0 torque

WORKDIR /usr/local/torque
RUN ./autogen.sh && \
    ./configure && \
    make && \
    make install && \
    cp contrib/init.d/trqauthd /etc/init.d/ && \
    cp contrib/init.d/pbs_mom /etc/init.d/pbs_mom && \
    cp contrib/init.d/pbs_server /etc/init.d/pbs_server && \
    cp contrib/init.d/pbs_sched /etc/init.d/pbs_sched && \
    ldconfig && \
    echo "localhost" > /var/spool/torque/server_name && \
    echo '/usr/local/lib' > /etc/ld.so.conf.d/torque.conf && \
    ldconfig

ENV HOSTNAME localhost

RUN cat /etc/hosts
COPY torque.setup /usr/local/torque/torque.setup
RUN trqauthd start && \
    ./torque.setup root localhost && \
    pbs_mom && pbs_sched && \
    qmgr -c "create queue debug queue_type=execution" && \
    qmgr -c "set queue debug enabled=true" && \
    qmgr -c "set queue debug started=true" && \
    qmgr -c "set server scheduling=True" && \
    qmgr -c 'set queue batch resources_default.walltime = 48:00:00' && \
    qmgr -c 'set queue batch resources_default.nodes = 1' && \
    qmgr -c 'set server default_queue = debug' && \
    echo "localhost np=1" >> /var/spool/torque/server_priv/nodes && \
    echo "docker np=1" >> /var/spool/torque/server_priv/nodes && \
    printf "\$pbsserver localhost" >> /var/spool/torque/mom_priv/config

COPY supervisord.conf /etc/supervisord.conf
RUN mkdir /var/log/supervisor && \
    chmod -R 777 /var/log/supervisor

# install Singularity
WORKDIR /opt/singularity
RUN VERSION=2.6.0 && \
    wget https://github.com/sylabs/singularity/releases/download/$VERSION/singularity-$VERSION.tar.gz && \
    tar xvf singularity-$VERSION.tar.gz && \
    cd singularity-$VERSION && \
    ./configure --prefix=/usr/local && \
    make && make install

# install Nextflow
WORKDIR /opt/nextflow
RUN VERSION=19.04.1 && \
    wget https://github.com/nextflow-io/nextflow/releases/download/v19.04.1/nextflow-$VERSION-all && \
    chmod +x nextflow-$VERSION-all && \
    ln -s /opt/nextflow/nextflow-$VERSION-all /usr/local/bin/nextflow

# Add entrypoint script to set the current hostname so the scheduler can communicat
COPY docker_entrypoint.sh /docker_entrypoint.sh

ENTRYPOINT [ "/docker_entrypoint.sh" ]
EXPOSE 10389 22 9618
CMD ["/usr/bin/supervisord"]
