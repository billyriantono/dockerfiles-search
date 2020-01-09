FROM nfcore/base
LABEL authors="domeally@coh.org" \
      description="Docker image providing trim_galore with multithread support"

COPY environment.yml /
RUN conda env create -f /environment.yml && conda clean -a
ENV PATH /opt/conda/envs/trim_galore/bin:$PATH