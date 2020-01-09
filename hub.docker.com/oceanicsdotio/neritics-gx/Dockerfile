FROM continuumio/miniconda3:4.6.14 AS base

COPY config/environment.yml ./
RUN conda env create -f environment.yml && rm -rf /opt/conda/pkgs/*

FROM continuumio/miniconda3:4.6.14

COPY --from=base /opt/conda/ /opt/conda/

WORKDIR neritics_gx

COPY openapi/api.yml ./openapi/api.yml
COPY neritics_gx ./neritics_gx
COPY src ./src

RUN chmod +x ./src/start.sh

ENTRYPOINT ["./src/start.sh"]