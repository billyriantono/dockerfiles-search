ARG BASE_CONTAINER=jupyter/all-spark-notebook
FROM $BASE_CONTAINER

USER root

# BASH Kernel
RUN pip install metakernel_bash --upgrade && \
    python -m metakernel_bash install
