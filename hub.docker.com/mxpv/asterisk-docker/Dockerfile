FROM centos:centos7
MAINTAINER Maksym Pavlenko <pavlenko.maksym@gmail.com>

ENV USER asterisk

# Full list of versions http://downloads.asterisk.org/pub/telephony/asterisk/
ENV VERSION 14.2.1

# Creates the user under which asterisk will run
RUN groupadd -r $USER                                                   && \
    useradd -r -g $USER $USER                                           && \
    mkdir /var/lib/asterisk                                             && \
    chown $USER:$USER /var/lib/asterisk                                 && \
    usermod --home /var/lib/asterisk $USER

# Get a source code
WORKDIR /tmp
RUN yum -y update                                                       && \
    yum -y install wget                                                 && \
    wget -nv http://downloads.asterisk.org/pub/telephony/asterisk/asterisk-$VERSION.tar.gz && \
    tar -zxvf asterisk-$VERSION.tar.gz

# Build Asterisk
WORKDIR /tmp/asterisk-$VERSION
RUN ./contrib/scripts/install_prereq install                            && \
    ./configure                                                         && \
    make menuselect/menuselect                                          && \
    make menuselect-tree                                                && \
    menuselect/menuselect --disable BUILD_NATIVE menuselect.makeopts    && \
    menuselect/menuselect --enable-category MENUSELECT_CHANNELS menuselect.makeopts && \
    make                                                                && \
    make install                                                        && \
    echo "/usr/local/lib" > /etc/ld.so.conf.d/usr_local.conf            && \
    /sbin/ldconfig

# Change ownership of asterisk folders
RUN chown -R $USER:$USER /var/lib/asterisk                              && \
    chown -R $USER:$USER /var/spool/asterisk                            && \
    chown -R $USER:$USER /var/log/asterisk                              && \
    chown -R $USER:$USER /var/run/asterisk                              && \
    chown -R $USER:$USER /etc/asterisk

# Cleanup
RUN rm -rf /tmp/*                                                       && \
    yum -y clean all

# Expose volumes
VOLUME /var/lib/asterisk
VOLUME /var/log/asterisk
VOLUME /etc/asterisk

WORKDIR /var/lib/asterisk
USER $USER
EXPOSE 5060

# Start asterisk
ENTRYPOINT ["/usr/sbin/asterisk"]
CMD ["-cvvvvv"]