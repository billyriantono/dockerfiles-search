FROM 007backups/base:2.0

LABEL company="007 Backups" \
      description="7-Zip image" \
      version="16.02" \
      maintainer="info@007backups.com"


ENV LESS_THAN_P7ZIP_VERSION 16.03


RUN set -ex \
    && apk add --upgrade --no-cache \
        "p7zip<$LESS_THAN_P7ZIP_VERSION"


CMD ["7z"]
