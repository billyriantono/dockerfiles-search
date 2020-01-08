FROM python:3
ADD __main__.py /
ADD _version.py /
ADD README.md /
ADD requirements.txt /
RUN pip install -r requirements.txt
CMD [ "python", "./__main__.py" ]