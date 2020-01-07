FROM ubuntu-debootstrap
MAINTAINER Stefan Baur

COPY scripts scripts

RUN chmod +x /scripts/*; /scripts/setup; /scripts/cleanup -f bash sh dash cat cp tty mktemp rm grep groups ls du python python2 python2.7 ipython ipython2.7 julia ldconfig ldconfig.real git git-receive-pack git-shell git-upload-archive git-upload-pack sudo

WORKDIR /data

# Define default command.
CMD sudo -H -u user ipython notebook --port=8888 --ip=0.0.0.0 --profile=julia --no-browser --notebook-dir=/data/notebooks

EXPOSE 8888

