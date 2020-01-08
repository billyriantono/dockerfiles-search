# 公式 Python ランタイムを親イメージとして使用
FROM python:3.4.1

# /app ディレクトリを作成
RUN mkdir /app

# 作業ディレクトリを /app に設定
WORKDIR /app

# 現在のディレクトリの内容を、コンテナ内の /app にコピー
ADD . /app

# requirements.txt で指定された必要なパッケージを全てインストール
RUN pip install -r requirements.txt

# ポート 5000 番をコンテナの外の世界でも利用可能に
EXPOSE 5000

# 環境変数の定義
ENV NAME World

# コンテナ起動時に app.py を実行
CMD ["python", "/app/main.py"]