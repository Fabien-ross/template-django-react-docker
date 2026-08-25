# Python (Django) and React — Development Environment in Docker

A minimal and reusable full-stack web development template using **Django** for the backend, **React** for the frontend, **PostgreSQL** as the database, and **Docker** for the development environment.

The goal of this repository is to provide a clean starting point for new web projects without having to manually configure the development environment each time.

**Clone it, start the containers, and start coding.**

> **Development template only:** this project is intended for local development. It does **not** include a production setup, reverse proxy, HTTPS configuration, or production application server.

---

## Table of Contents

1. [Technologies](#technologies)
2. [Prerequisites](#prerequisites)
3. [Installation and Setup](#installation-and-setup)
4. [Project Structure](#project-structure)
5. [Docker & Dev Container](#docker--dev-container)
6. [Development Workflow](#development-workflow)
7. [Testing the Backend / Frontend Connection](#testing-the-backend--frontend-connection)
8. [Customization](#customization)
9. [License](#license)

---

## Technologies

This template combines a few standard technologies into a ready-to-use development environment.

### Backend

* **Python**
* **Django** — web framework used to build the backend and API.
* Django's built-in **development server** is used to run the backend locally.

### Frontend

* **React** — library used to build the user interface.
* **Vite** — development server and build tool for the React application.

### Database

* **PostgreSQL** — relational database used by Django.

### Development Environment

* **Docker** — isolates the different parts of the application into containers.
* **Docker Compose** — orchestrates the backend, frontend, and database services.
* **VS Code Dev Containers** — provides a consistent development environment directly inside VS Code.

---

## Prerequisites

You will need the following tools installed on your machine:

* [Docker](https://www.docker.com/get-started)
* [Docker Compose](https://docs.docker.com/compose/)
* [VS Code](https://code.visualstudio.com/)
* The **Dev Containers** extension for VS Code

The project was originally developed using **WSL2** on Windows, but the template should also work in other environments as long as Docker and Docker Compose are properly configured.

You do **not** need to install Python, Node.js, or PostgreSQL directly on your host machine. They are provided through the development containers.

---

## Installation and Setup

### 1. Clone the repository

Clone the repository and move into the project directory:

```bash
git clone https://github.com/Fabien-ross/python-react-dev-project.git
cd python-react-dev-project
```

If you are using this repository as a template for another project, you can rename the directory as desired.

It is advised to add .env into the gitignore file right after cloning to avoid a later leaking of the secrets on github and to create a mock .env.example file (for example) to understand the structure of the .env file. However, always keep the .env so that the django superuser and the database configuration credentials are forwarded during the building of the devcontainer.

---

### 2. Open the project in VS Code

Open the project folder in VS Code.

If the **Dev Containers** extension is installed, VS Code should detect the `.devcontainer` configuration and suggest reopening the project inside the container.

You can also do it manually:

**Ctrl + Shift + P** → **Dev Containers: Reopen in Container**

Once reopened, VS Code will use the configuration provided by `.devcontainer/devcontainer.json`.

This gives you a development environment containing the tools and dependencies required by the project without having to configure them individually on your host machine.

---

### 3. Apply Django migrations

The template contains a minimal Django model (`MyModel`) as an example.

If you want to create the corresponding database table in the PostgreSQL database, run:

```bash
cd backend
python manage.py migrate
```

The migration system can then be used normally as your project grows:

```bash
python manage.py makemigrations
python manage.py migrate
```

You are free to remove `MyModel` and replace it with your own models.

---

### 4. Access the application

Both development servers are running as soon as you've launched the dev container.

**Frontend**

```text
http://localhost:5173
```

**Backend**

```text
http://localhost:8000
```

The template already includes the necessary configuration for communication between the React frontend and Django backend during development.

---

## Project Structure

The project is intentionally kept small so that it can easily be adapted to different applications.

```text
project/
│
├── backend/                  # Django backend
│   ├── apps/                 # Django applications
│   │   └── ...
│   ├── config/               # Django project configuration
│   ├── manage.py
│   ├── Dockerfile            # Backend container
│   ├── requirements.txt      # Python dependencies
│   └── ...
│
├── frontend/                 # React frontend
│   ├── src/                  # React source code
│   ├── Dockerfile            # Frontend container
│   ├── package.json          # Node.js dependencies and scripts
│   └── ...
│
├── .devcontainer/
│   └── devcontainer.json     # VS Code Dev Container configuration
│
├── compose.yml               # Docker Compose configuration
└── README.md
```

### Backend

The `backend/` directory contains the Django project.

The `apps/` directory is intended to contain the Django applications of your project, while `config/` contains the main Django project configuration.

This separation makes it easy to add new Django apps as the project grows.

### Frontend

The `frontend/` directory contains the React application.

Vite is used as the development server and build tool. The source code is located in `frontend/src/`.

### Infrastructure

Docker-related configuration is kept outside the application code where possible.

The `.devcontainer/` directory contains the configuration used by VS Code to create the development environment.

---

## Docker & Dev Container

### Docker Compose

The `compose.yml` file defines the services required by the development environment.

The template contains three main services:

```text
backend   → Django development server
frontend  → React/Vite development server
db        → PostgreSQL database
```

Each service runs in its own container while Docker Compose manages their networking and configuration.

The frontend and backend can therefore communicate with the PostgreSQL database and with each other without requiring PostgreSQL, Python, or Node.js to be installed directly on the host.

### VS Code Dev Container

The `.devcontainer/devcontainer.json` file configures the VS Code development environment.

The Dev Container approach is particularly useful when using this repository as a template because the same development environment can be reproduced on another machine with minimal setup.

---

## Development Workflow

A typical development session can be reduced to the following steps:

### Develop the frontend

The Vite development server is already running through the frontend container.

Changes made to the React source code should be reflected automatically through Vite's development features.

### Develop the backend

Django's development server automatically reloads when Python source files are modified.

This allows both sides of the application to be developed independently while still communicating with each other.

---

## Testing the Backend / Frontend Connection

The template includes a minimal endpoint to demonstrate communication between the React frontend and Django backend.

Open:

```text
http://localhost:5173/test
```

This page displays a message returned by the Django backend.

This simple example is intended as a starting point for implementing your own API endpoints and frontend requests.

You can replace it with your own API structure as the project develops.

---

## Customization

This repository is intended to be used as a **starting template**, not as a complete application.

After cloning it, you can freely adapt:

* Django models and applications
* API endpoints
* React components and pages
* PostgreSQL schema
* Dependencies
* Docker configuration
* Environment variables
* Authentication
* Frontend styling
* Project-specific functionality

The existing Django model and test endpoint are intentionally minimal examples that can be removed or replaced.

The same applies to the React application: it provides a basic starting point rather than imposing a specific architecture.

### Suggested approach

For a new project, you can start by:

1. Removing the example `MyModel`.
2. Creating your own Django applications inside `backend/apps/`.
3. Defining your database models.
4. Creating the required API endpoints.
5. Replacing the example React pages/components.
6. Adding your own dependencies.
7. Adjusting the Docker configuration if required.

---

## Production

**Production deployment is intentionally outside the scope of this template.**

This repository is designed specifically as a **development environment**.

It does not provide:

* Gunicorn
* Nginx or any WEB server
* HTTPS configuration
* Production Docker configuration
* Production database configuration
* Static file serving configuration
* Production deployment scripts

For a real deployment, the development setup should be replaced or extended with an appropriate production architecture.

---

## License

The code in this repository is released under the **MIT License**.

You are free to use, modify, and redistribute the code according to the terms of the license.

See the [MIT License](https://opensource.org/licenses/MIT) for more information.
