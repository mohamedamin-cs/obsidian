- django-admin startproject pyshop .
- python3 manage.py runserver
- pyhton3 manage.py makemigration → for database

| **Step** | **Action**           | **Command**                        | **Result**                                      |
| -------- | -------------------- | ---------------------------------- | ----------------------------------------------- |
| **1**    | **Change Models**    | Edit `models.py`                   | Python code is updated.                         |
| **2**    | **Create Migration** | `python3 manage.py makemigrations` | A new `.py` file is generated in `/migrations`. |
| **3**    | **Apply Migration**  | `python3 manage.py migrate`        | Your database schema is updated.                |

- python3 manage.py createsuperuser
_______________

vscode :
pipenv install django
pipenv shell

> python interpreter ---> pipenv --env
### first project
- add django app to setting.py
- change database to mysql => engine, user, password, host, port
- USER : aarfi || PASSWORD : password123 || PORT : 3306