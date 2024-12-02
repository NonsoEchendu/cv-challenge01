FROM python:3.11

WORKDIR /app/backend

COPY poetry.lock pyproject.toml .

RUN pip install poetry && \
    poetry config virtualenvs.create false && \
    poetry install --no-root --no-dev

COPY . .

RUN pip install sqlalchemy sqlmodel alembic

RUN chmod +x /app/backend/prestart.sh

EXPOSE 8000

CMD ["sh", "-c", "./ prestart.sh && poetry run uvicorn app.main:app --host 0.0.0.0 --port 8000"]