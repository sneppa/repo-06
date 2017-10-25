# Analyse Tomcat 

## Aufgabenstellung
Die Aufgage ist die grobe Architektur von Tomcat zu analysieren und zu dokumentieren. 
Durch die Dokumentation soll ein Überblick über den Quellcode von Tomcat erstellt werden.
Von besonderem Interesse ist das Zusammenspiel der Paketstruktur und der Klassen, um die Aufgaben und die Bereiche des Servers aufzuzeigen.

## Vorgehensweise
Über die import Statements ist es möglich die Zusammengehörigkeit der Klassen zu analysieren. Mit Hilfe der Script-Befehle -grep und -sed wurden die Quelltexte gefiltert. 
Klassen wie z. B. jUnit-Tests, die nicht den Ablauf des Programms beeinflussen, können hierbei direkt ausgefiltert werden.

grep = Mit grep lassen sich Dateien nach bestimmten Textstücken durchsuchen. Die Suchmuster werden "regular expressions" (auf Deutsch: regulärer Ausdruck) genannt.

sed = sed (von stream editor) ist ein nicht-interaktiver Texteditor für die Verwendung auf der Kommandozeile oder in Skripten

Erstellen der .dot Datei in /git/repo-06/Tomcat/java/org/apache
```
echo "digraph {" > test.dot ; grep -R "^import" * | sed -E "s/\//./g" | \
sed -E "s/\.java//g" | sed -E "s/\.\*//g" | sed -E "s/import //g" | \
grep -v ":java" | grep -v ":javax" | sed -E "s/;//g" | sed -E "s/:/ -> /" | \
grep -v "\.properties" | sed -E "s/\./_/g" | sed -E "s/_[A-Z].* ->/ ->/g" | \
sed -E "s/-> ([a-z_]*)_[A-Z][a-zA-Z]*/-> \1/g" | sed -E "s/org_apache_//g" | \
grep -v "juli_logging" | grep -v "tomcat_util" | grep -v "cataline_util" | grep -v "test" | \
sort | uniq >> test.dot ; echo "}" >> test.dot ;
```

Es wird eine .dot Datei erstellt, die für Klassen die verwendeten Pakete auflistet. Aus dieser Datei kann, durch das Programm Graphviz, eine PDF-Datei, catalina.dot, erstellt werden, welche die Verknüpfung der Klassen als Diagramm darstellt. 

Erstellen der .pdf Datei für den Graphen
```
dot -Tpdf catalina.dot > catalina.pdf
```

[Graph als PDF](output/catalina.pdf)

Hierbei wurden die Pakete catalina_core, catalina_valves und catalina_connector deutlich in den Mittelpunkt gestellt und sehr häufig verbunden.
Auf das Request-handling deuten die Klassen ApplicationRequest.java (catalina_core) und Request.java (catalina_connector) hin. Auf Grund der Namensgebung wurde zuerst die Klasse Request.java untersucht.

Durch das Debugging-Tool haben wir folgenden Ablauf feststellen können:
Die Klasse ApplicationRequest.java (catalina_core) wird von bei einem Get-Request nicht angesprochen, weshalb wir dann einen Breakpoint in der Klasse Request.java (catalina_connector) gesetzt haben.
Hierbei ist uns aufgefallen das nachdem erstellen eines Request Objektes die Funktion

## Probleme

