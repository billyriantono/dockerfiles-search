FROM continuumio/miniconda3:4.6.14

LABEL maintainer="Luigi Di Fraia"

RUN apt-get update --fix-missing

# Disable certificate verification in case CA certificates expired, but reenable after updating them
#RUN conda config --set ssl_verify no
#RUN conda update openssl ca-certificates certifi
#RUN conda config --set ssl_verify yes

# Certificate verification is currently failing, so disable it for now
RUN conda config --set ssl_verify no

RUN conda config --set channel_priority strict

ADD environment.yml /tmp/environment.yml
RUN conda env create -f /tmp/environment.yml

ENV PATH /opt/conda/envs/cubeenv/bin:$PATH

RUN jupyter nbextension enable --py --sys-prefix widgetsnbextension
RUN jupyter nbextension enable --py --sys-prefix ipyleaflet

RUN groupadd -r localuser && \
	useradd -s /bin/bash --no-log-init -r -g localuser localuser && \
	mkdir /home/localuser && \
	chown localuser.localuser /home/localuser

USER localuser

ENV PATH /opt/conda/envs/cubeenv/bin:$PATH

RUN echo "\n[ -f ~/.motd ] && cat ~/.motd" >> /home/localuser/.bashrc
RUN echo ". /opt/conda/etc/profile.d/conda.sh" >> /home/localuser/.bashrc
RUN echo "conda activate cubeenv" >> /home/localuser/.bashrc

COPY .motd /home/localuser/.motd
COPY .datacube.conf /home/localuser/.datacube.conf

WORKDIR /home/localuser

CMD jupyter notebook \
	--allow-root \
	--NotebookApp.ip='0.0.0.0' \
	--NotebookApp.port='8888' \
	--NotebookApp.token='secretpassword' \
	--NotebookApp.open_browser='False'

