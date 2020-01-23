FROM python:3.7-alpine3.8

RUN python -m pip install --upgrade pip && \    
    pip install cloudtracker && \ 
    pip install awscli --upgrade && \ 
    apk add jq

ENTRYPOINT ["cloudtracker"]