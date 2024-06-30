FROM python:3.12.4

LABEL maintainer="Andres Bermeo"

# Update system and install dependencies

# Set workdire
WORKDIR /opt/schedule/src

# Copy the variables in the container
COPY ./pyproject.toml ./poetry.lock* /tmp/

# Install the poetry dependencies
RUN cd /tmp \
    && python -m pip install --upgrade pip \
    && pip install -U gunicorn psutil poetry \
    && poetry export -f requirements.txt --output /opt/schedule/src/requirements.txt --without-hashes \
    && pip install --no-warn-script-location --disable-pip-version-check --no-cache-dir -r /opt/schedule/src/requirements.txt

# Copy project
COPY ./src /opt/schedule/src/

# Expose the port of the project
EXPOSE 8000

CMD [ "python", "manage.py", "runserver", "0.0.0.0:8000" ]


