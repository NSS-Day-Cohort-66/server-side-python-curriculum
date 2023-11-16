# Build Rare Professionally

In this sprint, you are going to be creating a new API for the Rare client side application to consume.

## Rare ERD from Database Team

https://dbdiagram.io/d/5f885a013a78976d7b77cb74

## Wireframes from Product Team

https://miro.com/app/board/o9J_kiGCSK4=/


## Sprint Process

**Step 1:** Read every ticket and give it a weight. Use the ERD and wireframes above as resources.

**Step 2:** Come to a team commitment for how many tickets you will complete in the sprint and communicate it to your Scrum Master _(an instructor)_.

**Step 3:** Each teammate will pull a ticket into the doing column and assign him/herself to it.

**Step 4:** Create branches and begin work. Create draft PRs ASAP and commit often.

## Setup

Accept the assignments as usual. One member follows the assignment links and creates the group name in each. The other members follow the links and join the created teams.

The client repo will have some boilerplate code in it to get you started.

The server side repo is a blank slate, ready for your elegant and advanced implementation of the API requirements written using the Django REST framework.

Next, choose one team member who will create the API project locally. As a team, walk through the creation of the Django application on that team member's computer. Open the [Level Up API Setup](./DRF_INSTALLS.md) chapter and follow those steps while in your rare directory. Make sure you do not use `levelup` for the project or application name. Use the following names instead.

### Creating the Project

```sh
django-admin startproject rare
```

### Creating the API Application

```sh
python3 manage.py startapp rareapi
```

### Creating the .gitignore

Once the project is set up, make sure you create a `.gitignore` file and put the content at [this URL](https://www.toptal.com/developers/gitignore/api/django) in there before your first commit. Finally, create a local git repo with `git init` and connect it to your team's server side github repo with `git remote add origin <github ssh url>`. Once you have everything setup, push up the code. The other team members can now clone down the new Django project repo.

### Ignoring migrations

Add the following pattern to the bottom of your gitignore file.

```txt
rareapi/migrations/**
```

### Issue Tickets

The requirements for this project are quite comprehensive. You will see many references to admin abilities. An admin is simply a user with more power. How do you give that power to a user? Update a user's `is_staff` property to `True`. Don't say we never gave you anything :)

## Checklist

Use this checklist to ensure that you have everything set up correctly before you make your first commit and PR.

- [ ] Django project created
- [ ] API application created
- [ ] Deleted `models.py` and `views.py`
- [ ] Created `.gitignore`
- [ ] Added `rareapi/migrations/**` to gitignore
- [ ] `.pylint` file created
- [ ] `.vscode/settings.json` file created with proper config settings
- [ ] `settings.py` updated with correct installed apps, CORS config, authentication/permission config, and middleware config
