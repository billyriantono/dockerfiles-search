FROM ubuntu:18.04

MAINTAINER Shatavia Morrison <smorrison@cdc.gov>

RUN apt-get update && apt-get install -y ncbi-blast+=2.6.0-1 \
        python

COPY /ureaplasmaMacrolide_v1/scripts/* /scripts/
COPY /ureaplasmaMacrolide_v1/primerSeqs/* /primerSeqs/

ENTRYPOINT ["python","/scripts/insilicoBlast_PCR.py"]
