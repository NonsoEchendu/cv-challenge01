# Use python3.11-slim as base image
FROM python:3.11-slim

# set working directory
WORKDIR /app

# Install system dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential curl \
    && rm -rf /var/lib/apt/lists/*

#Install Poetry
RUN curl -sSL https://install.python-poetry.org | python3 -
ENV PATH="/root/.local/bin:$PATH"

# Copy the Poetry files
COPY pyproject.toml poetry.lock ./

# Install Python dependencies using Poetry
RUN poetry config virtualenvs.create false \
    && poetry install --no-interaction --no-ansi --only main

# Copy the application code
COPY . .

# Make the prestart script executable
RUN chmod +x /app/prestart.sh

# Expose the FastAPI default port (8000)
EXPOSE 8000

# Run the prestart script and start the application
CMD ["bash", "-c", "./prestart.sh && uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload"]