FROM python:2.7

RUN mkdir -p /app
RUN cd /app && git clone https://code.google.com/p/google-apis-client-generator/
RUN chmod +x /app/google-apis-client-generator/setup.py
RUN cd /app/google-apis-client-generator && python /app/google-apis-client-generator/setup.py install

ENTRYPOINT ["/app/google-apis-client-generator/generate.sh"]

