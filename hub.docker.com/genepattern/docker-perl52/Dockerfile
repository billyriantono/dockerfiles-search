# copyright 2017-2018 Regents of the University of California and the Broad Institute. All rights reserved.
FROM perl:5.20

COPY common/container_scripts/runS3OnBatch.sh /usr/local/bin/runS3OnBatch.sh
COPY common/container_scripts/runLocal.sh /usr/local/bin/runLocal.sh

RUN  mkdir /build
COPY Dockerfile /build/Dockerfile
COPY jobdef.json /build/jobdef.json

RUN apt-get update && apt-get upgrade --yes && \
    apt-get install build-essential --yes && \
    apt-get install python-dev --yes && \
    curl -O https://bootstrap.pypa.io/get-pip.py && \
    python get-pip.py 
RUN    pip install awscli 
    
RUN chmod ugo+x /usr/local/bin/runS3OnBatch.sh
 
CMD ["/usr/local/bin/runS3OnBatch.sh" ]

