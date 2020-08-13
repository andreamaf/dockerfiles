FROM python:slim
RUN set -eux; \
        apt-get update; \
        apt-get install -y --no-install-recommends vim gcc
COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt
