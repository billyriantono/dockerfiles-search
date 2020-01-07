FROM chifleytech/spark:latest

#NCVR data (not enabled)
COPY ncvr-upload-data.sh /root/ncvr/ncvr-upload-data.sh
COPY create-table-ncvr.sql /root/ncvr/create_table_ncvr.sql

#SHOPPING CART data
COPY shopping-cart-upload-data.sh /root/upload-data/shopping_cart.sh
COPY create-tables-shopping.sql /root/create_tables.sql
RUN mkdir /data-init
COPY data/shopping/ /data-init/shopping/
COPY er-spark.jar /root/existing-udfs/er-spark.jar