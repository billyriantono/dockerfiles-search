FROM alpine
#
# Include dist
ADD dist/ /root/dist/
#
# Get and install dependencies & packages
RUN apk -U add \
                       bash \
                       build-base \
                       git \
                       gmp-dev \
                       libcap \
                       libffi-dev \
                       mpc1-dev \
                       mpfr-dev \
                       openssl \
                       openssl-dev \
                       python3 \
                       python3-dev \
                       py3-bcrypt \
		       py3-mysqlclient \
                       py3-requests \
                       py3-setuptools && \
#
# Setup user
    addgroup -g 2000 cowrie && \
    adduser -S -s /bin/ash -u 2000 -D -g 2000 cowrie && \
#
# Install cowrie
    mkdir -p /home/cowrie && \
    cd /home/cowrie && \
    git clone --depth=1 https://github.com/micheloosterhof/cowrie -b v2.0.0 && \
    cd cowrie && \
    mkdir -p log && \
    pip3 install --upgrade pip && \
    pip3 install --upgrade -r requirements.txt && \
#
# Setup configs
    setcap cap_net_bind_service=+ep /usr/bin/python3.7 && \
    cp /root/dist/cowrie.cfg /home/cowrie/cowrie/cowrie.cfg && \
    chown cowrie:cowrie -R /home/cowrie/* /usr/lib/python3.7/site-packages/twisted/plugins && \
#
# Start Cowrie once to prevent dropin.cache errors upon container start caused by read-only filesystem
    su - cowrie -c "export PYTHONPATH=/home/cowrie/cowrie:/home/cowrie/cowrie/src && \
                    cd /home/cowrie/cowrie && \
                    /usr/bin/twistd --uid=2000 --gid=2000 -y cowrie.tac --pidfile cowrie.pid cowrie &" && \
    sleep 10 && \
#
# Clean up
    apk del --purge build-base \
                    git \
                    gmp-dev \
                    libcap \
                    libffi-dev \
                    mpc1-dev \
                    mpfr-dev \
                    openssl-dev \
                    python3-dev \
                    py3-mysqlclient && \
    rm -rf /root/* /tmp/* && \
    rm -rf /var/cache/apk/* && \
    rm -rf /home/cowrie/cowrie/cowrie.pid
#
# Start cowrie
ENV PYTHONPATH /home/cowrie/cowrie:/home/cowrie/cowrie/src
WORKDIR /home/cowrie/cowrie
USER cowrie:cowrie
CMD ["/usr/bin/twistd", "--nodaemon", "-y", "cowrie.tac", "--pidfile", "/tmp/cowrie/cowrie.pid", "cowrie"]
