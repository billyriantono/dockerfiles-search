FROM continuumio/miniconda3

LABEL Name=pipeline Version=0.0.1

WORKDIR /app

ADD environment.yml /app
RUN conda env create -f environment.yml && conda clean -a -y
RUN echo "source activate bfa" >> ~/.bashrc

#
ADD docker-entrypoint.sh /app
ENTRYPOINT [ "/app/docker-entrypoint.sh" ]
CMD /bin/bash
#
ADD . /app
