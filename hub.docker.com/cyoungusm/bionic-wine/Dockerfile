FROM cyoungusm/bionic-wine:0.6

USER wine
ADD dotcache.tar.gz .
ADD dotwine.tar.gz .
COPY --chown=wine:wine .windows-serial .windows-serial
