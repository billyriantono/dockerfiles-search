FROM python:latest

# actualizando imagen docker e instalando requerimientos
RUN apt-get update && apt-get install -y stress cpulimit psmisc

# copiar aplicacion
RUN mkdir /stress
COPY server.py /stress/server.py

# instalar dependencias python
RUN pip install flask psutil

# configurando CMD y WORKDIR
CMD ["/usr/local/bin/python", "server.py"]
WORKDIR /stress