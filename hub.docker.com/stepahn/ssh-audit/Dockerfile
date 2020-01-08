FROM python:3-alpine

WORKDIR /usr/src/app
RUN wget -O /usr/src/app/ssh-audit.py https://github.com/arthepsy/ssh-audit/raw/master/ssh-audit.py
ENTRYPOINT [ "python", "/usr/src/app/ssh-audit.py" ]
