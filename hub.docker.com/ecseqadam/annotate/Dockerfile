FROM nfcore/base
LABEL authors="Adam Nunn" \
      email="adam.nunn@ecseq.com" \
      description="Docker image containing python3 tools for Thlaspi annotation"

COPY environment.yml /
COPY ryuto /usr/local/bin

RUN apt-get install -y gcc
RUN conda env create -f /environment.yml && conda clean -a
ENV PATH /opt/conda/envs/annotate/bin:$PATH