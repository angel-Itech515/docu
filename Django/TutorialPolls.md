# Init App
```bash
pip install django
python -m django --version

django-admin startproject mysite .
python manage.py runserver

python manage.py startapp polls
```

# Migrate models

**python manage.py migrate**

The [`migrate`](https://docs.djangoproject.com/en/5.2/ref/django-admin/#django-admin-migrate) command looks at the [`INSTALLED_APPS`](https://docs.djangoproject.com/en/5.2/ref/settings/#std-setting-INSTALLED_APPS) setting and creates any necessary database tables according to the database settings in your `mysite/settings.py` file and the database migrations shipped with the app (we’ll cover those later). You’ll see a message for each migration it applies. If you’re interested, run the command-line client for your database and type `\dt` (PostgreSQL), `SHOW TABLES;` (MariaDB, MySQL), `.tables` (SQLite), or `SELECT TABLE_NAME FROM USER_TABLES;` (Oracle) to display the tables Django created.

**python manage.py sqlmigrate polls 0001**

--------------------------------
**python manage.py migrate**

The [`migrate`](https://docs.djangoproject.com/en/5.2/ref/django-admin/#django-admin-migrate) command takes all the migrations that haven’t been applied (Django tracks which ones are applied using a special table in your database called `django_migrations`) and runs them against your database - essentially, synchronizing the changes you made to your models with the schema in the database.

Migrations are very powerful and let you change your models over time, as you develop your project, without the need to delete your database or tables and make new ones - it specializes in upgrading your database live, without losing data. We’ll cover them in more depth in a later part of the tutorial, but for now, remember the three-step guide to making model changes:

- Change your models (in `models.py`).
    
- Run [`python manage.py makemigrations`](https://docs.djangoproject.com/en/5.2/ref/django-admin/#django-admin-makemigrations) to create migrations for those changes
    
- Run [`python manage.py migrate`](https://docs.djangoproject.com/en/5.2/ref/django-admin/#django-admin-migrate) to apply those changes to the database.
    

The reason that there are separate commands to make and apply migrations is because you’ll commit migrations to your version control system and ship them with your app; they not only make your development easier, they’re also usable by other developers and in production.

Read the [django-admin documentation](https://docs.djangoproject.com/en/5.2/ref/django-admin/) for full information on what the `manage.py` utility can do.

