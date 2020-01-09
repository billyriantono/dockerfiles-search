FROM samesense/conda-singularity-docker
MAINTAINER Perry Evans <https://github.com/samesense>

RUN apt-get update -qqq \
&& apt-get install -y wget curl git 

RUN git clone https://github.com/samesense/run-proseq \
&& cd run-proseq \
&& conda env create -f requirements.txt

RUN apt-get autoremove -y \
&& apt-get remove --purge -y git
