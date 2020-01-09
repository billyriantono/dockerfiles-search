FROM ubuntu-debootstrap:14.04

RUN apt-get update && apt-get install --yes python python-pip postgresql-9.3 make postgresql-server-dev-9.3  python-dev libffi-dev git  && apt-get clean

RUN easy_install --upgrade pip

ADD ./ /

RUN pip install -r /docs_requirements.txt

WORKDIR /deis/docs

CMD ["/runall"]
