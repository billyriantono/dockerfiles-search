FROM python:3.7-alpine
LABEL maintainer="rhoboro <rhoboro@gmail.com>"
WORKDIR /usr/src/app
COPY template.py setup.py ./
RUN pip install .
CMD ["template"]
