---

title: "Get Executions"
weight: 10

menu:
  main:
    name: "Get List"
    identifier: "rest-api-execution-get-query"
    parent: "rest-api-execution"
    pre: "GET `/execution`"

---


Queries for the executions that fulfill given parameters.
Parameters may be static as well as dynamic runtime properties of executions.
The size of the result set can be retrieved by using the [Get Execution Count](../../reference/rest/execution/get-query-count.md) method.


# Method

GET `/execution`


# Parameters

## Query Parameters

<table class="table table-striped">
  <tr>
    <th>Name</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>businessKey</td>
    <td>Filter by the business key of the process instances the executions belong to.</td>
  </tr>
  <tr>
    <td>processDefinitionId</td>
    <td>Filter by the process definition the executions run on.</td>
  </tr>
  <tr>
    <td>processDefinitionKey</td>
    <td>Filter by the key of the process definition the executions run on.</td>
  </tr>
  <tr>
    <td>processInstanceId</td>
    <td>Filter by the id of the process instance the execution belongs to.</td>
  </tr>
  <tr>
    <td>activityId</td>
    <td>Filter by the id of the activity the execution currently executes.</td>
  </tr>
  <tr>
    <td>signalEventSubscriptionName</td>
    <td>Select only those executions that expect a signal of the given name.</td>
  </tr>
  <tr>
    <td>messageEventSubscriptionName</td>
    <td>Select only those executions that expect a message of the given name.</td>
  </tr>
  <tr>
    <td>active</td>
    <td>Only include active executions. Value may only be <code>true</code>, as <code>false</code> is the default behavior.</td>
  </tr>
  <tr>
    <td>suspended</td>
    <td>Only include suspended executions. Value may only be <code>true</code>, as <code>false</code> is the default behavior.</td>
  </tr>
  <tr>
    <td>incidentId</td>
    <td>Filter by the incident id.</td>
  </tr>
  <tr>
    <td>incidentType</td>
    <td>Filter by the incident type. See the <a href="../../user-guide/process-engine/incidents.md#incident-types" >}}">User Guide</a> for a list of incident types.</td>
  </tr>
  <tr>
    <td>incidentMessage</td>
    <td>Filter by the incident message. Exact match.</td>
  </tr>
  <tr>
    <td>incidentMessageLike</td>
    <td>Filter by the incident message that the parameter is a substring of.</td>
  </tr>
  <tr>
    <td>tenantIdIn</td>
    <td>Filter by a comma-separated list of tenant ids. An execution must have one of the given tenant ids.</td>
  </tr>
  <tr>
    <td>variables</td>
    <td>Only include executions that have variables with certain values.
    Variable filtering expressions are comma-separated and are structured as follows:<br/>
    A valid parameter value has the form <code>key_operator_value</code>.
    <code>key</code> is the variable name, <code>operator</code> is the comparison operator to be used and <code>value</code> the variable value.<br/>
    <strong>Note:</strong> Values are always treated as <code>String</code> objects on server side.<br/>
    <br/>
    Valid operator values are: <code>eq</code> - equal to; <code>neq</code> - not equal to; <code>gt</code> - greater than;
    <code>gteq</code> - greater than or equal to; <code>lt</code> - lower than; <code>lteq</code> - lower than or equal to;
    <code>like</code>.<br/>
    <code>key</code> and <code>value</code> may not contain underscore or comma characters.
    </td>
  </tr>
  <tr>
    <td>processVariables</td>
    <td>Only include executions that belong to a process instance with variables with certain values.
    Variable filtering expressions are comma-separated and are structured as follows:<br/>
    A valid parameter value has the form <code>key_operator_value</code>.
    <code>key</code> is the variable name, <code>operator</code> is the comparison operator to be used and <code>value</code> the variable value.<br/>
    <strong>Note:</strong> Values are always treated as <code>String</code> objects on server side.<br/>
    <br/>
    Valid operator values are: <code>eq</code> - equal to; <code>neq</code> - not equal to.<br/>
    <code>key</code> and <code>value</code> may not contain underscore or comma characters.
    </td>
  </tr>
  <tr>
    <td>variableNamesIgnoreCase</td>
    <td>Match all variable names provided in <code>variables</code> and <code>processVariables</code> case-insensitively. If set to <code>true</code> <strong>variableName</strong> and <strong>variablename</strong> are treated as equal.</td>
  </tr>
  <tr>
    <td>variableValuesIgnoreCase</td>
    <td>Match all variable values provided in <code>variables</code> and <code>processVariables</code> case-insensitively. If set to <code>true</code> <strong>variableValue</strong> and <strong>variablevalue</strong> are treated as equal.</td>
  </tr>
  <tr>
    <td>sortBy</td>
    <td>Sort the results lexicographically by a given criterion. Valid values are
    <code>instanceId</code>, <code>definitionKey</code>, <code>definitionId</code> and <code>tenantId</code>.
    Must be used in conjunction with the <code>sortOrder</code> parameter.</td>
  </tr>
  <tr>
    <td>sortOrder</td>
    <td>Sort the results in a given order. Values may be <code>asc</code> for ascending order or <code>desc</code> for descending order.
    Must be used in conjunction with the <code>sortBy</code> parameter.</td>
  </tr>
  <tr>
    <td>firstResult</td>
    <td>Pagination of results. Specifies the index of the first result to return.</td>
  </tr>
  <tr>
    <td>maxResults</td>
    <td>Pagination of results. Specifies the maximum number of results to return. Will return less results if there are no more results left.</td>
  </tr>
</table>


# Result

A JSON array of execution objects.
Each execution object has the following properties:

<table class="table table-striped">
  <tr>
    <th>Name</th>
    <th>Type</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>id</td>
    <td>String</td>
    <td>The id of the execution.</td>
  </tr>
  <tr>
    <td>processInstanceId</td>
    <td>String</td>
    <td>The id of the process instance that this execution instance belongs to.</td>
  </tr>
  <tr>
    <td>ended</td>
    <td>Boolean</td>
    <td>A flag indicating whether the execution has ended or not.</td>
  </tr>
  <tr>
    <td>tenantId</td>
    <td>String</td>
    <td>The tenant id of the execution.</td>
  </tr>
</table>


# Response Codes

<table class="table table-striped">
  <tr>
    <th>Code</th>
    <th>Media type</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>200</td>
    <td>application/json</td>
    <td>Request successful.</td>
  </tr>
  <tr>
    <td>400</td>
    <td>application/json</td>
    <td>Returned if some of the query parameters are invalid, for example if a <code>sortOrder</code> parameter is supplied, but no <code>sortBy</code>, or if an invalid operator for variable comparison is used. See the <a href="../../reference/rest/overview/_index.md#error-handling" >}}">Introduction</a> for the error response format.</td>
  </tr>
</table>


# Example

## Request

GET `/execution?variables=myVariable_eq_camunda`

## Response

Status 200.

    [{"id":"anId",
     "processInstanceId":"aProcInstId",
     "ended":false,
     "tenantId":null}]
