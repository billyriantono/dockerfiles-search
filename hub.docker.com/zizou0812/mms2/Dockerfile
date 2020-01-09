FROM python:3.6-alpine

RUN adduser -D mms

#COPY . /mms
WORKDIR /home/mms/back

COPY requirements requirements
RUN python -m venv venv
RUN pip install pip --upgrade
RUN venv/bin/pip install -r requirements/common.txt

COPY app app
COPY config.py run.py boot.sh ./

RUN chmod +x boot.sh

ENV FLASK_APP run.py
ENV FLASK_CONFIG development

RUN chown -R mms:mms ./
USER mms

EXPOSE 5000

ENTRYPOINT ["./boot.sh"]