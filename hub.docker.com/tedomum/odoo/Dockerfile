FROM odoo:8.0

USER root

RUN apt-get update \
 && apt-get install -y --no-install-recommends python-dev gcc python-pip file wget \
 && apt-get clean

RUN pip install genshi phonenumbers beautifulsoup4

RUN wget https://github.com/aeroo/aeroolib/archive/master.tar.gz \
 && tar -xf master.tar.gz \
 && cd aeroolib-master \
 && python setup.py install

RUN pip install unicodecsv

USER odoo
