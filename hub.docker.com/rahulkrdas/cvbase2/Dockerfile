FROM conda/miniconda2

RUN apt-get update && \
    /usr/local/bin/conda install opencv -y

RUN apt-get update && \
    apt-get install -y build-essential && \
    pip install cmake
