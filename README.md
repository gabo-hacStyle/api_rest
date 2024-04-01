## Installation Process

### 1. **Create a virtual environment**  
   This is for python packages (you may use venv for example). If you don´t wanna use virtual env, just skip this step.
      
   ``python -m  venv backend``


Replace 'backend' with your folder name.

  **NOTE: Right now I suggest you to continue with the rest of the installation process from your IDE because venv uses the current CLI you are working in to create the environment, if you kill the CLI, you kill the virtual environment.**
  
  So do something like this (if using vscode):
  
  ` cd backend `
  
  `code .`
  
Activate the environment
    
    source Scripts/activate
    
### 2. Install django and start a project

  ``pip install django``
  
**If you need to upgrade pip, I suggest you you do it to avoid any inconvenience in installing packages (pip will give you the command to upgrade itself if needed)**

Start the django project called 'api':

``django-admin startproject api``
  
  ``cd api/``
  
  ``python manage.py migrate``
  
  ``python manage.py runserver``

 
  With this commands you will be able to run the django project. Go to your browser to localhost:8000 and see the rocket, you did it!😎🚀
  
  But that´s not all, not even have we started...

Create a superuser to access the dashboard later

  ``python manage.py createsuperuser ``

  And follow the instructions.

### 3. Install *this* project (the real api_rest with CRUD methods)
  ``git clone https://github.com/gabo-hacStyle/api_rest.git
    cd api_rest
    pip install -r requirements.txt
  ``
  By doing that, you are installing all dependencies needed for the project, wait some seconds.
  Then, you need to remove the migrations folder
  ``rm -r migrations/``
  In the settings.py file within your api/ folder, make sure that you have within the INSTALLED_APPS this apps:
    > 'api_rest'
    > 
    > 'rest_framework'
    >
    > 'corsheaders'
    >
    > 'rest_framework_simplejwt'

  Go to the root of your django project in the terminal and run the migrations to start in your local, the db of the api_rest models.
    ``cd ..
      python manage.py makemigrations api_rest
      python manage.py migrate
    ``
### 4. Modify files to make the app work properly:
In the urls.py file in the api/ folder add the url of the api_rest. So erase all the code and copy/paste this:
  ``
  from django.contrib import admin
  from django.urls import path, include
  urlpatterns = [
      path('admin/', admin.site.urls),
      path('', include(('api_rest.urls', 'api_rest'), namespace='api_rest')),
  ]
  ``
### 5. See the results
Finally , run the server again (in the root of your django project)
> python manage.py runserver
And go to your browser to localhost:8000/users, there you go, you see the crud options from the dashboard


### 6. Consuming this API:
   If you wanna consume this api from your app, you need to set the cors settings correctly, so go to setting.py in the api/ folder and copy/paste this:
``
CORS_ALLOWED_ORIGINS = [
    "http://localhost:5173",
]
``




















    
