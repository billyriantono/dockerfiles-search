FROM python:3.8.1-slim
MAINTAINER Yasuhisa Yoshida <syou6162@gmail.com>

RUN apt-get -yq update && apt-get install -yq tk-dev git libpq-dev

RUN pip install numpy scipy matplotlib pandas jupyter jupyter_contrib_nbextensions janome psycopg2

RUN jupyter contrib nbextension install --user
RUN jupyter nbextension enable codefolding/main
RUN jupyter nbextension enable toc2/main
