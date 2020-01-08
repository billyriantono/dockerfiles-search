FROM designmynight/ubuntu16.04-build-tools:latest

RUN gem install deb-s3

CMD deb-s3 upload \
    --preserve-versions \
    --prefix ${APPLICATION_NAME}/ubuntu/xenial \
    --bucket ${BUCKET} \
    --access-key-id=${ACCESS_KEY} \
    --secret-access-key=${SECRET_KEY} \
    --sign=${GPG_KEY} \
    --s3-region=${S3_REGION}} \
    -c=${CODENAME} \
    pkg/${APPLICATION_NAME}_${PKG_VERSION}_amd64.deb