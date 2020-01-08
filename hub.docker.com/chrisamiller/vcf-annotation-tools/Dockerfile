FROM continuumio/miniconda3
RUN apt-get update && apt-get install -y \
    vim \
    git
WORKDIR /
RUN pip install --extra-index-url https://testpypi.python.org/pypi vcf-annotation-tools
