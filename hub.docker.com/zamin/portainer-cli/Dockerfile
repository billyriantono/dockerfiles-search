FROM python:2.7-alpine
RUN pip install --no-cache-dir portainer-cli
VOLUME /stack.yml
CMD ["sh", "-c", "portainer-cli configure $BASE_URL && portainer-cli login $USERNAME $PASSWORD && portainer-cli update_stack $STACK_ID $ENDPOINT_ID /stack.yml"]
