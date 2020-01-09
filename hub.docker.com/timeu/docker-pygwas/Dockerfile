# Dockerfile for PyGWAS
# Version 0.1

FROM timeu/docker-gwas-base 
MAINTAINER Uemit Seren <uemit.seren@gmail.com>

VOLUME ['/DATA']

WORKDIR /app

RUN /env/bin/pip install PyGWAS>=1.1.2 

CMD ["-h"]

ENTRYPOINT ["/env/bin/pygwas"]

