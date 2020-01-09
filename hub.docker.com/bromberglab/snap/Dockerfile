FROM bromberglab/predictprotein

LABEL LABEL bio_node=v1.0 \
      bionode_entrypoint=/app/bionode.sh \
      input_1="fasta_file" \
      input_2="mutation_list" \
      input_2="snap_output" \
      maintainer=mmiller@bromberglab.org

# setup system
ENV DEBIAN_FRONTEND="noninteractive"
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9 && \
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 228FE7B0D6EBED94 && \
    add-apt-repository -y 'deb [arch=amd64,i386] https://cran.rstudio.com/bin/linux/ubuntu xenial/' && \
    apt-add-repository -y 'deb http://rostlab.org/debian/ stable main contrib non-free' && \
    apt-get update && \
    apt-get -y --allow-unauthenticated install rostlab-debian-keyring && \
    apt-get update --fix-missing

# setup app
RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections && \
    echo snapfun shared/snapfun/nonprofit_org boolean true | debconf-set-selections && \
    apt-get -y install snapfun && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

COPY . /app

# copy SNAP default configuration
COPY snapfunrc.default /usr/share/snapfun/snapfunrc.default

# set environment variables
WORKDIR /input
ENV INPUT_PATH=/input OUTPUT_PATH=/output

# set project ENTRYPOINT
ENTRYPOINT ["snapfun", "-o", "/output/snap.out"]

# set project CMD
CMD ["--help"]
