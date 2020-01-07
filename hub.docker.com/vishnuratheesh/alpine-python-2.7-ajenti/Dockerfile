FROM jfloff/alpine-python:2.7-slim
RUN /entrypoint.sh \
  -p ajenti-panel \
  -p ajenti.plugin.dashboard \
  -p ajenti.plugin.settings \
  -p ajenti.plugin.plugins \
  -b libxml2-dev \
  -b libxslt-dev \
  -b libffi-dev \
  -b libressl-dev \
&& echo
CMD ["sudo ajenti-panel"]
# you won't be able to add more dependencies later though-- see 'Debugging'
