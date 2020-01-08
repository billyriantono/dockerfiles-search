FROM felix11h/scipy3_env
MAINTAINER felix11h.dev@gmail.com

USER root
RUN pip3 install --upgrade pip
RUN pip3 install jupyter

RUN pip3 install RISE
RUN jupyter-nbextension install rise --py --sys-prefix
RUN jupyter-nbextension enable rise --py --sys-prefix

EXPOSE 8888
