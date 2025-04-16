# Base Image
FROM node:23.11.0

# Set the working directory
WORKDIR /app

# Copy the application files
COPY . .

# Install dependencies
RUN npm install

# Expose the port the app runs on
EXPOSE 5173

# Start Nginx
CMD ["npm", "run", "dev", "--", "--host", "0.0.0.0"]
