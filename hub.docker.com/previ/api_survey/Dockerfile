FROM previ/flask

MAINTAINER Roberto Previtera <roberto.previtera@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

EXPOSE 5000

RUN mkdir /appl \
    mkdir /appl/api_survey

COPY . /appl/api_survey

CMD ["python", "/appl/api_survey/api.py"]
