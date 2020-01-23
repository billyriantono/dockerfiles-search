FROM python:3.7-stretch

WORKDIR /app

COPY . .
COPY etc/supervisord.conf /etc/

RUN apt-get update && apt-get install -y ffmpeg && \
    CC="cc -mavx2" pip3 install -U --force-reinstall --no-cache-dir pillow-simd && \
    pip3 install --no-cache-dir git+https://github.com/Supervisor/supervisor && \
    pip3 install --no-cache-dir -r ./requirements-docker.txt

ENTRYPOINT ["/usr/local/bin/supervisord"]
