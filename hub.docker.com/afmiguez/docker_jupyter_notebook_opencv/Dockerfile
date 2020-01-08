#This is a comment
FROM ubuntu:14.04
MAINTAINER Alessandro Miguez <afmiguez@gmail.com>
RUN apt-get update && apt-get install -y wget
RUN wget https://repo.continuum.io/archive/Anaconda2-4.2.0-Linux-x86_64.sh
RUN bash Anaconda2-4.2.0-Linux-x86_64.sh -b -p $HOME/anaconda
RUN mkdir /home/images
ADD [^.]* /home/images/

ENV PATH="/root/anaconda/bin:${PATH}"

RUN conda install -y opencv

# Add Tini. Tini operates as a process subreaper for jupyter. This prevents
# kernel crashes
ENV TINI_VERSION v0.6.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /usr/bin/tini
RUN chmod +x /usr/bin/tini
ENTRYPOINT ["/usr/bin/tini", "--"]

EXPOSE 8888
CMD ["jupyter", "notebook", "--no-browser","--port=8888","--ip=0.0.0.0","--notebook-dir=/home"]
