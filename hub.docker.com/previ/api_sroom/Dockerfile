FROM previ/flask:latest

MAINTAINER Roberto Previtera <roberto.previtera@gmail.com>

RUN mkdir /appl \
    mkdir /appl/api_sroom

COPY . /appl/api_sroom

EXPOSE 5000

CMD ["python", "/appl/api_sroom/api.py"]
