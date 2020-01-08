FROM python:3

LABEL maintainer "Michael Lambert"
LABEL image_type "Python with Jupyter"

ENV DOC_ROOT /home/jupyter/code

RUN useradd --create-home --shell /bin/bash jupyter 
RUN apt-get update \
	&& python3 -m pip install --upgrade pip \
	&& python3 -m pip install numpy scipy matplotlib ipython jupyter pandas sympy nose

WORKDIR ${DOC_ROOT}

USER jupyter

RUN jupyter notebook --generate-config

EXPOSE 8888

CMD ["jupyter", "notebook", "--allow-root", "--port=8888", "--no-browser", "--ip=0.0.0.0"]
