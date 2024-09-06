# Use an official Python3.12 runtime as a parent image
FROM python:3.12-slim

# Set the working directory
WORKDIR /backend

# Install Poetry
RUN pip install poetry

# Copy pyproject.toml and poetry.lock for dependency management
COPY ./backend/pyproject.toml ./backend/poetry.lock* ./


