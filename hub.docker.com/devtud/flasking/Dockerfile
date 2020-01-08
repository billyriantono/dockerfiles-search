FROM node:11.9.0-alpine as builder

WORKDIR /opt/flasking/

COPY src/ ./src/
COPY public/ ./public/
COPY package.json .
RUN npm install && npm run build

FROM python:3.7.2-alpine3.9

WORKDIR /opt/flasking

COPY requirements.txt .

RUN pip install -r requirements.txt

COPY --from=builder /opt/flasking/build/ ./build/
COPY server/ ./server/

RUN ls server
RUN ls build

ENV FLASK_APP=server/app.py

CMD ["flask", "run", "--port=7082", "--host=0.0.0.0"]
