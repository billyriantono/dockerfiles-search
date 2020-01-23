# Distributed under the terms of the Modified BSD License.
FROM jupyter/datascience-notebook

MAINTAINER Andrei Roudik <andrei@cs.du.edu>

USER root

# Installing nbgrader
RUN pip install nbgrader

# Install nbextensions
RUN jupyter nbextension install --sys-prefix --py nbgrader --overwrite && \
    jupyter nbextension enable --sys-prefix --py nbgrader && \
    jupyter serverextension enable --sys-prefix --py nbgrader
