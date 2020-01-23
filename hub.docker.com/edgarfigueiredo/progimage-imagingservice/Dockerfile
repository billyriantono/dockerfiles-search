FROM tiangolo/meinheld-gunicorn-flask:python3.7
LABEL Author=edgar@edgarneto.com
ADD . /app
RUN pip install -r requirements.txt
ENV PORT=5000
ENV LISTEN_PORT=5000
ENV LOG_LEVEL=debug
ENV MODULE_NAME=index
ENV VARIABLE_NAME=app
EXPOSE 5000
