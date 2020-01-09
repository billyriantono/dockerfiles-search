FROM ubuntu:18.10

WORKDIR /home
ENV LC_ALL C
SHELL ["/bin/bash", "-c"]

RUN apt-get update && apt-get install -y bzip2 git wget unzip && apt-get clean

RUN wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh
RUN bash Miniconda3-latest-Linux-x86_64.sh -bf && rm Miniconda3-latest-Linux-x86_64.sh
ENV PATH="/root/miniconda3/bin:${PATH}"

RUN git clone http://bitbucket.org/scilifelab-lts/reproducible_research_example.git
RUN conda config --add channels defaults && \
    conda config --add channels bioconda && \
    conda config --add channels conda-forge
RUN conda env create -f reproducible_research_example/conda_env.yml

RUN source activate my_conda_env && conda install r-tinytex=0.5 && echo "tinytex::install_tinytex()" | R --vanilla

CMD source activate my_conda_env;cd reproducible_research_example;snakemake results/SRR068303.pdf
