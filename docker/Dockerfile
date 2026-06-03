FROM liquibase/liquibase:latest

RUN lpm add mysql --global

WORKDIR /liquibase/changelog

COPY liquibase/ .
