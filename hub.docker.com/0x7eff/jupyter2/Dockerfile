# Choose your desired base image
FROM python:2.7

RUN apt-get update
RUN apt-get -y install net-tools less vim
# install jupyter via pip2
RUN pip install jupyter
#RUN pip install git+https://github.com/jupyter/notebook
COPY ./requirements.txt /root
COPY ./entryscript.sh /root
WORKDIR /root
RUN pip install -r requirements.txt

EXPOSE 8888
WORKDIR /opt/notebooks

ENTRYPOINT ["/root/entryscript.sh"]