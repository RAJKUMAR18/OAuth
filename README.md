# OAuth

## Few tips:
 settings.py
 ```

     INSTALLED_APPS = [
        'PREDEFINED APPS',
        'CUSTOM APPS',

        'django.contrib.sites',

        'allauth',
        'allauth.account',
        'allauth.socialaccount',
        'allauth.socialaccount.providers.google',
        'allauth.socialaccount.providers.twitter',
        'allauth.socialaccount.providers.github',
    ]
     TEMPLATES = [
        {
            'BACKEND': 'django.template.backends.django.DjangoTemplates',
            'DIRS': [os.path.join(BASE_DIR, 'templates')],
            'APP_DIRS': True,
            'OPTIONS': {
                'context_processors': [
                    'django.template.context_processors.debug',
                    'django.template.context_processors.request',
                    'django.contrib.auth.context_processors.auth',
                    'django.contrib.messages.context_processors.messages',
                ],
            },
        },
    ]
    
    LOGIN_REDIRECT_URL = 'home'
    LOGOUT_REDIRECT_URL = 'home'


    AUTHENTICATION_BACKENDS = (
        "django.contrib.auth.backends.ModelBackend",
        "allauth.account.auth_backends.AuthenticationBackend",
    )

    SITE_ID = 1

    ACCOUNT_EMAIL_REQUIRED = True
    ACCOUNT_USERNAME_REQUIRED = False
 ```
 
 project/urls.py
 ```
    url(r'^accounts/', include('allauth.urls')),
 ```
 
 templates/home.html
 ```
    {% load socialaccount %}

    {% if user.is_authenticated %}
    <p>Welcome {{ user.username }} !!!</p>
    <p><a href="{% url 'account_logout' %}">Log out</a>
    {% else %}
    <p><a href="{% url 'account_signup' %}">Sign Up</a></p>
    <p><a href="{% url 'account_login' %}">Log In </a></p>
    <p><a href="{% provider_login_url 'google' %}">Log In with Gmail</a></p>
    <p><a href="{% provider_login_url 'twitter' %}">Log In with Twitter</a></p>
    <p><a href="{% provider_login_url 'github' %}">Log In with Github</a></p>

    {% endif %}

 ```
 
 ## Most important is the callback URL this causes a lot of trouble 
 ![Github Oauth app image](https://github.com/RAJKUMAR18/OAuth/blob/master/sample_images/social_auth_github.png)
 
 
 ![Twitter Oauth app image](https://github.com/RAJKUMAR18/OAuth/blob/master/sample_images/social_auth_twitter.png)
 
 
 
 ## In the localhost:8000/admin
 
 
 You should change the **Sites** Domain.
 
 
 ![Sites changes](https://github.com/RAJKUMAR18/OAuth/blob/master/sample_images/admin_sites.png)
 
 
 Register your twitter or github app in the **Social Applications**  with the keys provided to you 
 
 
 ![Social Applications Changes](https://github.com/RAJKUMAR18/OAuth/blob/master/sample_images/admin_social_app.png)
 
 ### Notes
 **It was very troublesome to get good guides as most of them are 2-3 years old and the technologies have changed.**
 **Twitter does not even porvide a guide for starter it took too much effort to join every piece together and finally built this.**
