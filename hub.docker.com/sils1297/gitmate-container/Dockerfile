FROM coala/base
MAINTAINER Lasse Schuirmann lasse.schuirmann@gmail.com

RUN mkdir -p /usr/src/app
COPY . /usr/src/app

RUN mkdir -p /usr/src/subject

CMD [ "python", "/usr/src/app/run_coala.py" ]
