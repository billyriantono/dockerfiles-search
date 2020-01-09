FROM python:alpine3.10 as base

LABEL maintainer="Denis O'Meally (domeally@coh.org)" \
      version="1.2"

FROM base as builder
COPY ./PLEK.1.2.tar.gz / 
RUN tar zxf PLEK.1.2.tar.gz
RUN cd PLEK.1.2
CMD ['PLEK_setup.py']
FROM base
COPY --from=builder /PLEK.1.2 /usr/local/bin
RUN apk --no-cache add procps bash
RUN chmod a+x /usr/local/bin/PLEK*

