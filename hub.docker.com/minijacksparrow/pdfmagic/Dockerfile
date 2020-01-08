FROM python:2
ADD . /pdfmagic
WORKDIR /pdfmagic
RUN pip install -r requirements.txt
EXPOSE 8080
CMD ["python", "pdfmagic.py"]