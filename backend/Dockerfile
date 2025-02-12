# Build stage
# Base Image
FROM python:3.13-alpine3.20 AS builder

# Install poetry using pip
RUN pip install poetry

# Set the working directory
WORKDIR /app

# Copy the rest of the application files
COPY . .

# Production stage
FROM python:3.13-alpine3.20

# Set working directory
WORKDIR /app/api

# Copy necessary files from build stage
COPY --from=builder /app /app

# Create a non root user and group
RUN addgroup -S appgroup && adduser -S appuser -G appgroup

# Change ownership of the application files to the non root user
RUN chown -R appuser:appgroup /app

# Switch to the non root user
USER appuser

# Install dependency using Poetry
RUN poetry install

# Expose the port the app runs on
EXPOSE 8000

# Run the prestart script and start the server
CMD ["sh", "-c", "poetry run bash ./prestart.sh && poetry run uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload"]
