FROM continuumio/miniconda3:4.6.14 AS base

COPY config/environment.yml ./
RUN conda env create -f environment.yml && rm -rf /opt/conda/pkgs/*

FROM continuumio/miniconda3:4.6.14

COPY --from=base /opt/conda/ /opt/conda/

WORKDIR goodbuoy
COPY openapi/api.yml ./openapi/api.yml
COPY goodbuoy ./goodbuoy
COPY src ./src

ENV PATH /opt/conda/envs/goodbuoy/bin:$PATH
RUN chmod +x ./src/start.sh

CMD ["./src/start.sh"]
