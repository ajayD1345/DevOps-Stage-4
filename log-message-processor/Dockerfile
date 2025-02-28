# Use an official lightweight Python image
FROM python:3.10-slim

# Set working directory
WORKDIR /app

# Copy requirement files
COPY requirements.txt .

# Install dependencies
RUN pip3 install --no-cache-dir -r requirements.txt

# Copy rest of the files
COPY . .

# Expose port 8000
EXPOSE 8000

# Run the log-message-processor application
CMD ["python3", "main.py"]
