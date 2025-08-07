# Docker Learning: Django + PostgreSQL Setup with Docker Compose

This project is a **beginner-friendly** example to learn how to containerize a **Django** application with **PostgreSQL** using **Docker** and **Docker Compose**.

---

## 📦 Project Structure

docker_learning/
├── docker_basic/ # Django app
├── docker_learning/ # Django project settings
├── manage.py
├── Dockerfile
├── docker-compose.yml
├── .env # Environment variables
├── .gitignore
└── README.md


---

## 🚀 What You'll Learn

- How to containerize a Django app using Docker.
- How to use PostgreSQL as your database inside a Docker container.
- How to manage multi-container apps with Docker Compose.
- How to keep secrets and configs in a `.env` file.
- How to persist database data using Docker volumes.

---

## 🧰 Prerequisites

Make sure the following are installed on your system:

- Python 3.8+
- Git
- Docker
- Docker Compose

---

## 🔧 Installation Steps

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/docker-learning.git
cd docker-learning

2. Create a .env File
Create a .env file in the project root directory:

DEBUG=1
DB_NAME=postgres
DB_USER=postgres
DB_PASSWORD=postgres
DB_HOST=db
DB_PORT=5432
📝 Make sure this file is listed in .gitignore.

🐳 Docker Setup
3. Create Dockerfile
Dockerfile

# Dockerfile
FROM python:3.10-slim

ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

WORKDIR /app

COPY requirements.txt .
RUN pip install --upgrade pip && pip install -r requirements.txt

COPY . .

CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
4. Create docker-compose.yml

version: "3.9"

services:
  web:
    build: .
    command: python manage.py runserver 0.0.0.0:8000
    volumes:
      - .:/app
    ports:
      - "8000:8000"
    depends_on:
      - db
    env_file:
      - .env

  db:
    image: postgres:15
    env_file:
      - .env
    volumes:
      - postgres_data:/var/lib/postgresql/data/

volumes:
  postgres_data:

🏁 Running the Project
5. Build and Run Containers

sudo docker compose up --build
Your Django app should now be running at:
📍 http://localhost:8000/

🛠️ Apply Migrations
Open another terminal and run:


sudo docker compose exec web python manage.py migrate
👀 Check It’s Working
Visit: http://localhost:8000
You should see the default Django welcome page.

🧹 Useful Commands
Task	                      Command
Run migrations	            docker compose exec web python manage.py migrate
Create superuser	          docker compose exec web python manage.py createsuperuser
Access web container shell	docker compose exec web sh
Stop containers	            docker compose down
View running containers	    docker ps

📦 .gitignore
Here’s a sample .gitignore for your project:

gitignore

__pycache__/
*.pyc
*.pyo
*.pyd
*.sqlite3
.env
*.log
db.sqlite3
/static/
media/
.vscode/
.env.*

✅ Tips
Keep your secrets (passwords, keys) in .env and never commit them to Git.

🤝 Contributing
Pull requests are welcome. For major changes, open an issue first to discuss what you’d like to change.


🙋‍♂️ Author
Himanshu Aggarwal
Backend Developer | Docker & Django Learner

