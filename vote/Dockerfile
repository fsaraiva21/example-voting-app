FROM python:3.9-slim

EXPOSE 80

# Add curl for healthcheck and apache2-utils for seeding script
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    apache2-utils \
    curl \
    && rm -rf /var/lib/apt/lists/*

# Set the application directory
WORKDIR /app

# Install packages from list in requirements.txt
COPY requirements.txt /app/requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# Copy code from the current folder to /app inside the container
COPY . .

# Define launch command using gunicorn to set up web server
CMD ["gunicorn", "app:app", "-b", "0.0.0.0:80", "--log-file", "-", "--access-logfile", "-", "--workers", "4", "--keep-alive", "0"]