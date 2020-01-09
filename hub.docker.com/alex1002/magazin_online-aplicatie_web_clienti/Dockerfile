FROM python:3-slim
WORKDIR /aplicatie
ADD library_requirements.txt .
RUN apt-get update
RUN apt-get install -y $(cat library_requirements.txt)
ADD python_library_requirements.txt .
RUN pip install -r python_library_requirements.txt
ADD . .
CMD ["sh", "-c", "chmod +x start.sh"]
EXPOSE 80
WORKDIR /
CMD ["sh", "aplicatie/start.sh"]

