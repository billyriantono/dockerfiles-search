FROM python:3.7-alpine as base

LABEL maintainer="mmiller@bromberglab.org" \
      description="Filter for sra-toolkit fasterq-dump output"

FROM base as builder

# setup app
COPY . /app

FROM base

COPY --from=builder /app /app

# setup bio-node
LABEL bio-node=v1.0 \
      input="consumable sra_folder,--infolder,required,filename" \
      output_1="fastq_file,--out1,sra_1.fastq" \
      output_2="fastq_file,--out2,sra_2.fastq"

# set environment variables
WORKDIR /app
ENV INPUT_PATH=/input OUTPUT_PATH=/output 

# set app ENTRYPOINT
ENTRYPOINT ["python", "-m", "sra_filter"]

# set app CMD
CMD ["--help"]
