FROM jupyter/scipy-notebook

LABEL maintainer="Adham Beyki <adham@worksafe.vic.gov.au>"

USER $NB_UID
RUN conda install --quiet --yes \
    'conda-forge::boto3' \
    'conda-forge::awscli' \
    'conda-forge::smart_open' \
    'conda-forge::s3fs'

USER $NB_UID
