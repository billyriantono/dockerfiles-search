FROM continuumio/miniconda

COPY SQuIRE-env.yml /

RUN conda env create -f /SQuIRE-env.yml && conda clean -a

RUN git clone https://github.com/wyang17/SQuIRE; cd SQuIRE; pip install -e .

ENV PATH /opt/conda/envs/SQuIRE_env/bin:$PATH

COPY LIONS-env.yml /

Run git clone https://github.com/ababaian/LIONS.git

RUN conda env create -f /LIONS-env.yml python=3.5  && conda clean -a

ENV PATH /opt/conda/envs/LIONS_env/bin:$PATH
ENV PATH /LIONS/:$PATH
