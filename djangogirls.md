# Djangogirls Tutorial für Python und Django

- [Djangogirls Tutorial für Python und Django](#djangogirls-tutorial-für-python-und-django)
  - [Virtuelle Umgebung](#virtuelle-umgebung)
  - [Django Installation](#django-installation)
  - [Das erste Django Projekt - ein Blog](#das-erste-django-projekt---ein-blog)
  - [Webserver starten](#webserver-starten)
  - [Django-Models](#django-models)
    - [Django-Model erstellen](#django-model-erstellen)
    - [Eine Applikation für den Blog](#eine-applikation-für-den-blog)
    - [Tabellen für Models in deiner Datenbank erstellen](#tabellen-für-models-in-deiner-datenbank-erstellen)
  - [Django-Administration](#django-administration)
  - [Veröffentlichen](#veröffentlichen)
    - [Git](#git)
      - [Git-Repository](#git-repository)
  
## Virtuelle Umgebung
- Im Projektverzeichnis erstellen: python -m venv myvenv
- im Projektverzeichnis starten: **myvenv\Scripts\activate**  z.B. in der PowerShell von VS Code  ==> (myvenv)

## Django Installation
- zuerst pip aktualisieren: python -m pip install --upgrade pip
- Pakete mittels requirements-Datei installieren ==> requirements.txt erstellen
- in die Datei requirements.txt eintragen: Django~=3.1.4
- Installation starten mit: pip install -r requirements.txt oder python -m pip install -r requirements.txt

## Das erste Django Projekt - ein Blog
- ALLES in der virtuellen Umgebung machen
- Projekt erstellen: django-admin.exe startproject mysite .  <== Punkt nicht vergessen für aktuelles Verzeichnis
- Einstellungen anpassen in Datei settings.py  z.B. import os, TIME_ZONE, LANGUAGE_CODE, ALLOWED_HOSTS, STATIC_ROOT, ...
- im Projektverzeichnis eingeben: python manage.py migrate

## Webserver starten
(myvenv) **python manage.py runserver**


## Django-Models
- objektorientiertes Programmieren - Objekte und Vorlagen (Klassen)
- Objekt: Sammlung von Eigenschaften und Aktionsmöglichkeiten, das anhand einer Vorlage (Klasse) erstellt wird
- z.B. für den Blog - Post: title, text, author, created_date, published_date + veröffentlichen-Methode
- Der Gedanke dahinter ist, echte Dinge mit Hilfe von Eigenschaften (genannt Objekteigenschaften) und Aktionsmöglichkeiten (genannt Methoden) im Programmcode zu beschreiben.

### Django-Model erstellen
- ein "Modell" wird als Objekt in der Datenbank gespeichert wie eine Tabelle mit Spalten (Feldern) und Zeilen

### Eine Applikation für den Blog
- erstellen im Projektverzeichnis: python manage.py startapp blog
- Django mitteilen, diese Applikation zu benutzen: in Datei mysite/settings-py bei INSTALLED_APPS eintragen: 'blog.apps.BlogConfig',
- alle "Models" der Applikation werden in der blog/models.py Datei definiert
- Klassennamen immer mit einem Großbuchstaben beginnen
- Methoden beginnen mit Kleinbuchstaben und anstatt Leerzeichen Unterstrich verwenden

### Tabellen für Models in deiner Datenbank erstellen
- python manage.py makemigrations blog  ==> Migrationsdatei vorbereiten 
- python manage.py migrate blog  ==> auf die Datenbank anwenden


## Django-Administration
- Admin-Seite http://127.0.0.1:8000/admin/
- Super User erstellen: (myvenv) python manage.py createsuperuser   z.B. wkrass  wkrass@live.de
- Django-Admin-Dashboard in der Django-Dokumentation: https://docs.djangoproject.com/en/2.2/ref/contrib/admin/


## Veröffentlichen
- Deployen bedeutet, dass du deine Anwendung im Internet veröffentlichst.
- z.B. auf [PythonAnywhere](https://www.pythonanywhere.com/)

### Git
- Download von https://git-scm.com/

#### Git-Repository

Die Initialisierung des Git-Repositorys muss für jedes Projekt nur einmal gemacht werden
- git init
- git config --global user.name "wkrass"
- git config --global user.email wkrass@live.de

Git wird die Änderungen an all den Dateien und Ordnern in diesem Verzeichnis aufzeichnen. 
Wir wollen aber, dass einige Dateien ignoriert werden. Dazu legen wir eine Datei **.gitignore** im Hauptordner (djangogirls) des Repos an.

Es ist hilfreich den Befehl **git status** vor **git add** auszuführen oder immer dann, wenn du dir unsicher bist, was geändert wurde.
Das schützt vor manchen Überraschungen, wie z. B. das falsche Hinzufügen oder Übertragen von Dateien.