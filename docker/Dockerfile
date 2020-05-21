FROM postgres:latest

# ENV POSTGRES_HOST_AUTH_METHOD trust
# in the docker initialization, we do not build the data
ENV BUILD_MIMIC 0
ENV POSTGRES_PASSWORD postgres
ENV MIMIC_PASSWORD mimic

RUN mkdir -p /mimic_data /mimic-code

COPY data/ /mimic_data

COPY postgres/ /mimic-code/
COPY docker/setup.sh /docker-entrypoint-initdb.d/
