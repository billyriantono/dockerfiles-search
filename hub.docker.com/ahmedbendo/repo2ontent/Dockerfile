FROM ruby:2.6.1

ARG freetds_version=1.00.110

RUN apt-get update -qq && apt-get install -y --no-install-recommends build-essential libc6-dev wget
RUN wget http://www.freetds.org/files/stable/freetds-${freetds_version}.tar.gz && \
    tar -xzf freetds-${freetds_version}.tar.gz && \
    cd freetds-${freetds_version} && \
    ./configure --prefix=/usr/local --with-tdsver=7.3 && \
    make && \
    make install

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# https://github.com/moby/moby/issues/2259
# https://nickjanetakis.com/blog/docker-tip-56-volume-mounting-ssh-keys-into-a-docker-container
COPY entrypoint.sh /bin/entrypoint.sh
RUN chmod +x /bin/entrypoint.sh
ENTRYPOINT ["/bin/entrypoint.sh"]
