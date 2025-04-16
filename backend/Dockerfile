# Base Image
FROM python:3.11

# Set the working directory in the container
WORKDIR /app

# Install Node.js and npm
RUN apt-get update && apt-get install --no-install-recommends -y \
    nodejs \
    npm \
    curl \
    && rm -rf /var/lib/apt/lists/*

# Create a non root user and group
# RUN addgroup -S appgroup && adduser -S appuser -G appgroup

# Install poetry using pip
RUN curl -sSL https://install.python-poetry.org | python3 - 
    # && ln -s /root/.local/bin/poetry /usr/local/bin/poetry
# RUN pip3 install --no-cache-dir poetry

# Add Poetry to PATH
ENV PATH="/root/.local/bin:$PATH"

# Copy the rest of the application files
COPY . /app

# Change ownership of the application files to the non root user
# RUN chown -R appuser:appgroup /app

# Install dependencies as root before switching
# RUN poetry config virtualenvs.create false && poetry install --no-interaction --no-ansi

# Install dependencies
RUN poetry install 

# Switch to the non root user
# USER appuser

# Make sure the prestart script is executable
RUN chmod +x ./prestart.sh

# Expose the port the app runs on
EXPOSE 8000

# Run the prestart script and start the server
# CMD ["bash", "./prestart.sh"]
CMD ["sh", "-c", "poetry run bash ./prestart.sh && poetry run uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload"]
