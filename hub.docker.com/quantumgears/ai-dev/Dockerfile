FROM quantumgears/ai-dev:flask-ai-code-v2

ENV BASE_DIR  "/root/flask/ai-prod/quanta"

COPY ./embed* $BASE_DIR/gensim-data/
COPY ./sentm* $BASE_DIR/gensim-data/

WORKDIR $BASE_DIR
EXPOSE 8080

ENV NLTK_DATA $BASE_DIR/nlp/nltk_data
CMD ["python", "quanta_main.py"]
