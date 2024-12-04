# use python v3.11 as base image
FROM python:3.11

# set container working direct
WORKDIR /app/backend

# Update package list and install curl and bash
RUN apt-get update && apt-get install -y \
    curl \
    bash \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# install poetry
RUN curl -sSL https://install.python-poetry.org | python3 -

# add poetry to PATH
ENV PATH="/root/.local/bin:$PATH"

# copy application files
COPY . .

# install dependencies using poetry
RUN poetry install

# make prestart.sh executable
RUN chmod +x ./prestart.sh

# expose port app runs on
EXPOSE 8000

# run the prestart script and start server
CMD ["sh", "-c", "poetry run bash ./prestart.sh && poetry run uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload"]