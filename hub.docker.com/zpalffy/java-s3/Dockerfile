FROM java

MAINTAINER Eric Olson <zpalffy@gmail.com>

# Copy the default s3 config to home dir
COPY .s3cfg /root/

# add the s3 command
RUN java -version && apt-get update && apt-get -y install s3cmd