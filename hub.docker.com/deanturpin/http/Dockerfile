FROM ubuntu
RUN apt update --yes
RUN apt install --yes python
COPY . src
WORKDIR src
CMD ./serve.py
