FROM	python:3.4
COPY	requirements.txt /tmp/
RUN 	pip install -r /tmp/requirements.txt --no-cache-dir
COPY	app /app/
COPY	cmd.sh /
EXPOSE	9090
CMD	["/cmd.sh"]
