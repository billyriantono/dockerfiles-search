# Build container for frontend
FROM node:8-alpine
COPY ./frontend /app/frontend
WORKDIR /app/frontend
RUN yarn install
RUN yarn run build

# Actual backend container
FROM python:3.7-alpine
MAINTAINER Michael Pucher "michael.pucher.main+docker@gmail.com"

COPY backend /app/backend
WORKDIR /app

# Install required python dependencies
RUN set -ex; \
    apk add --no-cache git; \
    pip install --no-cache-dir -r backend/requirements.txt; \
    apk del git

COPY --from=0 /app/dist /app/dist
COPY app.py /app/app.py

CMD ["gunicorn", "app:app", "-w", "1", "--bind", "0.0.0.0:5000"]
