# Dockerfile for the FastAPI + Qiskit backend service
FROM python:3.13-slim

ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1
WORKDIR /app

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        build-essential \
        git \
        ca-certificates \
        libblas-dev \
        liblapack-dev \
        libopenblas-dev \
        libgomp1 \
    && rm -rf /var/lib/apt/lists/*

COPY pyproject.toml /app/

RUN python -m pip install --upgrade pip setuptools wheel
RUN python -m pip install --no-cache-dir \
    fastapi>=0.136.3 \
    qiskit>=2.4.1 \
    qiskit-aer>=0.17.2 \
    uvicorn[standard]

COPY qiskit_api.py /app/

EXPOSE 8000
CMD ["uvicorn", "qiskit_api:app", "--host", "0.0.0.0", "--port", "8000"]
