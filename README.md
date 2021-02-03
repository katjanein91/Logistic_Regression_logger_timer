# Logistic_Regression_UnitTest_Logging jupiter Notebook via Binder 

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

# Binder Badge Logistische Regression_Logging

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/katjanein91/Logistic-Regression.git/master?filepath=Logistische%20Regression%20Musterloesung.ipynb)

Durch das Anklicken des blauen badge oben oder über folgende URL erhälst man Zugriff zu Binder um die Musterlösung auszuführen:
<a href = "https://mybinder.org/v2/gh/katjanein91/Logistic-Regression.git/master?filepath=Logistische%20Regression%20Musterloesung.ipynb"> Logistische Regression Musterloesung </a>

Das Jupiter Notebook mit der Musterlösung wird im Browser geöffnet.\
Wähle unter dem Reiter 'Cell' --> 'Run All' aus um den Python Code auszuführen.\
Das erwartete Ergebnis zu den jeweiligen Aufgaben wird in der Output Zelle angezeigt.
Darüber Hinaus wird die Ausführungszeit für bestimmte Funktionen protokolliert, indem wir @mylogger & @my_timer zu jeder Funktion hinzufügen, die wir  protokollieren und deren Laufzeit kennen wollen. Dazu müsssen die notwendigen Wrapper Timer und Logger folgendermaßen eingerichtet werden:
 
```python 
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
    
 Die Wrapper werden wiefolgt für folgende zwei Funktionen verwendet:
 
 ```python
@my_logger
@my_timer
def logmodelFit():
    return logmodel.fit(X_train,y_train)
logmodelFit()
```
Eine Log-Datei "logmodelFit.log" wird ereugt, kann aber nur offline angesehen werden und im Falle von Fehlern kann der Code entsprechend gedebuggt werden.

```python
@my_logger
@my_timer
def logmodelPredict():
    return logmodel.predict(X_test)
predictions = logmodelPredict()
```
Bei der Ausführung des Notebooks wird die Laufzeit angezeigt. Für das obige Beispiel erhält man folgenden Output: "logmodelPredict ran in: 0.0019986629486083984 sec"

# Logistische Regression_UnitTest

Zwei Testfälle werden implementiert:

<ul>
  <li> Testfall 1: Prüfung ob der Vorhersagewert predict() es Modells korrekt funktioniert </li>
   Für Testdall 1 stehen zwei unterschiedliche Testdaten zur Verfügung: "unittest_data_OK.txt" und "unittest_data_N-OK.txt".
   Im Notebook wird das erste File ausgefüht. Der Test ist erfolgreich. Das der Testfall 1 muss fehlschlagen wenn das zweite File eingelesen wird.
   Dazu muss im Notebook an nachfolgender Stelle "unittest_data_OK.txt" durch "unittest_data_N-OK.txt" ersetzt werden.
  
  ```python
   with open("unittest_data_OK.txt", 'r') as f:
            content = f.read()
  ```
  
  <li> Testfall 2: Prüfung der Laufzeit der Trainingsfunktion fit(). Die Laufzeit der Trainingsfunktion überschreitet während der Testfallausführung den Grenwert von 120% der representativen Laufzeit nicht.<li>
  Die representative Laufzeit ist: 
  ![alt text](https://github.com/katjanein91/Logistic_Regression_logger_timer/blob/main/representative_laufzeit.PNG)
 Der Grenzwert 120% der representativen Laufzeit wird sowie die Laufzeit der Trainingsfunktion fit() wird ausgegen.
<ul>
  





