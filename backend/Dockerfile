# ---------- STAGE 1: Build ----------
FROM python:3.12-slim AS builder

WORKDIR /app

# System dependencies
RUN apt-get update && apt-get install -y build-essential

# Copy requirement file
COPY requirements.txt .

# Install dependencies
RUN pip install --upgrade pip && \
    pip install --prefix=/install -r requirements.txt


# ---------- STAGE 2: Final Image ----------
FROM python:3.12-slim

WORKDIR /app

# Create non-root user
RUN useradd -m appuser

# Copy installed packages from builder
COPY --from=builder /install /usr/local

# Copy project code
COPY . .

# Give permission
RUN chown -R appuser:appuser /app

USER appuser

EXPOSE 8000

CMD ["gunicorn", "config.wsgi:application", "--bind", "0.0.0.0:8000"]
