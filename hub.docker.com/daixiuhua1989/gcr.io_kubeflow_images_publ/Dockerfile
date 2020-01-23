FROM python:3.6-alpine

RUN pip install --no-cache-dir requests

COPY gitlab-release /usr/bin/

CMD ["/usr/bin/gitlab-release", "--help"]
 update
RUN apt-get install --force-yes -y ffmpeg git
RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Create application folder
RUN mkdir /app

# Download banana-split
RUN git clone https://github.com/pathartl/banana-split /app

# Copy startup script
COPY start.sh /app/

# Start application
WORKDIR /app
CMD ./start.sh

# Declare application port
EXPOSE 8080
