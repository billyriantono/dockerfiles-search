# Python crontab sample

FROM python:3.5.1

# add to application
RUN mkdir /app
WORKDIR /app
ADD requirements.txt /app/

RUN pip install -r requirements.txt
RUN pip install --upgrade google-api-python-client
RUN pip install --user  --upgrade google-cloud
RUN pip install google-cloud-storage
RUN pip install google-cloud-vision
COPY 'credential.json' .
ENV GOOGLE_APPLICATION_CREDENTIALS='credential.json'
ENV aws_access_key_id='AKIAR443ERLQK3XT2TVS'
ENV aws_secret_access_key='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'
ENV mongodb='mongodb://rcorazzi:Acesso123@ds137760.mlab.com:37760/sifra_invoices'

RUN pip install -U --force-reinstall bottom
RUN pip install -U python-dotenv
RUN pip install gevent
ADD *.py /app/


CMD ["python", "batch.py"]