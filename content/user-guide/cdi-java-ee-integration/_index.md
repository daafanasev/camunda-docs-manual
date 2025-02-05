---

title: "CDI and Java EE Integration"
weight: 60

menu:
  main:
    identifier: "user-guide-cdi"
    parent: "user-guide"

---

The camunda-engine-cdi module provides programming model integration with CDI (Context and Dependency Injection). CDI is the Java EE 6 standard for Dependency Injection. The camunda-engine-cdi integration leverages both the configuration of the Camunda engine and the extensibility of CDI. The most prominent features are:

 * A custom El-Resolver for resolving CDI beans (including EJBs) from the process,
 * Support for @BusinessProcessScoped beans (CDI beans, the lifecycle of which are bound to a process instance),
 * Declarative control over a process instance using annotations,
 * The Process Engine is hooked-up to the CDI event bus,
 * Works with both Java EE and Java SE,
 * Support for unit testing.

### Quarkus Engine Extension
Since Quarkus ArC does not aim to fully implement CDI 2.0, you cannot use the full range of features the `camunda-engine-cdi` module provides.
Read about the limitations in the [Quarkus Integration](../../user-guide/quarkus-integration/cdi-integration.md#limitations) guide.


# Maven Dependency

To use the camunda-engine-cdi module inside your application, you must include the following Maven dependency:

### Заметка class="info" >}}
  Please import the [Camunda BOM](/get-started/apache-maven/) to ensure correct versions for every Camunda project.


```xml
<dependency>
  <groupId>org.camunda.bpm</groupId>
  <artifactId>camunda-engine-cdi</artifactId>
</dependency>
```

Replace 'x' with your Camunda Platform version.

### Заметка class="info" >}}
  There is a [project template for Maven](../../user-guide/process-applications/maven-archetypes.md) called `camunda-archetype-ejb-war`, which gives you a complete running project, including CDI integration.

