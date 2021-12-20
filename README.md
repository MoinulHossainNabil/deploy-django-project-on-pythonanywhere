# Deploy Django Application on Pythonanywhere

The markup demonstrates how to deploy any django application on pythonanywhere in the simplest way.

# Dummy Project Structure

Take following example as the normal flow of a django application throughout the process:
        
        proj/
            __init__.py
            settings.py
            asgi.py
            urls.py
            wsgi.py
        app1/
            __init__.py
            admin.py
            apps.py
            models.py
            tests.py
            urls.py
            views.py
        templates/
        static/
        manage.py
        
Assumed it as a boilerplate to follow along with the article. The sturcture might be slightly or completely different. There is nothing wrong with that. But the most important part to focus on is the **settings.py** file inside the **proj/** directory.

Modify some configuration that is okay when we are in development but the production structure of a django project is too way different that we normally follow while playing with some simple applications in development. This is not about production standard architecture it is just for when you want you simple application go live without any kind of extra hassle and spending a lot of time to configure things manually for ages.

# Modifying settings.py

First of all make the following changes in the **proj/settings.py** file.

    DEBUG = False
    ALLOWED_HOSTS = ['localhost', '127.0.0.1', 'yourusername.pythonanywhere.com', ]

Now add the **STATIC_ROOT** if you have not set it yet
    
    STATIC_ROOT = BASE_DIR / 'staticfiles'
    
**NB: STATIC_ROOT must be a directory that does not already exist in the STATICFILES_DIRS if you have**

Now if you have a virtual environment activate it first. Then freeze all of the packages used in the application by running the following command.

    pip freeze > requirements.txt
    
# Git

That is all from the project changes. Now, first of all, create an empty public repository in your github account to avoid hassles. Then push the codebase to the repository you just created by following the below procedures sequentially (skip the step if you have already the code in github repo set as public by following minimal django standard)

    git init
    touch .gitignore
    
Add ignorable files in the .gitignore. You may use this [.gitignore content](https://djangowaves.com/tips-tricks/gitignore-for-a-django-project/) for common files and directories.

    git add .
    git config user.name "yourgithubusername"
    git config user.email "yourgithubemail"
    git commit -m "commit message"
    git branch -M main
    git remote add origin https://github.com/yourgithubusername/repository_name.git
    git push -u origin main
    
# Pythonanywhere

Now login to your pythonanywhere account. Go to the **Account** and from **Api Token** tab create a new api token if you already don't have any. Now get back to **Dashboard** and open a new **$ Bash**  console. And install the following pakage.

    pip3.8 install --user pythonanywhere
    
    
3.8 is the python version. You should use your required and desired version. After successfully installing the package run the following command.

    pa_autoconfigure_django.py --python=3.8 github_repository_url
    
Mention the version in --python=3.8 that you used when installing the pythonanywhere pakage above. This package is a shortcut to automate the deployment process on pythonanywhere machine. When you run the above command you might see the follwoing actions performed automatically.

+ Downloading your code from GitHub
+ Creating a virtualenv on PythonAnywhere, just like the one on your own computer
+ Updating your settings file with some deployment settings
+ Setting up a database on PythonAnywhere using the manage.py migrate command
+ Setting up your static files
+ And configuring PythonAnywhere to serve your web app via its API

Now keep patient it might take a few while to complete the process and if everything goes as expected then you are on live.

# You are on live

Now if the process is complete then you app is on live. go to **yourusername.pythonanywhere.com**. to check your app..
            
