FROM nfcore/base
LABEL authors="Lukas Heumos" \
      description="Docker image containing all requirements for nf-core/guideseq pipeline"

COPY environment.yml /
RUN conda env create -f /environment.yml && conda clean -a
ENV PATH /opt/conda/envs/nf-core-guideseq-1.0dev/bin:$PATH
