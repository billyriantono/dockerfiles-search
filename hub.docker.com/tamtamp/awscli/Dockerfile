FROM alpine
MAINTAINER tamtamp


RUN apk update && apk upgrade && \
    apk add git wget bash less groff py-pip jq curl && \
    pip install --upgrade pip
RUN pip install awscli==1.16.125

ENTRYPOINT []
CMD ["tail","-f","/dev/null"]
    
