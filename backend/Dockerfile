FROM python:3.12-slim

ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1

WORKDIR /app

RUN useradd -m appuser

COPY --chown=appuser:appuser app.py /app/app.py

USER appuser

EXPOSE 8080
CMD ["python", "app.py"]