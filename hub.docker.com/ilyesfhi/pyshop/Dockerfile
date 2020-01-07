FROM python:3.7.3

RUN mkdir Pyshop
WORKDIR Pyshop
COPY ./requirement.txt /Pyshop/
RUN pip install -r requirement.txt
COPY . .

EXPOSE 8000
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
