FROM replikation/debian_basic
MAINTAINER Christian Brandt <christian.jena@gmail.com>
ENV URL=http://www.bioinformatics.babraham.ac.uk/projects/fastqc/
ENV ZIP=fastqc_v0.11.8.zip
ENV DST=/fastqc
RUN   apt-get update
RUN   apt-get install -y default-jre
RUN   wget $URL/$ZIP && \
      unzip $ZIP && \
      rm $ZIP && \
      cd FastQC* && \
      chmod 755 fastqc && \
      ln -s /FastQC/fastqc /bin/fastqc
ENTRYPOINT ["fastqc"]
CMD ["--help"]
