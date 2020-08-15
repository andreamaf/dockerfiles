FROM python:slim
RUN set -eux; \
        apt-get update; \
        apt-get install -y --no-install-recommends vim gcc g++
COPY requirements.txt .
RUN pip install -r requirements.txt
