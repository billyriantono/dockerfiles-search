FROM jupyter/scipy-notebook

# Variables de entorno
ENV RPM_PATH=/solutions/app/rpm \
	PIP_PATH=/solutions/app/pip

USER root
RUN whoami
# Script de arranque
COPY initial.py /solutions/
#RUN chmod 777 /solutions/initial.py && \
#	chmod a+x /solutions/initial.py && \
#	sed -i -e 's/\r$//' /solutions/initial.py

RUN chmod 777 /solutions/initial.py && \
	chmod a+x /solutions/initial.py && \
	sed -i -e 's/\r$//' /solutions/initial.py


# Volumenes para el python
VOLUME /solutions/app


CMD ["python3", "/solutions/initial.py"]