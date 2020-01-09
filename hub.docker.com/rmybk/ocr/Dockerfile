FROM python:3.6.9-buster

RUN apt-get -y update && apt-get install -y \
	vim \
	poppler-utils \
	tesseract-ocr \
	libtesseract-dev
RUN useradd --user-group --create-home --shell /bin/bash pythonuser

WORKDIR /home/pythonuser

CMD /bin/bash

USER pythonuser
