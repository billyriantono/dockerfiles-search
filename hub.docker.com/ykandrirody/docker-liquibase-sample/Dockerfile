FROM java:7
COPY . /app/
WORKDIR /app/

RUN chmod +x ./run_init_1.sh
RUN chmod +x ./run_init_2.sh
RUN chmod +x ./run_all_1.sh
RUN chmod +x ./run_all_2.sh

RUN javac Main.java
CMD ["java", "Main"]
