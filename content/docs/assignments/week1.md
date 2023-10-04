---
weight: 200
title : 'Week1'
date : 2023-09-21T10:38:27+02:00
tags: ["draft"]
author: "Leon"
math: false
---

# AB

## Aufgabe 1 (Servlet in Betrieb nehmen)

tomcat...

## Aufgabe 2 (Repetition Verteilte Systeme)

Beantworten Sie folgende Fragen auf einem separaten Blatt Papier:

1.	Zeichnen Sie die Struktur im Dateisystem dieser JEE-Webapplikation auf. <br>
      **Hinweis**: Öffnen sie die WAR-Datei - das ist die gefragte Struktur.

![webapp struktur](/webfr/webapp_struktur.png)

4. Was ist die Funktion des Files `web.xml`?
> Das web.xml File enthält Konfigurationsinformationen über eine JAVA EE Anwendung. In diesem File werden die Servelts, Filer, Listener und andere Eigenschaften konfiguriert.
> Tomcat liest dann diese Informationen ein und stellt dementsprechend die Anwendung bereit.

3. Kann man den Servlet-Eintrag aus dem File `web.xml` löschen?
> Kann ab Servlet Version 3.0 gemacht werden. Dabei muss aber via Annotation diese Information in der Klasse erwähnt werden
> `@WebServlet(...)`

4. Erklären Sie welche URLs vom `BasicServlet` verarbeitet werden?
> http://localhost:8080/basic
> http://localhost:8080/basic/questionaires

5. Was ist ein `ServletContext`?
> Beschreibt den Kontext der gesamten WebApp. 
> Kann mehrere Servlets beinhalten und wird beim Start der Webapp initialisiert und konfiguriert. 

6. Analysieren Sie das Servlet `BasicServlet`, indem Sie zu jeder nummerierten Zeile (#1, #2, ..., #7) im folgenden Code eine kurze Erklärung geben:


```java
public class BasicServlet extends HttpServlet {	#1 

	protected void doGet(HttpServletRequest request,
			HttpServletResponse response) throws ServletException, IOException {	#2
		response.setContentType("text/html; charset=utf-8");	#3

		String[] pathElements = request.getRequestURI().split("/");
		if (isLastPathElementQuestionnaires(pathElements)) {	#4
			handleQuestionnairesRequest(request, response);
		} else {
			handleIndexRequest(request, response);
		}
	}

	private boolean isLastPathElementQuestionnaires(String[] pathElements) {
		String last = pathElements[pathElements.length-1];
		return last.equals("questionnaires");
	}

	...

	private void handleIndexRequest(HttpServletRequest request,
			HttpServletResponse response) throws IOException {
		PrintWriter writer = response.getWriter();	#5
		writer.append("<html><head><title>Example</title></head><body>");
		writer.append("<h3>Welcome</h3>");
		String url = request.getContextPath()+request.getServletPath();
		writer.append("<p><a href='" + response.encodeURL(url) + "/questionnaires'>All Questionnaires</a></p>");
		writer.append("</body></html>");
	}
	
	@Override
	public void init(ServletConfig config) throws ServletException {	#6
		super.init(config);
		QuestionnaireInitializer.createQuestionnaires();	#7
	}
}
```

> #1: Die Klasse ist ein HttpServlet und kann die Http Methoden wie GET, POST verarbeiten (doGet(), doPost())
> #2: Alle GET-Requests werden in dieser Methode verarbeitet. Im Parameter response wird die Antwort abgelegt.
> #3: Der Typ der Antwort wird festgelegt, in diesem Fall HTML. Muss **unbedingt** vor response.getWrite() erfolgen.
> #4: Dispatching aufgrund des letzten URL-Path-Elements.
> #5: Mit response.getWriter() wird ein Buffer für die Antwort bereitgestellt.
> #6: Hier kann das Servlet initialisiert werden, entweder beim ersten Request oder beim Hochfahren der App ("load-on-startup")
> #7: Initialisierung einiger Fragebögen zu Testzwecken.


# UB

## Aufgabe 1

`gradle build && sudo cp build/libs/ab2.war /opt/tomcat/webapps`

`curl -X PUT -i http://localhost:8080/ab2`

`curl -X DELETE -i http://localhost:8080/ab2`
