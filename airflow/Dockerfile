FROM ghcr.io/astral-sh/uv:0.13.7@sha256:96f40d3904aad8d0bd010539001d36c8e2188b981e1334471a90c4a1d93bb490 AS uv

FROM apache/airflow:3.4.0-python3.11@sha256:be92e15d57c5be726fc39a91cd09cce8f7488483b67979e0fb74c1a2c7cfb4e2

USER root

COPY --from=uv /uv /usr/local/bin/uv
COPY dbt/requirements.txt /opt/dbt-requirements.txt

RUN uv venv /opt/dbt-venv --python /usr/local/bin/python \
    && uv pip install --python /opt/dbt-venv/bin/python --require-hashes --no-cache \
       -r /opt/dbt-requirements.txt \
    && chown -R airflow: /opt/dbt-venv

ENV DATAFORGE_DBT_BIN=/opt/dbt-venv/bin/dbt

USER airflow
