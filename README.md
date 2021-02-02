# Logistic_Regression_logger_timer jupiter Notebook via Binder 

Dieses Repository enthält eine:
<ul>
  <li> Die von conda verwendete Standardkonfigurationsdatei'environment.yml', die eine Python umgebung installiert</li>
  <li> Jupyter Notebook mit der Musterlösung  'Logistische Regression Musterloesung.ipynb'</li>
  <li> Daten für die Ausführung des Projektse 'advertising.csv' </li>
 </ul>
 
<b>Plattform:</b>\
Für die reproduktion des Projekts im Bereich Logistic Regression wird die Plattform myBinder <a href = "https://mybinder.org">https://mybinder.org/</a> verwendet.
 
 <b>Quelle:</b>\
Die Übungsaufgabe, Musterlösunge und die Daten stammen aus dem Udemy- Kurs <a href = "https://www.udemy.com/course/python-data-science-machine-learning/learn/lecture/7758116#overview">"Phython für Data Science, Maschinelles Lernen & Visualization"</a>.
  
<b>Begleitende Literatur:</b>\
<a href = http://faculty.marshall.usc.edu/gareth-james/ISL/ISLR%20Seventh%20Printing.pdf>"Introduction to Statistical Learning" von Gareth James</a>

# Binder Badge Logistische Regression_logger_timer

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/katjanein91/Logistic-Regression.git/master?filepath=Logistische%20Regression%20Musterloesung.ipynb)

Durch das Anklicken des blauen badge oben oder über folgende URL erhälst man Zugriff zu Binder um die Musterlösung auszuführen:
<a href = "https://mybinder.org/v2/gh/katjanein91/Logistic-Regression.git/master?filepath=Logistische%20Regression%20Musterloesung.ipynb"> Logistische Regression Musterloesung </a>

Das Jupiter Notebook mit der Musterlösung wird im Browser geöffnet.\
Wähle unter dem Reiter 'Cell' --> 'Run All' aus um den Python Code auszuführen.\
Das erwartete Ergebnis zu den jeweiligen Aufgaben wird in der Output Zelle angezeigt.
Darüber Hinaus wird die Ausführungszeit für bestimmte Funktionen protokolliert, indem wir @mylogger & @my_timer zu jeder Funktion hinzufügen, die wir  protokollieren und deren Laufzeit kennen wollen. Dazu müsssen die notwendigen Wrapper Timer und Logger folgendermaßen eingerichtet werden:
 
```
# Decorators
from functools import wraps


def my_logger(orig_func):
    import logging
    logging.basicConfig(filename='{}.log'.format(orig_func.__name__), level=logging.INFO)

    @wraps(orig_func)
    def wrapper(*args, **kwargs):
        logging.info(
            'Ran with args: {}, and kwargs: {}'.format(args, kwargs))
        return orig_func(*args, **kwargs)

    return wrapper


def my_timer(orig_func):
    import time

    @wraps(orig_func)
    def wrapper(*args, **kwargs):
        t1 = time.time()
        result = orig_func(*args, **kwargs)
        t2 = time.time() - t1
        print('{} ran in: {} sec'.format(orig_func.__name__, t2))
        return result

    return wrapper
    ```
    
 Die Wrapper werden wiefolgt verwendet:
 
 #### TBD
 
Die Logger-Datei kann nur offline angesehen werden und im Falle von Fehlern kann der Code entsprechend gedebuggd werden. 
