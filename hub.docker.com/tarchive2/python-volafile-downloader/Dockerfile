FROM python:3.7

RUN git clone https://github.com/tarchive/python-volafile-downloader.git

WORKDIR /python-volafile-downloader

RUN pip install -r requirements.txt

VOLUME /python-volafile-downloader

ENTRYPOINT ["python", "./downloader.py"]
