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
      - [Initialisierung](#initialisierung)
      - [Dateien ignorieren - .gitignore](#dateien-ignorieren---gitignore)
      - [Was wurde geändert?](#was-wurde-geändert)
      - [Änderungen speichern](#änderungen-speichern)
    - [Code auf GitHub veröffentlichen](#code-auf-github-veröffentlichen)
      - [Repository erstellen](#repository-erstellen)
      - [Git-Repository auf meinem Computer mit dem auf GitHub verbinden](#git-repository-auf-meinem-computer-mit-dem-auf-github-verbinden)
    - [Blog auf PythonAnywhere einrichten](#blog-auf-pythonanywhere-einrichten)
      - [Code von GitHub herunterladen und PythonAnyhwere dazu bringen, diesen zu erkennen und als Web Applikation anzubieten](#code-von-github-herunterladen-und-pythonanyhwere-dazu-bringen-diesen-zu-erkennen-und-als-web-applikation-anzubieten)
  - [Django-URLs](#django-urls)
  - [Django-Views](#django-views)
  - [Django-Template](#django-template)
  
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

### Git-Repository

#### Initialisierung
Die Initialisierung des Git-Repositorys muss für jedes Projekt nur einmal gemacht werden
- git init
- git config --global user.name "wkrass"
- git config --global user.email wkrass@live.de

#### Dateien ignorieren - .gitignore
Git wird die Änderungen an all den Dateien und Ordnern in diesem Verzeichnis aufzeichnen. 
Wir wollen aber, dass einige Dateien ignoriert werden. Dazu legen wir eine Datei **.gitignore** im Hauptordner (djangogirls) des Repos an.

#### Was wurde geändert?
Es ist hilfreich den Befehl **git status** vor **git add** auszuführen oder immer dann, wenn du dir unsicher bist, was geändert wurde.
Das schützt vor manchen Überraschungen, wie z. B. das falsche Hinzufügen oder Übertragen von Dateien.

#### Änderungen speichern
- git add --all .
- git commit -m "My Django Girls app, first commit"

### Code auf GitHub veröffentlichen

#### Repository erstellen
- auf https://www.github.com/ ein neues Repository erstellen "my-first-blog"
- https://github.com/wkrass/my-first-blog.git

#### Git-Repository auf meinem Computer mit dem auf GitHub verbinden
- git remote add origin https://github.com/<your-github-username>/my-first-blog.git
- git push -u origin master


### Blog auf PythonAnywhere einrichten
- für ein PythonAnywhere Konto registrieren  ==> User wkrass mit E-Mail wkrass@live.de
- erstellen eines PythonAnywhere API-Tokens
- Bash Console aufrufen

#### Code von GitHub herunterladen und PythonAnyhwere dazu bringen, diesen zu erkennen und als Web Applikation anzubieten  
  $ pip3.6 install --user pythonanywhere  # Tool installieren (wird nur einmal gemacht)
  $ pa_autoconfigure_django.py --python=3.6 https://github.com/wkrass/my-first-blog.git
- den Code von GitHub herunterladen
- eine virtuelle Umgebung auf PythonAnywhere einrichten, genau wie die auf meinem eigenen Computer
- meine Einstellungen mit ein paar Veröffentlichungseinstellungen aktualisieren
- eine Datenbank auf PythonAnywhere einrichten mit dem Befehl manage.py migrate
- meine statischen Dateien einrichten
- PythonAnywhere so einrichten, dass es meine Web-App über seine Schnittstelle (API) präsentieren kann

Diese Schritte wurden auf PythonAnywhere automatisiert, aber es sind die selben Schritte, 
die bei jedem anderen Server-Provider gemacht werden müssen.

- [Django deployment checklist](https://docs.djangoproject.com/en/3.1/howto/deployment/checklist/) 
  nutzen!
- [Debugging Tipps](https://tutorial.djangogirls.org/de/deploy/#debugging-tipps)


Die Datenbank auf PythonAnywhere ist vollständig unabhängig von meiner Datenbank auf meinem eigenen PC, daher
- ( ... ) $ python manage.py createsuperuser  ==> wkrass, wkrass@live.de

>Für Änderungen auf dem **lokalen Setup** arbeiten. So wird in der Web-Entwicklung gearbeitet - Änderungen lokal machen und diese dann auf GitHub veröffentlichen und dann die Änderungen auf den produktiven Webserver ziehen. So kannst du Sachen ausprobieren, ohne deine produktive Website kaputt zu machen.

## Django-URLs
- mysite/urls.py Datei
- 'http://127.0.0.1:8000/' soll die Homepage des Blogs werden und eine Liste der Posts zeigen  ==> blog/urls.py
- Django-URL-Resolver ignoriert den Domain-Namen (z.B. http://127.0.0.1:8000/), der im vollständigen Pfad voransteht.
- blog/urls.py  ==> view  z.B. post_list

## Django-Views
- In der View schreiben wir die Logik unserer Anwendung.
  So werden Informationen aus dem Model abgefragt werden, welches du zuvor erzeugt hast und diese werden an ein Template weitergeben.
- blog/views.py  ==> def post_list(request):    return render(request, 'blog/post_list.html', {})

## Django-Template
- wird in HTML beschrieben
- Templates werden z.B. im Verzeichnis blog/templates/blog gespeichert
- post_list.html