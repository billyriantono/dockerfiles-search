FROM python:3.7-alpine

VOLUME /workspace/resources/userdata

WORKDIR /workspace
COPY requirements.txt /workspace

# Environment Variables for future use
ENV BOT_TOKEN telegram_bot_token
ENV UPDATE_INTERVAL 300

RUN mkdir -p /workspace/resources/userdata
RUN apk update && apk add gcc musl-dev libffi-dev openssl-dev
RUN pip install --no-cache-dir -r requirements.txt

COPY . /workspace

CMD python .docker/initconfig.py && python robotrss.py
