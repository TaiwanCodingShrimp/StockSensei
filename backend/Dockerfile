# Use an official Python3.12 runtime as a parent image
FROM python:3.12

# Install system dependencies
RUN apt-get update \
    #can add the required system dependency here !
	&& rm -rf /var/lib/apt/lists/*

# Install Poetry
RUN pip install poetry

# Set the working directory
WORKDIR /backend

# Copy pyproject.toml and poetry.lock for dependency management
COPY ./pyproject.toml ./poetry.lock* ./

# Skip install packages listed in the [tool.poetry.dev-dependencies] 
RUN poetry config virtualenvs.create false \
	&&poetry install --no-dev --no-interaction --no-ansi

#Copy the backend codes to the working directory
COPY ./src /backend/

# This is not required
# Run database migrations during the build process (optional, but useful for CI/CD if we applied later)
# RUN python manage.py migrate

#Expose Port 8000:
EXPOSE 8000

HEALTHCHECK --interval=30s --timeout=5s --start-period=10s --start-interval=1s --retries=3 \
CMD curl --fail http://localhost:8000/health/ || exit 1

# For development we will use Django's built-in server for temporary,so we mark this one for now
# Use Gunicorn to serve Django in production (replace with manage.py for dev)
# CMD ["gunicorn", "--bind", "0.0.0.0:8000", "app.wsgi:application"]


# Use Django's built-in development server for development
CMD ["python", "/backend/src/manage.py", "runserver", "0.0.0.0:8000"]

