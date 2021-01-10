# Djangogirls Tutorial für Python und Django
  
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

>Für Änderungen auf dem **lokalen Setup** arbeiten. So wird in der Web-Entwicklung gearbeitet - Änderungen lokal machen und diese dann auf GitHub veröffentlichen und dann die Änderungen auf den produktiven Webserver ziehen. 
>So kannst du Sachen ausprobieren, ohne deine produktive Website kaputt zu machen.

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
- <div></div> definiert einen Abschnitt auf einer Seite

## Deployment
### Commit und Push lokal
- commit und push auf GitHub
- Achtung: im lokalen Projektverzeichnis! z.B. C:\python\djangogirls
> $ git add --all .  # --all berücksichtigt auch gelöschte Dateien; 
  der . steht für das aktuelle Verzeichnis  
> $ git status  
> $ git commit -m "HTML der Site geändert."  
> $ git push  

### Neuen Code auf PythonAnywhere ziehen
- Öffne die PythonAnywhere consoles page und gehe zur Bash-Konsole (oder starte eine neue).
- cd ~/<deine-pythonanywhere-domain>.pythonanywhere.com
- git pull
- unter "Files" sieht man die Dateien
- unter "Web" Reload ausführen

## Django-ORM und QuerySets
- **ORM** = Object-Relational Mapping
- Ein **QuerySet** ist eine Liste von Objekten eines bestimmten Models. QuerySets erlauben es dir, Daten aus der Datenbank zu lesen, zu filtern und zu sortieren.

### Django-Shell
(myvenv) ~/djangogirls$ python manage.py shell  ==> Interaktive Django-Konsole
  > from blog.models import Post  
  > Post.objects.all() ==> alle Posts anzeigen  
  > Post.objects.create(author=me, title='Sample title', text='Test')

User-Objekt ermitteln und "me" zuweisen:  
- from django.contrib.auth.models import User
- User.objects.all()
- me = User.objects.get(username='wkrass')

Filtern
- Post.objects.filter(author=me) 
- Post.objects.filter(title__contains='title')  ==> 2 Unterstriche zw. title und contains  
  __ trennt Feldname und Operationen bzw. Filter

bereits publizierte Posts
- from django.utils import timezone
- Post.objects.filter(published_date__lte=timezone.now())

Post mit meiner publish-Methode publizieren
-  post = Post.objects.get(title="Sample title")  ==> Instanz des Posts holen
-  post.publish()  ==> mit der in models.py definierten Methode publizieren

Objekte ordnen
- Post.objects.order_by('created_date')  ==> aufsteigend
- Post.objects.order_by('-created_date') ==> absteigend

Komplexe Queries durch Methoden-Verkettung
- Post.objects.filter(published_date__lte=timezone.now()).order_by('published_date')

## Dynamische Daten in Templates
- Posts im HTML-Template erscheinen lassen mit Views (Verbindung zw. Model und Template)
- In einer View entscheiden wir, was (welches Model) wir in einem Template anzeigen werden.
- in blog\views.py hinzufügen
  ```
  from django.shortcuts import render  
  from django.utils import timezone  
  from .models import Post  
  
  def post_list(request):  
      posts = Post.objects.filter(published_date__lte=timezone.now()).order_by('published_date')
      return render(request, 'blog/post_list.html', {'posts': posts})
  ```
- Variable posts für das QuerySet
- 'posts': posts  ==> Name 'posts' für die Übergabe an das Template

## Django-Templates
- Die **Django-Template-Tags** erlauben uns, Python-artige Dinge ins HTML zu bringen, 
  so dass man einfach und schnell dynamische Websites erstellen kann.
- Variable in einem Django-Template: z.B. {{ posts }}

Liste mit for-Schleife anzeigen
```
{% for post in posts %}
    {{ post }}
{% endfor %}
```

### Alles auf PythonAnywhere ...

Zuerst Code auf GitHub schieben
```
$ git status
[...]
$ git add --all .
$ git status
[...]
$ git commit -m "Modified templates to display posts from database."
[...]
$ git push
```

dann Code von GitHub auf PythonAnywhere ziehen (in Bash-Console auf PythonAnywhere)
```
$ cd <deine-pythonanywhere-domain>.pythonanywhere.com
$ git pull
[...]
```
- unter "Web" neu laden

## CSS
Cascading Style Sheets (CSS) ist eine Sprache, die das Aussehen und die Formatierung einer Website beschreibt. Es handelt sich wie bei HTML um eine Auszeichnungssprache (Markup Language).

### Bootstrap
**Bootstrap** ist eines der bekanntesten HTML- und CSS-Frameworks für die Entwicklung von schönen Webseiten: https://getbootstrap.com/

Im <head>-Abschnitt der html-Datei einfügen
<link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css">
<link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap-theme.min.css">

### Statische Dateien in Django
Statische Dateien sind alle deine CSS- und Bilddateien. Ihr Inhalt hängt nicht vom Requestkontext ab, sondern gilt für alle Benutzer gleichermaßen.
==> Ordner static in der App erstellen  
Django findet automatisch alle Ordner mit dem Namen "static" in all unseren App-Ordnern. So ist es in der Lage, ihre Inhalte als statische Dateien zu nutzen.

### CSS-Datei
- Ordner CSS im Verzeichnis static erstellen und darin die Datei blog.css
- [CSS-Selektoren Anleitung](http://www.w3schools.com/cssref/css_selectors.asp)
- kostenlose Online-Kurse "Basic HTML & HTML5" und "Basic CSS" auf [freeCodeCamp](https://learn.freecodecamp.org/).