FROM fluendo/docker-buildbot-xenial-x86_64

MAINTAINER fluendo

# Install required packages
RUN apt-get install -y \
        sqlite3 \
        postgresql-common libpq-dev \
        gettext \
        python-svn && ln -sf /usr/lib/python2.7/dist-packages/pysvn/_pysvn_2_7.x86_64-linux-gnu.so /usr/lib/python2.7/dist-packages/pysvn/_pysvn_2_7.so

CMD ["./run.sh"]
