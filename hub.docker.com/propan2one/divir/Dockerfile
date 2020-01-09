FROM nfcore/base
LABEL authors="Delmotte Jean" \
      description="Docker image containing all requirements for nf-core/divir pipeline"

COPY environment.yml /
RUN conda env create -f /environment.yml && conda clean -a
ENV PATH /opt/conda/envs/nf-core-divir-1.0dev/bin:$PATH
