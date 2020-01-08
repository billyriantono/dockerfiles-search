FROM kennethreitz/pipenv

ADD . /ansible-install

RUN cd /ansible-install && pipenv install -v --deploy --system
