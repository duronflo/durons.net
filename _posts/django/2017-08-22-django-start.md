---
title: Erste Schritte mit dem Webframework Django
permalink: /technology/django/first-steps-django
categories: [Web-Development]
tags: [Python, Web]
technology: django
---

![](/assets/images/django-image.png)

## Philosophiefrage: Projekt vs. App ?

Hier kann man wieder sensieren anfangen und keine plausible Definition finden. Bei Django ist das mega simple formuliert. App ist eine Web-Applikation, wie ein Blog-System oder ein Umfrage-App.

Ein Projekt ist eine Sammlung von Apps. Wie man ein Projekt anlegt findet man hier.

Erzeugen einer App innerhalb eines Projekts. Wir legen hier mal eine App, die eine einfache Umfrage darstellt.

	python manage.py startapp polls

## Datenbank Integration und die Model Erzeugung (MVC-Konzept)
Django folgt ebenfalls dem Model-View-Controller (MVC) Konzept und man muss im Prinzip ein model anlegen, welches einem 
Objekt in der Datenbank entspricht.  Hier eine Vorgehensweise wie das MVC im Django umgesetzt ist. Man entwirft seine 
Datenstruktur im Endeffekt im Model und migrierte diese dann automatisch in die Datenbank. Über simple Shell-Befehle 
spielen wir dann bisschen mit der fertigen Datenbank, legen neue Objekte an und löschen dieses. Zustätzlich sind auch 
einfach Filterabfrage aufgeführt. Der Vorteil an diesem Konzept ist man kann seine Modelstruktur im Projektverlauf 
stetig verändern kann, man migriert diese einfach neu in die Datenbank. Wie mächtig das Ganze ist werden wir noch sehen.

### Schritte zum Anlegen eines Models:

Erzeugen eines Models (in models.py im polls-Ordner). Hier eine Frage und eine Antwort, die direkt in Relation stehen (1-n).
Beispiel:

	from __future__ import unicode_literals

	from django.db import models


	class Question(models.Model):
	    question_text = models.CharField(max_length=200)
	    pub_date = models.DateTimeField('date published')


	class Choice(models.Model):
	    question = models.ForeignKey(Question, on_delete=models.CASCADE)
	    choice_text = models.CharField(max_length=200)
	    votes = models.IntegerField(default=0)
	
	python manage.py makemigrations # erzeugt die notwendigen Migrationsschritte für die Integration bzw. Migration
	python manage.py migrate # führt die Migration durch

Nachdem wir das Model erfolgreich in die Datenbank erzeugt haben, spielen wir ein bisschen mit der Datenbank-API herum, dem Controller im MVC-Konzept.


	>>from polls.models import Question, Choice   # Import the model classes we just wrote.

	# No questions are in the system yet.
	>>> Question.objects.all()
	[]

	# Create a new Question.
	# Support for time zones is enabled in the default settings file, so
	# Django expects a datetime with tzinfo for pub_date. Use timezone.now()
	# instead of datetime.datetime.now() and it will do the right thing.
	>>> from django.utils import timezone
	>>> q = Question(question_text="What's new?", pub_date=timezone.now())

	# Save the object into the database. You have to call save() explicitly.
	>>> q.save()

	# Now it has an ID. Note that this might say "1L" instead of "1", depending
	# on which database you're using. That's no biggie; it just means your
	# database backend prefers to return integers as Python long integer
	# objects.
	>>> q.id
	1

	# Access model field values via Python attributes.
	>>> q.question_text
	"What's new?"
	>>> q.pub_date
	datetime.datetime(2012, 2, 26, 13, 0, 0, 775217, tzinfo=<UTC>)

	# Change values by changing the attributes, then calling save().
	>>> q.question_text = "What's up?"
	>>> q.save()

	# objects.all() displays all the questions in the database.
	>>> Question.objects.all()
	[<Question: Question object>]

Mehr Datenbank-Queries und sonstige Zugriffe findet man in der offiziellen Doku.

### Die automatisch erzeugte Admin-Page
 
Django nimmt den Nutzer das Erzeugen einer Admin-Seite ab. Beispielsweise kann so sehr einfach eine Seite erzeugt werden zum hinzufügen von Content. Mit dieser Art und Weise wird die Erzeugung von Daten bzw. Inhalten komplett getrennt von der Darstellungsweise. Für Projekte im frühen Stadium ist das optimal um neue Datenbankeinträge sehr einfach hinzufügen zu können.

#### Erste Schritt, man legt einen Superuser/Adminuser an:

	$ python manage.py createsuperuser
	Um das Question-Objekt hinzufügen müssen wir es dem Admin-Interface bekannt machen.   


Das geschieht wie folgt:

	from .models import Question
	admin.site.register(Question)
	
	
Installation basiert auf der Quick Install Guide von Djangoproject. Empfohlene Entwicklungsumgebung (Einrichtung)
## Installation von Pyhton

Pyhton muss installiert werden. Laut Installationsanleitung wird mindestens die Version 3.4 gefordert, allerdings soll die 2.7 auch funktionieren. Die Python Version 2.7 ist noch gäniger daher werde ich mit dieser fortfahren. Außerdem ist sie bereits vorinstalliert bei Mint, man muss also nichts tun.

## Installation von Django

Es gibt mehrere Möglichkeiten das Django Paket zu installieren, einerseits über den Paketdienst apt oder aber auch über den Python-eignen Paketdienst namens PIP. Ich habe mich für die gängige Methode mit PIP entschieden, da diese die aktuellere Version von Django enthält.
Installation von PIP

Als erstes muss PIP (via get-pip.py) heruntergeladen werden:

PIP Download

Und mit folgendem Befehl installiert werden:

	$ sudo python get-pip.py

## Installation und Einrichten von virtualenv

Virtualenv ist Tool um eine isolierte Python-Umgebung zu schaffen. Man macht das um Versionkonflikte von Pyhton-Module zu vermeiden. Oft entwickelt man Tools wo einfach bestimmte Versionen einzelner Module notwendig sind, mit Hilfe von virtualenv kann man sich eine solche autarke Umgebung schaffen.

	sudo pip install virtualenv

Anlegen einer virtuellen Umgebung in einem beliebigen Ordner, bspw. im  /home-Verzeichnis:

	$ virtualenv django-env

Aktivierung/Deaktivierung der Umgebung im entsprechenden Verzeichnis:

	# Aktivieren
	$ source django-env/bin/activate

	# Deaktivieren
	$ deactivate

Installation von Django in der isolierten virtuellen Umgebung:

	(django-env) pip install Django

Anlegen eines Django Projekts:
 

	django-admin startproject mysite

Übersicht der erzeugten Dateien (Auszug aus djangoproject.com):

	mysite/
	    manage.py
	    mysite/
	        __init__.py
	        settings.py
	        urls.py
	        wsgi.py

Information von der Django Mainpage

* The outer mysite/ root directory is just a container for your project. Its name doesn’t matter to Django; you can rename it to anything you like.
* manage.py: A command-line utility that lets you interact with this Django project in various ways. You can read all the details about manage.py in django-admin and manage.py.
* The inner mysite/ directory is the actual Python package for your project. Its name is the Python package name you’ll need to use to import anything inside it (e.g. mysite.urls).
* mysite/__init__.py: An empty file that tells Python that this directory should be considered a Python package. If you’re a Python beginner, read more about packages in the official Python docs.
* mysite/settings.py: Settings/configuration for this Django project. Django settings will tell you all about how settings work.
* mysite/urls.py: The URL declarations for this Django project; a “table of contents” of your Django-powered site. You can read more about URLs in URL dispatcher.
* mysite/wsgi.py: An entry-point for WSGI-compatible web servers to serve your project. See How to deploy with WSGI for more details.

Starten des Django Development Servers (nicht für Server im Produktionsmodus)

	python manage.py runserver

Der Server ist nun online auf dem lokalen PC. Und kann im Broswer unter http://localhost:8000 angesehen werden.