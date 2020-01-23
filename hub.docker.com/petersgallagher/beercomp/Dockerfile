FROM python:3.6
ENV PYTHONUNBUFFERED 1
ENV BEERCOMP_GMAP_KEY AIzaSyAcCgCKW2DF4iYwasI0_nediRkORxFop0U
RUN mkdir /code
WORKDIR /code
ADD requirements.txt /code/
RUN pip install -r requirements.txt
ADD . /code/