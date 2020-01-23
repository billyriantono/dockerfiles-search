FROM python:3.7.3-stretch

COPY requirements.txt /tmp/

RUN pip install -r /tmp/requirements.txt

RUN useradd --create-home appuser
WORKDIR /home/appuser
USER appuser
ENV PYTHONUNBUFFERED=0

# COPY yourscript.py .

# CMD [ "python", "./yourscript.py" ]

