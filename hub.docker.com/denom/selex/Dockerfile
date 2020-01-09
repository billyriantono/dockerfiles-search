FROM nfcore/base
LABEL authors="Denis O'Meally" \
      description="Docker image containing all requirements for nf-core/selex pipeline"

COPY environment.yml /
RUN conda env create -f /environment.yml && conda clean -a
ENV PATH /opt/conda/envs/nf-core-selex-1.0dev/bin:$PATH
