FROM tensorflow/tensorflow:2.0.0-gpu-py3

WORKDIR /transformer-dialogue
COPY . .

RUN pip install -r requirements.txt
RUN chmod +x ./scripts/run_docker.sh

CMD [ "./scripts/run_docker.sh" ]