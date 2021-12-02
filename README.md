# Basic blog site
### Created with Django, GraphQL and Vue

Django blog back end to administer, persist, and serve the data. Graphene to create the GraphQL API and Apollo to query the API. Vue front end to consume and display the data. 

There is no styling on this project, it was just created to:
- Build the Django data model and admin interface
- Wrap the data model in a GraphQL API using Graphene-Django
- Create and route to separate Vue components for each view of the data
- Query the GraphQL API dynamically to populate the Vue components using Apollo

---

# Backend 

## Installation

Use the package manager [pip](https://pip.pypa.io/en/stable/) to install the required environment.

```bash
pip install -r requirements.txt
```

The admin logins are:
- username: tompain
- password: Hello123 

---

## Running the programme

To start the application:

```bash
$ python manage.py runserver
```

---

## Django Project Components

The Django project contains two apps, the main backend app along with the blog app. 

---

# Frontend

## Project setup
```
npm install
```

## Compiles and hot-reloads for development
```
npm run serve
```

---

# Running the site

You must have the Django application running at http://localhost:8000 and the Vue application running at http://localhost:8080.

django-cors-headers is used for cross-origin resource sharing (CORS).
