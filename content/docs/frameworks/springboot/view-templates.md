---
weight: 999
title: "View Templates"
description: ""
icon: "article"
date: "2023-10-12T20:01:22+02:00"
lastmod: "2023-10-12T20:01:22+02:00"
draft: false
toc: true
---

## Example

### th:replace - What does this do (line 2)?
- Replace this content with the content of the layout. More precisely with the fragment "maincontent".
- Define the tag "section" as content attribute for the maincontent fragment. The section-part will later be placed inside the layout template.

-- resources/templates/questionnaires/list.html --

{{< prism lang="html" line-numbers="true" >}}
<!DOCTYPE html>
<html th:replace="~{layout :: maincontent(~{::section})}">

<section>
    <a class="btn btn-success float-end" th:href="@{/questionnaires} + '?form'">
        Add Questionnaire
    </a>
    <h3>Questionnaires</h3>
    <div th:if="${questionnaires.isEmpty()}">
        <h2 style="text-align: center">No Questionnaires found</h2>
    </div>
    <div style="padding-top: 10px;">
        <table class="table table-condensed table-hover">
            <tbody>
            <tr th:each="questionnaire : ${questionnaires}">
                <td colspan="1" style="vertical-align: middle;" th:text="${questionnaire.id}" />
                <td colspan="3" style="vertical-align: middle;" th:text="${questionnaire.title}" />
                <td colspan="10" style="vertical-align: middle;" th:text="${questionnaire.description}" />
                <td>
                    <div class="btn-group float-end" role="group">
                        <a class="btn btn-secondary" th:href="@{/questionnaires} + '/' + ${questionnaire.id}">Show</a>
                    </div>
                </td>
            </tr>
            </tbody>
        </table>
    </div>
</section>

</html>
{{< /prism >}}

### fragment - inside layout.html

and in the layout.html?
- Define the fragment name "maincontent" with an attribute called "content"
- The body contains a div with a header, the content (from the attribute) and the footer

{{< prism lang="html" line-numbers="true" >}}
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org" th:fragment="maincontent(content)">
<head>
	<title>Flashcard App</title>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" />
</head>
<body>
	<div class="container-fluid">
        <div th:replace="~{header :: header}">Header Placeholder</div>
        <div th:replace="${content}">Content Placeholder</div>
        <div th:replace="~{footer :: footer}">Footer Placeholder</div>
	</div>
</body>
</html>
{{< /prism >}}
