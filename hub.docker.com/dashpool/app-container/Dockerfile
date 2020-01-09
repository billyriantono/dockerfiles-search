#FROM python:3.7-slim-buster
FROM tiangolo/uwsgi-nginx-flask:python3.7

COPY ./requirements.txt /app/requirements.txt
WORKDIR /app
RUN pip install -r requirements.txt

COPY . /app

RUN cd pyLib && python setup.py build install && \
	cd ../my-dash-core-components && pip install . && \
	cd .. && rm -rf pyLib my-dash-core-components && \
	mv defaults.cfg ../  && \
	mv setup.sh / && chmod 700 /setup.sh

EXPOSE 5000

ENTRYPOINT ["/setup.sh"]
