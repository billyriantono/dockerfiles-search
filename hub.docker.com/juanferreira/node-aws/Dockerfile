FROM node:10.16-jessie

RUN apt-get update && apt-get install python-dev python-pip -y

RUN pip install awscli

# Clean up apt-get cache (helps keep the image size down)
RUN apt-get autoclean && apt-get clean
RUN rm -rf /var/lib/apt/lists/* /tmp/*

CMD [ "bash" ]