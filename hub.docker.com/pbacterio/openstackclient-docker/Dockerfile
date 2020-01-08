FROM python:alpine
RUN apk  -U add gcc musl-dev libffi-dev linux-headers openssl-dev && \
    pip install python-openstackclient python-neutronclient oslo.log

FROM python:alpine
COPY --from=0 /usr/local/lib/python3.6/site-packages /usr/local/lib/python3.6/site-packages
COPY --from=0 /usr/local/lib/python3.6/__pycache__ /usr/local/lib/python3.6/__pycache__
COPY --from=0 /usr/local/bin /usr/local/bin
CMD ["openstack"]
