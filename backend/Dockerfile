# Production-oriented image: layer-cached dependency install, non-root user,
# built-in health check. (A true multi-stage build would only help if we
# compiled native wheels; every dependency here ships a manylinux wheel.)
FROM python:3.12-slim

ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1

WORKDIR /app

# Dependencies first, so a code-only change reuses the cached layer.
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

# Run as an unprivileged user. /app/uploads is where uploaded files live
# (shared between the API and the worker through a volume).
RUN useradd --system --create-home app \
    && mkdir -p /app/uploads \
    && chown -R app:app /app
USER app

EXPOSE 8000

HEALTHCHECK --interval=30s --timeout=5s --start-period=30s --retries=3 \
  CMD python -c "import urllib.request; urllib.request.urlopen('http://localhost:8000/api/v1/health')" || exit 1

CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]
