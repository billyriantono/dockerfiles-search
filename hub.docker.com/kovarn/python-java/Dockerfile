FROM kovarn/python-java:python35-java8

MAINTAINER Mustafa Khandwawala <mustafa.svnit@gmail.com>

COPY environment.yml /
RUN conda env create -f /environment.yml
RUN echo source activate Py36Sci >> /root/.bashrc \
    && echo 'export PYTHONPATH="/dist/python"' >> /root/.bashrc \
    && echo 'export PDFREAD="/dist/java"' >> /root/.bashrc
COPY java /dist/java
