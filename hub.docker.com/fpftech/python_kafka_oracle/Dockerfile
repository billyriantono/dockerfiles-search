FROM fpftech/python_oracle:1.0.1-postgres
LABEL maintainer="portela.eng@gmail.com"

ADD requirements.txt ${APP_FOLDER}/
RUN pip3 install --no-cache-dir -r ${APP_FOLDER}/requirements.txt
