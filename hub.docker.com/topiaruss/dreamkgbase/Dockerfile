#FROM topiaruss/nvidia-ub1404cuda80:8.0-devel-cudnn5
#FROM nvidia/cuda:8.0-cudnn5-devel
#FROM nvidia/cuda:7.5-cudnn5-devel
FROM nvidia/cuda:9.2-devel-ubuntu18.04 

ENV LANG=C.UTF-8 LC_ALL=C.UTF-8

RUN apt-get update --fix-missing && \
    apt-get install -y \
    bzip2 ca-certificates gcc git libfreeimage-dev libfreeimage3 \
    libglib2.0-0 libsm6 libxext6 libxrender1 vim wget && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/

RUN echo 'export PATH=/opt/conda/bin:$PATH' > /etc/profile.d/conda.sh
RUN wget --quiet \
    https://repo.continuum.io/miniconda/Miniconda3-4.5.4-Linux-x86_64.sh \
    -O ~/miniconda.sh && \
    /bin/bash ~/miniconda.sh -b -p /opt/conda && \
    rm ~/miniconda.sh
ENV PATH /opt/conda/bin:$PATH

COPY environment.yml /home/

RUN echo 'create conda env, clean' && \
    cd /home && conda env create --name dreamkg_docker --force

# may want to integrate these into the environment.yml. Currently they use pytorch channel
RUN conda install -y --name dreamkg_docker pytorch torchvision -c pytorch


# Insert useful scripts, and timestamp the build
COPY scripts /scripts

RUN echo "gpu base created " > /created_gpubase.txt && \
    date >> /created_gpubase.txt

ENTRYPOINT ["/bin/bash", "-c"]
CMD ["/scripts/ident.sh"]
