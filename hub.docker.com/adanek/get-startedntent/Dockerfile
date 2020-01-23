FROM python:3.7-alpine

WORKDIR /usr/src/app

COPY . .
RUN pip install .

ENTRYPOINT ["dogwhistle"]
CMD ["--help"]
