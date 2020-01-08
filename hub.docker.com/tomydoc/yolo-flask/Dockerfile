FROM python:3.7.5-slim-stretch

ENV LANG=C.UTF-8 LC_ALL=C.UTF-8
ENV PYTHON_VERSION=3.7
ENV PYTHONPATH=$PYTHONPATH:/work/ml

RUN apt-get update \
 && apt-get install -y git wget vim curl build-essential \ 
                       bzip2 curl grep sed dpkg xclip \
 && pip install flask opencensus-ext-flask opencensus-ext-azure

WORKDIR /work
ADD ./ml_server.py /work/

CMD ["python", "ml_server.py"]