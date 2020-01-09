FROM python:3.7-alpine

WORKDIR /app

ENV PYTHONPATH=/app
ENV DATASET_TAR_FILE_PATH /app/yelp_dataset.tar
ENV DATASET_FOLDER_PATH /app/dataset
ENV RESULTS_FOLDER_PATH /app/results

VOLUME ${DATASET_FOLDER_PATH}
VOLUME ${RESULTS_FOLDER_PATH}

COPY . .

CMD ["python", "data_challenge/wrapper.py"]
