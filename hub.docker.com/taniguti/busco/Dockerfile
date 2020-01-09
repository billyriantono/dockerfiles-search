FROM kastman/busco-docker:3.0.0 

WORKDIR /workspace

RUN wget https://busco.ezlab.org/datasets/fungi_odb9.tar.gz \
    && tar -xf fungi_odb9.tar.gz \
    && rm fungi_odb9.tar.gz 


RUN wget https://busco.ezlab.org/datasets/basidiomycota_odb9.tar.gz \
    && tar -xf basidiomycota_odb9.tar.gz \
    && rm basidiomycota_odb9.tar.gz

ENV PATH $PATH:/software/applications/augustus/3.2.2/bin/:/software/applications/bamtools/v2.4.0/bin/:/software/applications/hmmer-3.1b2-linux-intel-x86_64/binaries/
ENV AUGUSTUS_CONFIG_PATH /software/applications/augustus/3.2.2/bin/augustus
