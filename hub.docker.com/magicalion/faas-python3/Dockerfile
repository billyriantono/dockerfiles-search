FROM magicalion/singleuser:latest-gpu

USER root

# Alternatively use ADD https:// (which will not be cached by Docker builder)
RUN apt-get update -y && apt-get install -y curl && echo "Pulling watchdog binary from Github." \
    && curl -sSL https://github.com/openfaas/faas/releases/download/0.7.7/fwatchdog > /usr/bin/fwatchdog \
    && chmod +x /usr/bin/fwatchdog

#RUN echo "http://dl-8.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories
#RUN apk --no-cache --update-cache add gcc gfortran build-base wget freetype-dev libpng-dev openblas-dev
#RUN apk update && apk upgrade && apk add --no-cache alpine-sdk gcc gfortran python-dev build-base wget freetype-dev libpng-dev openblas-dev
#RUN apk update && apk upgrade && apk add --no-cache jpeg-dev
#RUN apk update && apk upgrade && apk add --no-cache libc6-compat
#RUN apk add --no-cache --update python-dev gfortran py-pip build-base
#RUN ln -s /usr/include/locale.h /usr/include/xlocale.h

#ADD https://github.com/scipy/scipy/releases/download/v1.0.0/scipy-1.0.0-cp36-cp36m-manylinux1_x86_64.whl .
#RUN pip install scipy-1.0.0-cp36-cp36m-manylinux1_x86_64.whl
#RUN BLAS=~/src/BLAS/libfblas.a LAPACK=~/src/lapack-3.5.0/liblapack.a pip install numpy
#RUN BLAS=~/src/BLAS/libfblas.a LAPACK=~/src/lapack-3.5.0/liblapack.a pip install scipy

WORKDIR /root/

RUN apt-get update -y && apt-get install -y --reinstall build-essential

COPY base_requirements.txt   .
#RUN conda install -y pygpu
RUN /home/jovyan/.virtualenvs/basenv/bin/pip install -r base_requirements.txt -i https://pypi.python.org/simple
#RUN pip install -r requirements.txt -i https://mirrors.ustc.edu.cn/pypi/web/simple

COPY index.py           .

ENV fprocess="python3 index.py"
ENV read_timeout=300
ENV write_timeout=300
ENV upstream_timeout=300
ENV exec_timeout=300
ENV hard_timeout=300
ENV write_debug=true
