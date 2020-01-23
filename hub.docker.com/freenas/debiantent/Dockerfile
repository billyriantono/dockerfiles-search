# Migration to Bitbucket
FROM alpine
RUN apk add --no-cache bash
RUN apk add --no-cache py-pip gcc python-dev musl-dev
RUN pip install --upgrade pip
RUN pip install browsepy	
RUN mkdir /downloads

EXPOSE 8080

# Default command
CMD ["browsepy", "0.0.0.0", "8080", "--directory", "/downloads"]
