FROM node:8.1.2
RUN node --version > /node_ver.txt

FROM python:2.7.13

COPY --from=0 /node_ver.txt .

# Do something inside a nginx container
CMD bash
