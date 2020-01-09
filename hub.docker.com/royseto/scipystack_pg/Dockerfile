FROM ipython/scipystack

MAINTAINER roy.seto@gmail.com

COPY build_postgis.sh /tmp/
RUN /tmp/build_postgis.sh && /bin/rm -f /tmp/build_postgis.sh

RUN LD_LIBRARY_PATH=/usr/local/pgsql/lib \
    PATH=/usr/local/pgsql/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin \
    pip2 install csvkit GeoAlchemy2 ipython-sql psycopg2 sqlalchemy
