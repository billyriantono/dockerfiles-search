FROM python:3-slim
ADD ./Dictionary-2.py /Dictionary-2.py
ADD /requirements.txt .
RUN pip install -r requirements.txt
ENTRYPOINT ["python", "./Dictionary-2.py"]