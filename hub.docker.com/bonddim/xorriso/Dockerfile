FROM ubuntu:latest

RUN apt-get update && apt-get install -y --no-install-recommends \
        genisoimage \
        isolinux    \
        rsync       \
        xorriso     \
    && rm -rf /var/lib/apt/lists/*

CMD ["/bin/bash"]
