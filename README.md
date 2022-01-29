# Django OAuth Google and FaceBook Authentication
This is a sample project to explore social (Google) OAuth 2.0 authentication integration with Django using [`django-allauth`](https://django-allauth.readthedocs.io/en/latest/index.html).

### 1. Set up your Django project

create a virtual environment (highly recommended):
- To **create** virtual environment:
    ```Shell
    $ virtualenv env_name # using virtualenv
    ``` 
- To **activate** virtual environment (Linux/Mac OS):
    ```Shell
    $ source env_name/bin/activate
    ``` 
Install development dependencies,

    pip install -r requirements.txt

Apply migrations

    python manage.py migrate

Create a SuperUser

    python manage.py createsuperuser

Run the Web Application locally

    python manage.py runserver

## Configuring Google APIs

To add Google login on your app, you’ll need to set up OAuth application via [**Google Developers Console**](https://console.developers.google.com/).


### 1. Create New Google APIs project

Head over to Google Developer APIs Console and create a new project:

- Go to ***Dashboard, create a New Project***
- Name your new project, preferably your website or app name. User will be able to see this project name when we redirect them to Google login page.
- Click ***'Create'*** to proceed.

### 2. Register App at OAuth Consent Screen

Next, register your app by filling the OAuth consent screen. You only need to provide 'App name', 'User support email' and 'Email addresses' under 'Developer contact information. Click 'Save and Continue' button.

### 3. Create New API Credentials

Back to 'Dashboard', go to 'Credentials' on left panel and click 'Create Credentials' button at the top. On the dropdown, choose 'OAuth Client ID' option.

Under ***'Authorized JavaScript origins'***, add the following URIs:

    http://localhost:8000
    http://127.0.0.1:8000

Under ***Authorized redirect URIs***

    http://127.0.0.1:8000/accounts/google/login/callback/
    http://localhost:8000/accounts/google/login/callback/

You will get ***Client ID*** and ***Client Secret***copy these details to input in Djngo admin or can be given inputed in ***settings.py*** file


## Configuring Facebook OAuth

To add Facebook login on your app, you’ll need to set up OAuth application via [**Facebook Developer App**](https://developers.facebook.com/apps).

### 1.Create New App

- Press Create App  and Select App Type as ***'Consumer'*** or ***None*** 
- Enter *** Display Name *** and press create App (it may promt for password)
- In the list of Apps press Setup ***Facebook Login*** and select ***Web*** 
- In site url input ***http://localhost:8000***
- Goto settings > Basic copy ***App ID*** and ***App secret*** save changes


Head over to ***http://localhost:8000/admin*** 

### 1.Add Site

- Click Add a site from Sites Option
- Fill in the below details
- Domain name: `localhost:8000`
- Display name: `localhost`

- [Note]: There is a possiblity that Django will insert ***example.com*** delete this
- If you get any errors In settings.py change from `SITE_ID=1` to `SITE_ID=2` or 3 (This is not needed if you gave configurations in settings.py in `SOCIALACCOUNT_PROVIDERS`)

- Select ***Social Applications*** and click Add Social Application select provider as Google or Facebook
- Fill the deatils
- Clientid: `<App ID or Client ID>`
- Secret Key: `<API secret, client secret, or consumer secret>`
- Sites as `localhost:8000`