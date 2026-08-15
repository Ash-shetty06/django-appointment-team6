# Django Appointment Comprehension

A standalone salon appointment system based on the open-source
**django-appointment** project by Adams Pierre David.

This repository is intended for learning how to explore, understand, model,
debug, and modify an existing software system.

The application has been configured as a simple salon appointment system that
can be explored from three perspectives:

- **Customer** — browse services and book appointments
- **Salon staff/provider** — view and manage appointments
- **Salon manager** — administer the system

You do not need to understand the code before running the system. Start by
using it and observing its behaviour.

---

## 1. Requirements

You need:

- Git
- Python 3
- A web browser
- A code editor such as VS Code

Check that Python is installed:

```bash
python3 --version
```

### `python3` or `python`?

This guide uses `python3`.

On some computers, particularly Windows, Python 3 may instead be available as:

```bash
python --version
```

If `python3` does not work but `python` reports Python 3, replace `python3`
with `python` in the commands below.

---

## 2. Clone the repository

```bash
git clone https://github.com/mjpalash/django-appointment-comprehension.git
cd django-appointment-comprehension
```

---

## 3. Create a virtual environment

Create a Python virtual environment:

```bash
python3 -m venv .venv
```

Then activate it.

### macOS / Linux

```bash
source .venv/bin/activate
```

### Windows PowerShell

```powershell
.venv\Scripts\Activate.ps1
```

Once activated, your terminal will normally show something like:

```text
(.venv)
```

at the beginning of the prompt.

---

## 4. Install dependencies

```bash
python3 -m pip install -r requirements.txt
```

Using `python3 -m pip` rather than simply `pip` helps ensure that packages
are installed for the Python interpreter being used by this project.

---

## 5. Create the local database

Run the existing database migrations:

```bash
python3 manage.py migrate
```

This creates the local SQLite database and the tables required by the
application.

---

## 6. Load the demo salon

Run:

```bash
python3 manage.py load_salon
```

This loads the demo configuration from:

```text
demo_data/salon.json
```

It creates the salon services, staff members, working hours, and local
accounts used to explore the application.

You should see output indicating that the salon configuration was loaded and
the services and staff members were created.

The command can safely be run again. Existing demo records will be updated
rather than unnecessarily duplicated.

---

## 7. Start the application

```bash
python3 manage.py runserver
```

Django should display an address similar to:

```text
http://127.0.0.1:8000/
```

Open this address in your browser.

To stop the server, return to the terminal and press:

```text
Ctrl+C
```

### If port 8000 is already in use

Another program may already be using Django's default port.

You can start the application on another port instead:

```bash
python3 manage.py runserver 8001
```

Then open:

```text
http://127.0.0.1:8001/
```

If you use another port, substitute that port wherever this guide refers to
`8000`.

---

# Exploring the System

The system can be explored from three different user perspectives.

## Customer

Open:

```text
http://127.0.0.1:8000/
```

From here you can browse salon services and make an appointment.

Try completing an appointment from beginning to end and observe the different
steps involved.

---

## Salon Staff / Provider

Open:

```text
http://127.0.0.1:8000/staff/login/
```

One demo staff account is:

```text
Username: riya
Password: salon123
```

After logging in, you can access the staff appointment calendar and other
staff-facing functionality.

Other demo staff accounts are defined in:

```text
demo_data/salon.json
```

---

## Salon Manager

Open Django's administration interface:

```text
http://127.0.0.1:8000/admin/
```

Use:

```text
Username: salonadmin
Password: admin123
```

The manager account has administrative access to the local demo system.

These are deliberately simple **local classroom demo credentials**. They must
not be used for a real deployed system.

---

# Personalize Your Salon

The demo salon configuration is stored in:

```text
demo_data/salon.json
```

You are encouraged to explore this file and personalize your local version of
the system.

For example, you can experiment with changing:

- salon name
- tagline
- colors
- service names
- service descriptions
- prices
- staff names
- services offered by each staff member
- working days and hours

Some presentation changes, such as the salon name or colors, can be visible
after refreshing the page.

For database-backed information such as services and staff, run:

```bash
python3 manage.py load_salon
```

again after changing `salon.json`.

---

# Useful Django Commands

Check the project for configuration problems:

```bash
python3 manage.py check
```

Apply database migrations:

```bash
python3 manage.py migrate
```

Reload the salon demo configuration:

```bash
python3 manage.py load_salon
```

Start the development server:

```bash
python3 manage.py runserver
```

---

# Repository Structure

You do not need to understand the entire repository before beginning.

Some useful places to explore are:

```text
django-appointment-comprehension/
│
├── appointment/              Main appointment application
│   ├── models.py             Application data/domain models
│   ├── views.py              Customer-facing behaviour
│   ├── views_admin.py        Staff/admin behaviour
│   ├── forms.py              Forms and validation
│   ├── urls.py               Appointment URL routes
│   ├── templates/            Appointment UI templates
│   ├── management/           Custom Django commands
│   └── migrations/           Database schema history
│
├── config/                   Django project configuration
│   ├── settings.py
│   ├── urls.py
│   └── views.py
│
├── demo_data/
│   └── salon.json            Editable demo salon configuration
│
├── templates/
│   ├── home.html             Salon homepage
│   └── staff_login.html      Staff login page
│
├── manage.py                 Django command-line entry point
└── requirements.txt          Python dependencies
```

A useful way to begin is:

1. Run the system.
2. Use it as different users.
3. Observe its behaviour.
4. Form questions about how that behaviour is produced.
5. Use the code, documentation, models, database, and experiments to answer
   those questions.

---

# Troubleshooting

## `python3` command not found

Try:

```bash
python --version
```

If this reports Python 3, use `python` instead of `python3` throughout the
setup instructions.

---

## Port already in use

If:

```bash
python3 manage.py runserver
```

reports that port 8000 is already in use, choose another port:

```bash
python3 manage.py runserver 8001
```

---

## Database/table errors

Make sure you have run:

```bash
python3 manage.py migrate
```

before:

```bash
python3 manage.py load_salon
```

The first command creates the database structure. The second loads the demo
salon data into that structure.

---

## Changes to `salon.json` are not appearing

For changes to services, staff, prices, working hours, or other database-backed
information, run:

```bash
python3 manage.py load_salon
```

again and refresh the application.

---

# Upstream Project

This repository is a teaching-oriented fork of **django-appointment**, created
by Adams Pierre David.

The original project provides the appointment scheduling system. This fork
adds a small standalone salon scenario, demo configuration, local accounts,
and setup intended to make the system convenient to explore in a
software-comprehension setting.

The appointment application code originates from the upstream project and
remains subject to its original license.

The original upstream README has been preserved at:

```text
docs/upstream/README.md
```

The original license is retained in this repository.

For deeper information about the underlying appointment application, consult
the upstream documentation and source code.