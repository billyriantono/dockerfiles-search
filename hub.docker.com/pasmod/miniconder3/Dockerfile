FROM pasmod/base

WORKDIR /var/www

RUN apt-get update
RUN apt-get install -y python3-dev

RUN wget http://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh  -O miniconda.sh && \
    bash miniconda.sh -b -p /root/miniconda && \
    rm /var/www/miniconda.sh && \
    /root/miniconda/bin/conda config --set always_yes True --set changeps1 True && \
    /root/miniconda/bin/conda update -q conda && \
    /root/miniconda/bin/conda info -a && \
    /root//miniconda/bin/pip install ipython[notebook]

ADD . .
RUN chmod +x start-notebook.sh

ENV PATH="/root/miniconda/bin:$PATH"
ENV PYTHONPATH /var/www
