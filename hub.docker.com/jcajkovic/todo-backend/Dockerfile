FROM python:2.7-alpine
ADD . /todo
WORKDIR /todo
EXPOSE 5050
RUN pip install -r requirements.txt
ENTRYPOINT ["python", "todo-backend.py"]
