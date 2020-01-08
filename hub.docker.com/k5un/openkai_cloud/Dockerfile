FROM python:3.7
ENV PYTHONUNBUFFERED 1
ENV SECRET_KEY jjaom@8n0_jg3l@qlapt$-hsrs5n@*nynqg$658a3bz&8@!0@&
RUN mkdir /usr/src/webapps
WORKDIR /usr/src/webapps
COPY . /usr/src/webapps/
RUN pip install -r requirements.txt