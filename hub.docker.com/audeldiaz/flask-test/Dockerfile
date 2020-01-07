FROM python:3-alpine3.7
COPY src/ /src
WORKDIR /src
COPY requirements.txt /src/requirements.txt
RUN pip install -r requirements.txt
RUN pytest
CMD [ "python", "main.py" ]