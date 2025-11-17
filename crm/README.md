📘 CRM System – Django + Celery + Redis + GraphQL

A production-ready CRM system built with Django, GraphQL (Graphene), Celery for asynchronous tasks, Redis as a message broker, and scheduled task automation.

🚀 Features

Django-based CRM backend

GraphQL API using Graphene

Celery background workers

Celery Beat for scheduled reports

Redis for task brokering

Daily CRM activity reporting

Admin dashboard

Customer & Lead management module

📦 Tech Stack
Component	Technology
Backend	Django 5+
API	GraphQL (Graphene-Django)
Task Queue	Celery
Message Broker	Redis
Database	SQLite/PostgreSQL/MySQL
Logging	Custom log handler (/tmp/crm_report_log.txt)
🛠 Installation & Setup

Follow the steps below to install and run the CRM project.

1️⃣ Clone the repository
git clone <repo-url>
cd crm

2️⃣ Create and activate virtual environment
python3 -m venv venv
source venv/bin/activate      # Mac/Linux
venv\Scripts\activate         # Windows

3️⃣ Install dependencies
pip install -r requirements.txt

4️⃣ Environment Variables

Copy .env.example into .env (if provided):

cp .env.example .env


Required variables (if not already in settings):

SECRET_KEY=your_secret_key
DEBUG=True
DATABASE_URL=sqlite:///db.sqlite3
REDIS_URL=redis://localhost:6379/0

5️⃣ Apply Migrations
python manage.py migrate

6️⃣ Create Superuser
python manage.py createsuperuser

7️⃣ Run the Django Development Server
python manage.py runserver


Your backend is now accessible at:

http://127.0.0.1:8000/

⚡ Celery & Celery Beat Setup
8️⃣ Start Redis
sudo apt install redis-server
sudo systemctl start redis


(Optional: enable on boot)

sudo systemctl enable redis

9️⃣ Start Celery Worker
celery -A crm worker -l info

🔟 Start Celery Beat Scheduler
celery -A crm beat -l info


This handles automated CRM tasks such as scheduled daily reporting.

🧪 Verify Task Logs

Celery logs daily CRM reports to:

cat /tmp/crm_report_log.txt

🧩 GraphQL API

Visit the GraphQL IDE:

http://127.0.0.1:8000/graphql/

Example Query:
{
  allCustomers {
    edges {
      node {
        id
        firstName
        lastName
        email
      }
    }
  }
}

📁 Project Structure
crm/
│── crm/                   # Django project config
│── crm_app/               # CRM application (models, tasks, schema)
│── schema/                # GraphQL schema (optional)
│── manage.py
│── requirements.txt
│── README.md
│── venv/

🧰 Common Commands
Action	Command
Start Django server	python manage.py runserver
Run Celery worker	celery -A crm worker -l info
Run Celery beat	celery -A crm beat -l info
View logs	cat /tmp/crm_report_log.txt
Create migrations	python manage.py makemigrations
Apply migrations	python manage.py migrate
🐞 Troubleshooting
Redis not running?
sudo systemctl status redis
sudo systemctl restart redis

Celery worker not receiving tasks?

Check Redis host/port in settings

Ensure Celery worker + beat are both running

Check logs for errors

GraphQL errors?

Ensure graphene_django is installed

Ensure schema is correctly linked in urls.py