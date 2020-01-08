FROM python:3.7

#installing tini
ENV TINI_VERSION v0.15.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini
RUN chmod +x /tini
ENTRYPOINT ["/tini","--"]

#RUN echo "deb http://deb.debian.org/debian jessie-backports main" | tee --append /etc/apt/sources.list.d/jessie-backports.list > /dev/null &&\
#      apt-get update  && apt-get install -y --no-install-recommends -t jessie-backports openjdk-8-jre

#installing jupyter-scala
#RUN cd /tmp &&\
#      wget https://raw.githubusercontent.com/alexarchambault/jupyter-scala/master/jupyter-scala && \
#      /bin/bash jupyter-scala

#installing bash_kernel
RUN pip3 install bash_kernel

#installing extern requirements
COPY requirements.txt /tmp
RUN pip install --no-cache-dir -r /tmp/requirements.txt



#activating the kernels and extensions
RUN jupyter nbextension enable --py --sys-prefix widgetsnbextension
RUN jupyter serverextension enable --py jupyter_http_over_ws
RUN python -m bash_kernel.install

#folder for mounting the notebooks folder
RUN mkdir -p /usr/src/app
VOLUME /usr/src/app
WORKDIR /usr/src/app


EXPOSE 8888

CMD ["jupyter","notebook","--ip='0.0.0.0'","--NotebookApp.token=''","--allow-root","--NotebookApp.allow_origin='https://colab.research.google.com'"]
