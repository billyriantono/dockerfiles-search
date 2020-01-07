FROM docker:17.12.1-dind

# ビルド用ツールとaws-cliの追加
RUN apk upgrade && apk add --no-cache git make ca-certificates \
    py-pip python && \
    pip install --upgrade pip && \
    pip install awscli && \
    apk del --purge py-pip
