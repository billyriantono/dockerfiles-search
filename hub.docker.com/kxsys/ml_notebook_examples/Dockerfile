# ARG usage in FROMs has to go up here in global

ARG jupyterq_img=kxsys/jupyterq:latest

####

FROM debian:9 AS base

####

FROM $jupyterq_img AS jupyterq

FROM jupyterq

# do not clean here, its cleaned later!
RUN apt-get update \
	&& apt-get -yy update

ARG port=8888
ENV PORT=${port}
EXPOSE ${port}/tcp

ARG VCS_REF=dev
ARG BUILD_DATE=dev

LABEL	org.label-schema.schema-version="1.0" \
	org.label-schema.name=jupyterq \
	org.label-schema.description="ML notebook examples using Jupyter kernel for kdb+" \
	org.label-schema.vendor="Kx" \
	org.label-schema.license="Apache-2.0" \
	org.label-schema.url="https://code.kx.com/q/ml/" \
	org.label-schema.version="${VERSION:-dev}" \
	org.label-schema.vcs-url="https://github.com/KxSystems/ml_notebook_examples.git" \
	org.label-schema.vcs-ref="$VCS_REF" \
	org.label-schema.build-date="$BUILD_DATE" \
	org.label-schema.docker.cmd="docker run --rm -it -v `pwd`/q:/tmp/q -p $PORT:$PORT kxsys/ml_notebook_examples"

RUN apt-get -yy --no-install-recommends install build-essential \
	&& apt-get clean \
	&& find /var/lib/apt/lists -type f -delete

COPY docker/init /init

USER kx

COPY . /home/kx/ml_notebook_examples 

RUN . /opt/conda/etc/profile.d/conda.sh \
	&& conda activate kx \
	&& pip install --no-cache-dir -r /home/kx/ml_notebook_examples/requirements.txt \
	&& conda install -y -c anaconda graphviz \
	&& conda clean -y --all 
	

USER root
#RUN apt-get remove -y --purge build-essential \
#	&& apt-get -y autoremove

ENTRYPOINT ["/init"]
CMD . /opt/conda/etc/profile.d/conda.sh \
	&& conda activate kx \
	&& printf "\npoint your browser at http://127.0.0.1:%s/tree/notebooks\n\n" $PORT \
	&& exec jupyter notebook --notebook-dir=/home/kx/ml_notebook_examples --ip='0.0.0.0' --port=$PORT --no-browser
