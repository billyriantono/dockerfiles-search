FROM python:3.7.2-stretch

WORKDIR /opt/dbg-debarcode
COPY . .
RUN apt-get update && \
    apt-get install --yes pigz && \
    apt-get install --yes parallel 
RUN python -m venv ./venv
RUN ./venv/bin/pip install -r requirements.txt

# Pull in some ARGS for defining container name
ARG IMAGE_NAME
ARG SOURCE_BRANCH
ARG SOURCE_COMMIT
RUN printf "Container Name: $IMAGE_NAME\n" > imageInfo.txt
RUN printf "Source Branch: $SOURCE_BRANCH\n" >> imageInfo.txt
RUN printf "Source Commit: $SOURCE_COMMIT" >> imageInfo.txt

ENTRYPOINT ["bash", "/opt/dbg-debarcode/scripts/entrypoint.sh"]

