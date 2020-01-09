FROM  debian:latest

RUN   apt-get update

RUN   DEBIAN_FRONTEND=noninteractive apt-get install -y python-pip apache2
RUN   DEBIAN_FRONTEND=noninteractive apt-get install -y texlive texlive-latex-recommended texlive-latex-extra texlive-fonts-recommended

RUN   pip install Sphinx==1.4
RUN   pip install sphinx_rtd_theme
RUN   pip install alabaster 
RUN   pip install sphinx_bootstrap_theme
RUN   rm -rf /var/www/html
RUN   ln -s /doc/build/html /var/www/html

WORKDIR /doc

CMD service apache2 start && /bin/bash 
