# Build stage
# Base Image
FROM node:20.18.1-alpine3.20 AS builder

# Set the working directory
WORKDIR /app

# Copy dependencies
COPY package.json package-lock.json ./

# Install dependencies
RUN npm install && npm cache clean --force

# Copy the rest of the application files
COPY . .

# Production stage
FROM node:20.18.1-alpine3.20

# Copy necessary files from build stage
COPY --from=builder /app /app

# Expose the port the app runs on
EXPOSE 5173

# Start Nginx
CMD ["npm", "run", "dev" "--", "--host"]
