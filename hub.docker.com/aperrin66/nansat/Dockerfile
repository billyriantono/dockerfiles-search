FROM akorosov/nansat_base

LABEL maintainer="Anton Korosov <anton.korosov@nersc.no>"
LABEL purpose="Nansat and other geospatial Python libs"

COPY utilities /tmp/utilities
COPY nansat /tmp/nansat
COPY setup.py /tmp/
WORKDIR /tmp
RUN python setup.py install
