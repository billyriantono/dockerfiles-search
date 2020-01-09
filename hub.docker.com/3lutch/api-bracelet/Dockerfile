FROM python:3
COPY requirements.txt /
ADD _version.py /
ADD __main__.py /
RUN pip install -r requirements.txt
CMD [ "python", "./__main__.py" ]
