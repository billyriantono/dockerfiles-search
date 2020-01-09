FROM ubuntu:latest

RUN apt-get update
RUN apt-get install -y dialog apt-utils git wget
RUN apt-get install -y python3 python3-pip

RUN pip3 install matplotlib

RUN pip3 install tqdm \
    numpy \
    pandas \
    imageio \
    git+https://github.com/christang/patsy.git@patsy-pickles \
    dash \
    dash_renderer \
    dash_core_components \
    dash_html_components \
    dash_table_experiments \
    h5py \
    statsmodels \
    luigi \
    scipy \
    nose \
    numba \
    quandl \
    git+https://github.com/PennWhartonBudgetModel/Utilities \
    pipenv \
    botocore \
    pylint

RUN wget https://dl.bintray.com/boostorg/release/1.65.1/source/boost_1_65_1.tar.bz2 && \
    tar --bzip2 -xf boost_1_65_1.tar.bz2 && \
    mkdir boost && \
    cd boost_1_65_1 && \
    ./bootstrap.sh --with-python=python3.6 --prefix=~/boost && \
    ./b2 stage && \
    cd .. && \
    rm boost_1_65_1.tar.bz2
