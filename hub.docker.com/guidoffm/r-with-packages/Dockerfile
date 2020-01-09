FROM r-base

#ENV http_proxy=http://prosim2100.bku.db.de:42424
#ENV https_proxy=http://prosim2100.bku.db.de:42424

RUN R -e 'install.packages(c("data.table", "randomForest", "caret", "lubridate"))'
#RUN R -e 'install.packages(c("awspack"))'
#RUN R -e 'install.packages("aws.s3", repos = c("cloudyr" = "http://cloudyr.github.io/drat"))'
