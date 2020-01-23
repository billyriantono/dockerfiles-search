FROM  circleci/python:3.6.4

RUN   sudo apt-get update \
      && sudo apt-get install locales-all -y

RUN   wget -qO - https://www.mongodb.org/static/pgp/server-3.4.asc | sudo apt-key add - \
      && echo "deb http://repo.mongodb.org/apt/debian jessie/mongodb-org/3.4 main" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list \
      && sudo apt-get update && sudo apt-get install mongodb-org-tools -y
