FROM jupyterhub/jupyterhub

LABEL maintainer = "demian <demian.avendano@protonmail.com>"

ENV UTILES htop vim 

USER root 

RUN apt-get -y update && \
    apt-get -y upgrade && \
    apt-get -y install $UTILES && \
    apt-get purge && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*


COPY ./libs.txt /home/src/libs.txt
COPY ./ambermd_libs.txt /home/src/ambermd_libs.txt
COPY ./omnia_libs.txt   /home/src/omnia_libs.txt

RUN conda install --yes --file /home/src/libs.txt && \
    conda install --yes -c ambermd --file /home/src/ambermd_libs.txt && \
    conda install --yes -c omnia   --file /home/src/omnia_libs.txt


