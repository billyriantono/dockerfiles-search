FROM debian:jessie

RUN apt-get update && apt-get -y upgrade

RUN apt-get install -y \
    python3-pip python3-dev python3-virtualenv \
    python3-numpy python3-scipy python3-matplotlib \
    ipython ipython-notebook python3-pandas python3-nose

RUN pip3 install --upgrade pip virtualenv
RUN pip3 install --upgrade tensorflow ipython jupyter
RUN pip3 install --upgrade pip virtualenv
RUN pip3 install --upgrade beautifulsoup4 html5lib bs4 lxml

RUN virtualenv --system-site-packages -p python3 ~/tensorflow

# prevent jupyter error
# AttributeError: 'module' object has no attribute 'ensure_future'
# https://github.com/tornadoweb/tornado/issues/2015
RUN pip3 install --ignore-installed tornado==4.4.3

RUN /bin/bash -c "source /root/tensorflow/bin/activate"

WORKDIR /notebooks

ENV PYTHONIOENCODING=UTF-8

CMD jupyter-notebook --ip="*" --no-browser --allow-root