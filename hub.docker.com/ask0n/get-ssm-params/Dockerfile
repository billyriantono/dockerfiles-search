FROM alpine:3.5

ENV GET_SSM_VERSION=v1.3.0

RUN apk --no-cache add curl ca-certificates && update-ca-certificates
RUN curl -fsSL https://github.com/ProjectThor/get-ssm-params/releases/download/${GET_SSM_VERSION}/get-ssm-params > /usr/local/bin/get-ssm-params \
    && chmod +x /usr/local/bin/get-ssm-params
RUN apk del --purge curl
