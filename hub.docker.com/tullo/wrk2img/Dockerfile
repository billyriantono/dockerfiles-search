FROM python:slim
RUN pip install wrk2img
RUN groupadd -g 1000 wrk2img
RUN useradd -u 1000 -g 1000 --system wrk2img
RUN mkdir /data && chown 1000:1000 /data
USER wrk2img
WORKDIR /data
ENTRYPOINT [ "bash" ]
