from python:3.6.4-slim-jessie

COPY . ${HOME}
RUN python setup.py install



EXPOSE 8080


ENTRYPOINT ["roman_numerals_webservice"]