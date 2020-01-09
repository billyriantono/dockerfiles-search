FROM hashicorp/terraform:light

RUN apk add --update --no-cache \
    python3 \
    zip

RUN pip3 install --upgrade pip && \
    pip3 install --upgrade --target /aws-sdk \
    boto3 \
    requests_aws4auth
