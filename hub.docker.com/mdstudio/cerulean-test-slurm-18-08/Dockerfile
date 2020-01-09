FROM mdstudio/cerulean-test-base:latest

USER root

# Install munge (needed by slurm)
RUN apt-get update && \
    apt-get install -y --no-install-recommends munge libmunge2 && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*
RUN chmod 0700 /etc/munge /var/log/munge && \
chmod 0711 /var/lib/munge && \
mkdir /var/run/munge && \
chmod 0755 /var/run/munge && \
chmod 0400 /etc/munge/munge.key

RUN chown -R munge:munge /etc/munge /var/lib/munge /var/log/munge /var/run/munge


# Install slurm
RUN groupadd --system slurm && useradd --system --gid slurm --create-home slurm
RUN echo slurm:slurm | chpasswd

RUN mkdir -p /var/spool/slurmctld/state
RUN chown -R slurm:slurm /var/spool/slurmctld

RUN mkdir -p /usr/local/etc/slurm

RUN mkdir -p /var/log/slurm
RUN chown -R slurm:slurm /var/log/slurm

COPY slurm.cert /usr/local/etc/slurm/slurm.cert
COPY slurm.key /usr/local/etc/slurm/slurm.key
RUN chmod 600 /usr/local/etc/slurm/slurm.key

COPY install_slurm.sh /usr/local/bin/
COPY slurm_timeout.diff /usr/local/etc/
WORKDIR /usr/local
RUN apt-get update && \
    apt-get --no-install-recommends install -y gcc make libssl-dev libmunge-dev tar wget patch && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN /bin/bash /usr/local/bin/install_slurm.sh slurm-18-08-4-1.tar.gz

COPY slurm.conf /usr/local/etc/slurm/slurm.conf

# Add start-up scripts
COPY start-services.sh /etc/start-services.sh
RUN chmod +x /etc/start-services.sh
CMD /etc/start-services.sh
