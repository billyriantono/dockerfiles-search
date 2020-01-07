FROM python:2.7-alpine3.7
WORKDIR /
ADD https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-192.0.0-linux-x86_64.tar.gz /google-cloud-sdk.tar.gz
RUN tar xzvf /google-cloud-sdk.tar.gz
RUN yes | /google-cloud-sdk/install.sh
RUN /google-cloud-sdk/bin/gcloud components install app-engine-python

FROM python:2.7-alpine3.7
COPY --from=0 /google-cloud-sdk /google-cloud-sdk
ADD ./server /server
EXPOSE 8080 8000
ENV OAUTH_IS_ADMIN=1
ENTRYPOINT ["/google-cloud-sdk/bin/dev_appserver.py"]
CMD ["--admin_host", "0.0.0.0", "--host", "0.0.0.0", "--enable_host_checking", "False", "/server"]
