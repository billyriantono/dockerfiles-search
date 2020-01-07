FROM jfloff/alpine-python:3.4-slim
RUN /entrypoint.sh \
	-p requests \
	-p ipython \
	-p flask \
	&& echo
WORKDIR /workspace
CMD ["ipython"]

