FROM python

COPY . /usr/src/app
WORKDIR /usr/src/app
RUN pip --no-cache-dir install -r requirements.txt

CMD ["python", "__main__.py"]