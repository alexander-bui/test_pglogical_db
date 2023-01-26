FROM postgres:15.1

# Update and get pglogical package
RUN apt-get update && apt-get install -y curl
RUN curl https://dl.2ndquadrant.com/default/release/get/deb | bash && apt-get update

### IMPORTANT: use 2.4.2
RUN apt-get install -y -V postgresql-${PG_MAJOR}-pglogical