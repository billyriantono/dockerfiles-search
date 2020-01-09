FROM ipython/ipython:3.x

MAINTAINER Sebastien Chassot (sinux) <sebastien@sinux.net>

VOLUME /notebooks
WORKDIR /notebooks

EXPOSE 8888

# You can mount your own SSL certs as necessary here
ENV PEM_FILE /key.pem
# $PASSWORD will get `unset` within notebook.sh, turned into an IPython style hash
ENV PASSWORD Dont make this your default
ENV USE_HTTP 0

RUN apt-get update && apt-get install -y texlive-latex-recommended
RUN apt-get install -y texlive-fonts-recommended
RUN apt-get install -y texlive-latex-extra

RUN apt-get install -y python-scipy python-numpy python-matplotlib
RUN apt-get install -y python3-scipy python3-numpy python3-matplotlib
RUN apt-get install -y octave r-base
RUN pip install oct2py rpy2
RUN pip3 install oct2py rpy2

ADD notebook.sh /
RUN chmod u+x /notebook.sh

CMD ["/notebook.sh"]
