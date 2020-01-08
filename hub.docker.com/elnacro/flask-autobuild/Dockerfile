FROM ubuntu:latest


ENV HOME_DIR="/opt/docker-sample"
ENV FLASK_APP="app.py"


RUN apt-get update && apt-get install -y apt-utils python-pip git


RUN pip install flask pyyaml
COPY ./source ${HOME_DIR}


ADD flask.conf ${HOME_DIR}/flask.conf

WORKDIR ${HOME_DIR}


EXPOSE 5000
ENTRYPOINT ["/usr/local/bin/flask", "run"]
CMD ["-h", "0.0.0.0"]