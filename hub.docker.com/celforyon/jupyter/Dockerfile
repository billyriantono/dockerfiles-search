FROM celforyon/cling

LABEL maintainer="Alexis Pereda <alexis@pereda.fr>"
LABEL version="1.0"
LABEL description="Docker with Jupyter"

RUN  apt update \
	&& apt install --no-install-recommends --no-install-suggests -y \
		python3-pip python3-setuptools python3-wheel \
	&& rm -rf /var/lib/apt/lists/*

RUN  pip3 install --upgrade pip \
	&& pip3 install jupyter

WORKDIR /opt/cling/Jupyter/kernel
RUN  pip3 install -e . \
	&& jupyter-kernelspec install cling-cpp11 \
	&& jupyter-kernelspec install cling-cpp14 \
	&& jupyter-kernelspec install cling-cpp1z

COPY ./bin /usr/local/bin

RUN mkdir /jupyter

WORKDIR /jupyter

ENV IP "127.0.0.1"
ENV PORT 80

VOLUME /jupyter
EXPOSE 80

CMD ["notebook"]
