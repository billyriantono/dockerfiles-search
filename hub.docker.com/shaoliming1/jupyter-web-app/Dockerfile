FROM gcr.io/kubeflow-images-public/jupyter-web-app:v0.5.0
RUN apt-get -qq update && apt-get install -y sed && \
sed -i "s/https\:\/\/ajax\.googleapis\.com\/ajax\/libs\/jquery\/3.3.1\/jquery\.min.js/http\:\/\/code\.jquery\.com\/jquery\-3\.3\.1\.min\.js/" /app/kubeflow_jupyter/rok/templates/layout.html && \
sed -i "s/https\:\/\/ajax\.googleapis\.com\/ajax\/libs\/jquery\/3.3.1\/jquery\.min.js/http\:\/\/code\.jquery\.com\/jquery\-3\.3\.1\.min\.js/" /app/kubeflow_jupyter/default/templates/layout.html
