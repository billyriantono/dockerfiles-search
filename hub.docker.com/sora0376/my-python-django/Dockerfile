FROM python:3.7-alpine3.9

# ワーキングディレクトリを変数定義
ARG project_dir=/web/app/

# Dockerコンテナに実行ディレクトリ下のファイルを追加する
ADD app $project_dir

WORKDIR $project_dir
RUN apk add git openssl-dev build-base libffi-dev
RUN pip install -r requirements.txt

EXPOSE 8000

ENTRYPOINT python manage.py runserver ${IP}:${PORT}