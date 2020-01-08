FROM ubuntu:xenial
ENV DEBIAN_FRONTEND noninteractive
ENV USERNAME jupyter

RUN apt-get -qqy update \
	&& apt-get -qqy install python-dev build-essential virtualenv python3 \
	&& apt-get -qqy autoclean \
	&& rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
	&& groupadd $USERNAME \
	&& useradd -m -d /jupyter -s /usr/sbin/nologin -g $USERNAME $USERNAME

USER $USERNAME


WORKDIR /jupyter
RUN mkdir workbooks && mkdir .jupyter
ADD conf/jupyter_notebook_config.py .jupyter/
RUN /bin/bash -c "virtualenv -p `which python3` venv && source venv/bin/activate && pip install pandas matplotlib jupyter"

EXPOSE 5050
VOLUME ["/jupyter/workbooks"]
CMD /jupyter/venv/bin/jupyter notebook --notebook-dir=/jupyter/notebooks --ip=0.0.0.0 --port=5050
