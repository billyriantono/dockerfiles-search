FROM ubuntu:18.04 as base

LABEL bio_node=v1.0 \
      bionode_entrypoint=/app/bionode.sh \
      input_1="fastq_file|fastq_gz" \
      input_2="fastq_file|fastq_gz" \
      output_1="fasta_file" \
      output_2="fasta_file" \
      maintainer=mmiller@bromberglab.org \
      description="An ultra-fast all-in-one FASTQ preprocessor (QC/adapters/trimming/filtering/splitting/merging...)"

FROM base as builder

# setup app
COPY . /app

# setup system
RUN apt-get update -y && apt-get install -y \
    build-essential \
    #libnss-sss \
    curl \
    wget \
    zlib1g-dev \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

WORKDIR /tmp
RUN LATEST=$(basename $(curl -Ls -o /dev/null -w %{url_effective} https://github.com/OpenGene/fastp/releases/latest/download/) | cut -c 2-) && \
    echo ${LATEST} > /app/version && \
    wget -q https://github.com/OpenGene/fastp/archive/v${LATEST}.tar.gz && \
    tar xzf v${LATEST}.tar.gz && \
    cd fastp-${LATEST} && \
    mkdir -p /install/bin && PREFIX=/install make && PREFIX=/install make install

FROM base

COPY --from=builder /install /usr/local
COPY --from=builder /app /app

# set environment variables
WORKDIR /app
ENV INPUT_PATH=/input OUTPUT_PATH=/output

ENTRYPOINT ["fastp"]

# set project CMD
# CMD []
