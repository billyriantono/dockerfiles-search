FROM python:3.7-alpine
LABEL exposed.command.single=createmd

COPY results.sh /
COPY requirements.txt /
RUN apk add git && \
    pip install -r /requirements.txt

RUN pip install git+https://github.com/CivicActions/createmd.git#egg=createmd

VOLUME /results
WORKDIR /src
ENTRYPOINT ["/results.sh"]
CMD ["--help"]