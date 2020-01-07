FROM jhgoodwin/python35base
# modeled from: https://www.aptible.com/documentation/enclave/tutorials/faq/dockerfile-caching/pip-dockerfile-caching.html
# If needed, install system dependencies here

# Add requirements.txt before rest of repo for caching
ADD requirements.txt /app/
WORKDIR /app
RUN pip install -r requirements.txt

ADD . /app

CMD ["python", "-u", "/app/main.py"]
#CMD ["/bin/bash"]
