FROM fedora:23

RUN dnf -y install git python-pip

RUN python3 -m pip install -U pip

RUN pip3 install flask
RUN pip3 install flask_script
RUN pip3 install flask_bootstrap
RUN pip3 install flask_moment
RUN pip3 install flask_wtf

RUN mkdir -p /home/dev

WORKDIR /home/dev
RUN git clone https://github.com/sofiannagounine/docker_web_flask.git

EXPOSE 5000

WORKDIR /home/dev/docker_web_flask
ENTRYPOINT ["python3","hello.py","runserver","-h=0.0.0.0"]
