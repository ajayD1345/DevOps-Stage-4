# Use an official lightweight Python image
FROM python:2.7-slim

# Set working directory
WORKDIR /app

# Install system dependencies and upgrade pip
RUN apt-get update && apt-get install -y --no-install-recommends \
    gcc python3-dev libffi-dev \
    && rm -rf /var/lib/apt/lists/* 

# Copy and install dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy the rest of the application files
COPY . .

# Create a non-root user and switch to it
RUN addgroup --system appgroup && adduser --system --group appuser \
    && chown -R appuser:appgroup /app
USER appuser

# Expose port 8000
EXPOSE 8000

# Run the log-message-processor application
CMD ["python3", "main.py"]
