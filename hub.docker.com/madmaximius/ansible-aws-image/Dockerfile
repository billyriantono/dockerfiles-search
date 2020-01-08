FROM kennethreitz/pipenv

RUN apt-get update

RUN apt-get install -y zip

ADD . /ansible-install

RUN cd /ansible-install && pipenv install -v --deploy --system
