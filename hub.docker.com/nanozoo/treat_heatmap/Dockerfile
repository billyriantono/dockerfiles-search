FROM continuumio/miniconda3
RUN apt update && apt-get clean
RUN conda config --add channels conda-forge && conda config --add channels default
RUN conda install pandas numpy seaborn matplotlib=3.1.2
