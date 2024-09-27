FROM python:3.12.1-slim-bullseye
RUN apt-get update && apt-get install -y cron nano\
    apt-utils \
    && apt-get install -y cron nano \
    && rm -rf /var/lib/apt/lists/*

ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1
WORKDIR /djangoapp

COPY . /djangoapp

COPY entrypoint.sh ./scripts/entrypoint.sh

RUN chmod +x /djangoapp/scripts/entrypoint.sh

RUN pip install --no-cache-dir -r requirements.txt

ENTRYPOINT ["/djangoapp/scripts/entrypoint.sh"]
CMD ["gunicorn", "--bind", "0.0.0.0:8000", "core.wsgi:application"]