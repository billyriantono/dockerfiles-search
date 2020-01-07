FROM picymru/base:latest
RUN apk-install python3 python3-dev py-pip && \
	mkdir -p /app

WORKDIR /app

ONBUILD ADD requirements.txt /app
ONBUILD RUN pip install -r requirements.txt
ONBUILD ADD . /app