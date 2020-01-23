FROM petzi/pre-commit:1.15.2-9
RUN apk add --no-cache \
    gcc \
    musl-dev \
    python3-dev
COPY requirements.txt /
RUN pip3 install --no-cache-dir -r requirements.txt
COPY .pre-commit-config.yaml /
