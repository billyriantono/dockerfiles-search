FROM python:3.7-stretch

RUN mkdir /build
COPY . /build/
RUN pip install /build && rm -rf /build

EXPOSE 8500

ENTRYPOINT [ "swarmer" ]