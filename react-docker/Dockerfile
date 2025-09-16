# Use Node.js 20 on a lightweight Alpine Linux base image
FROM node:20-alpine

# Create a new group 'app' and a system user 'ash' in that group
RUN addgroup ash && adduser -S -G app ash

# Switch to the non-root user 'app' for better security
USER ash

# Set working directory inside container to /app
WORKDIR /app

# Copy only package.json and package-lock.json for installing dependencies
COPY package*.json ./

# Switch back to root temporarily to change ownership of /app
USER root
# Change ownership of all files in /app to user 'ash' and group 'app'
RUN chown -R ash:app .
# Switch back to non-root user
USER ash

# Install Node.js dependencies as user 'app'
RUN npm install

# Copy the rest of the application source code into /app
COPY . .

# Expose port 5173 (for example, Vite dev server)
EXPOSE 5173

# Default command to run when container starts
CMD npm run dev
