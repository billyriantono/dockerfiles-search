FROM jupyter/scipy-notebook 

MAINTAINER Max Joseph <maxwell.b.joseph@colorado.edu> 

COPY environment.yml environment.yml

ENV JUPYTER_LAB_ENABLE=yes

RUN conda env update -n root -f environment.yml && \
	rm environment.yml

