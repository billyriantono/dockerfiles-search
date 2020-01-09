FROM ubuntu:18.04 as base
COPY --from=bromberglab/bio-node /bio-node /bio-node

LABEL maintainer=mmiller@bromberglab.org \
      description="NCBI sra-toolkit optimization for faster and more reliable (batch) downloads of SRA read files"

# bio-node
LABEL bio-node=v1.0 \
      input_1="sra_id,,optional,content" \
      input_2="sra_ids,--sralist,optional,filename" \
      output="sra_folder,--outdir," \
      parameters="--split-files"

# setup system
RUN apt-get update && apt-get install -y \
    wget \
    curl \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

FROM base as builder

ARG SRA_TOOLKIT_RELEASE=current
ARG ASPERA_CONNECT_RELEASE=3.9.8
ARG ASPERA_CONNECT_BUILD=176272

# setup app
COPY . /app

RUN useradd -ms /bin/bash builder && \
    mkdir /install && chmod 777 /install && \
    chown -R builder:builder /app

USER builder

WORKDIR /tmp
RUN mkdir /install/bin && \
    mkdir /install/share && \
    wget -q --output-document src1.tar.gz https://ftp-trace.ncbi.nlm.nih.gov/sra/sdk/${SRA_TOOLKIT_RELEASE}/sratoolkit.${SRA_TOOLKIT_RELEASE}-ubuntu64.tar.gz && \
    tar -xzf src1.tar.gz && \
    SRA=$(ls | grep sratoolkit) && \
    cp -r $SRA/bin/* /install/bin && \
    wget -q --output-document src2.tar.gz https://download.asperasoft.com/download/sw/connect/${ASPERA_CONNECT_RELEASE}/ibm-aspera-connect-${ASPERA_CONNECT_RELEASE}.${ASPERA_CONNECT_BUILD}-linux-g2.12-64.tar.gz && \
    tar -xzf src2.tar.gz && \
    ASPERA=$(ls | grep ibm-aspera-connect) && \
    bash $ASPERA > /dev/null && \
    mv ~/.aspera /install/share/aspera && \
    mv /app/default.kfg /install/bin/ncbi/default.kfg

FROM base

COPY --from=builder /install /usr/local
COPY --from=builder /app /app

# set environment variables
WORKDIR /app
ENV SRA_TMP_DIR=/tmp INPUT_PATH=/input OUTPUT_PATH=/output

# set project ENTRYPOINT
ENTRYPOINT ["bash", "/app/evenfasterq-dump.sh"]

# set project CMD
CMD ["--help"]
