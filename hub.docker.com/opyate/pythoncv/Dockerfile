FROM python:2.7
RUN apt-get update && \
    apt-get install -y libfreetype6-dev \
                    gfortran \
                    libopenblas-dev \
                    liblapack-dev \
                    imagemagick
RUN pip install Cython
RUN pip install numpy
RUN pip install matplotlib
RUN pip install Pillow
RUN pip install scipy
RUN pip install networkx
RUN pip install scikit-learn
RUN pip install scikit-image
