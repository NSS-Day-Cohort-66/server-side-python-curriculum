# Installations and Configuration

1. Clone the repo
2. pipenv shell
3. pipenv install
4. Open in VS code and select interpreter
5. python3 manage.py migrate

## Setup

### Select Python Interpreter

Open VS Code and press <kbd>⌘</kbd><kbd>SHIFT</kbd><kbd>P</kbd> (Mac), or <kbd>Ctrl</kbd><kbd>SHIFT</kbd><kbd>P</kbd> (Windows) to open the Command Palette, and select "Python: Select Interpreter".

Find the option that has:

`honeyrae-<random string>`

## Create Base Django Tables

Django gives user and role management tables for your application out of the box, and there is a built-in migration file that makes the tables in a SQLite database for you. Go ahead and run that migration to set up the initial tables.

```sh
python3 manage.py migrate
```

