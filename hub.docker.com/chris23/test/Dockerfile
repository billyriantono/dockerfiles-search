FROM ubuntu:latest
COPY tfile.txt tmp/
RUN chown root:root tmp/tfile.txt
RUN chmod -R 777 tmp/tfile.txt
CMD cat tmp/tfile.txt
