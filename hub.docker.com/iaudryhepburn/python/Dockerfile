FROM iaudryhepburn/base

# ADD https://raw.githubusercontent.com/ihepburn/saltstack_os/master/files/sources.list /etc/apt/sources.list

RUN git clone --depth 1 https://github.com/ihepburn/saltstack_os.git $saltdir
RUN apt-get -y update && \
    salt-call --file-root=$saltdir --local --pillar-root=$saltdir/pillar state.highstate
RUN rm -rf $saltdir

RUN apt-get autoclean && \
    apt-get autoremove && \
    rm -rf /var/lib/apt/lists/*
