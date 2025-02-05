---

title: "Introduction"
weight: 10
layout: "single"

menu:
  main:
    identifier: "user-guide-introduction"

---


Welcome to the Camunda Platform Manual! Camunda is a Java-based framework supporting BPMN for workflow and process automation, CMMN for Case Management and DMN for Business Decision Management. Also see: [Implemented Standards](../../introduction/implemented-standards.md).

This document contains information about the features provided by the Camunda Platform.

To give you an overview of Camunda, the following illustration shows the most important components along with some typical user roles.

{{< img src="img/architecture-overview.png" title="Camunda Components and Roles" >}}


# Process Engine & Infrastructure

* [Process Engine](../../user-guide/process-engine/_index.md) The process engine is a Java library responsible for executing BPMN 2.0 processes, CMMN 1.1 cases and DMN 1.3 decisions. It has a lightweight POJO core and uses a relational database for persistence. ORM mapping is provided by the MyBatis mapping framework.
* [Spring Framework Integration](../../user-guide/spring-framework-integration/_index.md)
* [CDI/Java EE Integration](../../user-guide/cdi-java-ee-integration/_index.md)
* [Runtime Container Integration](../../user-guide/runtime-container-integration/_index.md) (Integration with application server infrastructure.)

# Modeler

* [Camunda Modeler](../../modeler/_index.md): Modeling tool for BPMN 2.0 and CMMN 1.1 diagrams as well as DMN 1.3 decision tables.
* [bpmn.io](http://bpmn.io/): Open-source project for the modeling framework and toolkits.

# Web Applications

* [REST API](../../reference/rest/_index.md) The REST API allows you to use the process engine from a remote application or a JavaScript application. (Note: The documentation of the REST API is factored out into own documents.)
* [Camunda Tasklist](../../webapps/tasklist/_index.md) A web application for human workflow management and user tasks that allows process participants to inspect their workflow tasks and navigate to task forms in order to work on the tasks and provide data input.
* [Camunda Cockpit](../../webapps/cockpit/_index.md) A web application for process monitoring and operations that allows you to search for process instances, inspect their state and repair broken instances.
* [Camunda Admin](../../webapps/admin/_index.md) A web application that allows you to manage users, groups and authorizations.
