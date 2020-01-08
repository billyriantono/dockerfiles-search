FROM python:3.6-slim
COPY . /app
WORKDIR /app
RUN pip install -r requirements.txt
EXPOSE 5000

ENV MODEL_NAME MnistModel
ENV API_TYPE REST
ENV SERVICE_TYPE MODEL
ENV PERSISTENCE 0

CMD exec seldon-core-microservice $API_TYPE --service-type $SERVICE_TYPE --persistence $PERSISTENCE