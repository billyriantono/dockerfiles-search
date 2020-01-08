FROM postgres:latest

ENV POSTGRES_PASSWORD bb4life

ADD 01DBUSER.sql docker-entrypoint-initdb.d/01DBUSER.sql 
ADD 02tbl_team.sql docker-entrypoint-initdb.d/02tbl_team.sql
ADD teams.csv /home/teams.csv