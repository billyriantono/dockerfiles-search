FROM python

COPY . /srv
RUN pip install -r /srv/requirements.pip

ENTRYPOINT ["python3", "/srv/src/cf.py"]
CMD ["-h"]