FROM julia:0.5.2

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    git cmake zlib1g libhdf5-dev build-essential wget unzip && \
    rm -rf /var/lib/apt/lists/*

RUN julia -e 'Pkg.clone("Bio"); using Bio'

ENTRYPOINT ["julia"]
