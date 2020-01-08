FROM debian:9-slim

ENV LANG=C.UTF-8 LC_ALL=C.UTF-8
ENV PATH=/opt/miniconda3/bin:$PATH

RUN apt update && apt install -y wget \
   bzip2 \
   && apt clean all \
   && rm -rf /var/lib/apt/lists/* \
   && wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh \
   && chmod 775 Miniconda3-latest-Linux-x86_64.sh \
   && ./Miniconda3-latest-Linux-x86_64.sh -p /opt/miniconda3 -b \
   && rm -rf Miniconda3-latest-Linux-x86_64.sh \
   && conda install jupyter -y \
   && conda upgrade --all -y \
   && conda clean --all -y

EXPOSE 8888

WORKDIR "/jupyter_files"

CMD ["/bin/bash"]
