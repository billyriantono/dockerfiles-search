FROM babim/alpinebase

ENV UID=787 UNAME=plexpy GID=787 GNAME=plexpy

RUN addgroup -g $GID $GNAME \
 && adduser -SH -u $UID -G $GNAME -s /usr/sbin/nologin $UNAME \
 && apk add --no-cache git python \
 && mkdir /plexpy && chown $UID:$GID /plexpy

USER $UNAME

RUN git clone https://github.com/drzoidberg33/plexpy.git /plexpy

VOLUME /config

EXPOSE 8181

WORKDIR /plexpy

CMD ["/usr/bin/python", "PlexPy.py", "--datadir=/config"]
