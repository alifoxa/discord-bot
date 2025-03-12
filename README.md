# Unit Converter Application Documentation

This documentation provides an overview of the Unit Converter Application, outlining its components and describing how to start the application and access it via a web browser.

## Overview

The Unit Converter Application is a containerized solution that leverages Docker to orchestrate multiple services. It uses a Flask-based backend for conversion logic, a frontend built with HTML/CSS/JavaScript for user interaction, and an Nginx reverse proxy for efficient routing. The application relies on a PostgreSQL database for persistence and data management.

## Components

- **prepare-app.py**  
  This script sets up the environment by creating a dedicated Docker network and building the service images using `docker-compose build`.

- **start-app.py**  
  This script launches the application in detached mode using `docker-compose up -d` and automatically opens the default web browser to display the application.  
  **Access the Application:** [http://localhost](http://localhost)

- **end-app.py**  
  This script gracefully stops the application by shutting down all containers, removing the Docker network, pruning unused Docker volumes, and cleaning up images related to the project.

- **docker-compose.yml**  
  Defines the multi-container application services:
  - **postgres_db:** Hosts the PostgreSQL database required for data storage.
  - **backend:** Runs the Flask server that contains the conversion logic and communicates with the database.
  - **frontend:** Builds and serves the user interface. It includes the HTML, CSS, and JavaScript files that render the conversion interface.
  - **nginx:** Acts as a reverse proxy server by routing incoming web requests to the appropriate backend service.

- **backend/app.py**  
  Implements the conversion logic using Flask. This file connects to the PostgreSQL database, reads conversion data from a JSON file, and sets up API endpoints for the frontend to interact with.

- **Frontend Assets**  
  - **Dockerfile (in the frontend directory):** Builds the frontend application on top of the Nginx image.
  - **index.html, styles.css, script.js:** Provide the complete structure, styling, and functionality for the application’s user interface.

- **nginx/nginx.conf**  
  Configures the Nginx server to serve the static frontend content and act as a proxy for API requests to the backend.

## How to Run the Application

1. **Prepare the Application:**

   Run the preparation script to build the Docker images and set up the network:
   ```bash
   python prepare-app.py
   ```

2. **Start the Application:**

   Launch the application with:
   ```bash
   python start-app.py
   ```
   After starting, the application will automatically open in your default web browser. If it does not open automatically, navigate manually to: [http://localhost](http://localhost)

3. **Stop and Clean Up:**

   When you wish to stop the application, run:
   ```bash
   python end-app.py
   ```
   This will terminate the running containers, remove the Docker network, and clean up volumes and images associated with the application.
