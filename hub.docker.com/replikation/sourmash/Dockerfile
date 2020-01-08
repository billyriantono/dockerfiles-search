FROM replikation/debian_basic
MAINTAINER Christian Brandt <christian.jena@gmail.com>
RUN apt-get update
RUN apt-get install -y python-dev python-tk
RUN wget https://bootstrap.pypa.io/get-pip.py
RUN python get-pip.py
RUN pip install numpy
RUN pip install scipy
RUN pip install matplotlib
RUN sed -i 's/tkagg/agg/g' /usr/local/lib/python2.7/dist-packages/matplotlib/mpl-data/matplotlibrc
RUN mkdir /root/.config/
RUN mkdir /root/.config/matplotlib
RUN /bin/sh -c "echo 'backend: Agg' > /root/.config/matplotlib/matplotlibrc"
# from the sourmash github
ENV PACKAGES python-setuptools ca-certificates
ENV SOURMASH_VERSION master
RUN apt-get update && \
    apt-get install -y --no-install-recommends ${PACKAGES} && \
    apt-get clean

RUN git clone https://github.com/dib-lab/sourmash.git -b ${SOURMASH_VERSION} && \
    cd sourmash && \
    python setup.py install
