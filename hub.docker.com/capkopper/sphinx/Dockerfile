FROM python:3.4.2-wheezy

RUN pip install sphinx
RUN pip install sphinx_rtd_theme
RUN pip install sphinxcontrib-blockdiag
RUN apt-get update && \
    apt-get install graphviz -y

WORKDIR /doc

CMD ["/bin/bash"]
