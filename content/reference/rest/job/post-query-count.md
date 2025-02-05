---

title: "Get Job Count (POST)"
weight: 50

menu:
  main:
    name: "Get List Count (POST)"
    identifier: "rest-api-job-post-query-count"
    parent: "rest-api-job"
    pre: "POST `/job/count`"

---


Queries for jobs that fulfill given parameters. This method takes the same message body as the [Get Jobs (POST)](../../reference/rest/job/post-query.md) method and therefore it is slightly more powerful than the [Get Job Count](../../reference/rest/job/get-query-count.md) method.


# Method

POST `/job/count`


# Parameters

## Request Body

A JSON object with the following properties:

<table class="table table-striped">
  <tr>
    <th>Name</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>jobId</td>
    <td>Filter by job id.</td>
  </tr>
  <tr>
    <td>jobIds</td>
    <td>Filter by a JSON array of job ids.</td>
  </tr>
  <tr>
    <td>jobDefinitionId</td>
    <td>Only select jobs which exist for the given job definition.</td>
  </tr>
  <tr>
    <td>processInstanceId</td>
    <td>Only select jobs which exist for the given process instance.</td>
  </tr>
  <tr>
    <td>processInstanceIds</td>
    <td>Only select jobs which exist for the given a JSON array of process instance ids.</td>
  </tr>
  <tr>
    <td>executionId</td>
    <td>Only select jobs which exist for the given execution.</td>
  </tr>
  <tr>
    <td>processDefinitionId</td>
    <td>Filter by the id of the process definition the jobs run on.</td>
  </tr>
  <tr>
    <td>processDefinitionKey</td>
    <td>Filter by the key of the process definition the jobs run on.</td>
  </tr>
  <tr>
    <td>activityId</td>
    <td>Only select jobs which exist for an activity with the given id.</td>
  </tr>
  <tr>
    <td>withRetriesLeft</td>
    <td>Only select jobs which have retries left. Value may only be <code>true</code>, as <code>false</code> is the default behavior.</td>
  </tr>
  <tr>
    <td>executable</td>
    <td>Only select jobs which are executable, i.e., retries &gt; 0 and due date is <code>null</code> or due date is in the past. Value may only be <code>true</code>, as <code>false</code> is the default behavior.</td>
  </tr>
  <tr>
    <td>timers</td>
    <td>Only select jobs that are timers. Cannot be used together with <code>messages</code>. Value may only be <code>true</code>, as <code>false</code> is the default behavior.</td>
  </tr>
  <tr>
    <td>messages</td>
    <td>Only select jobs that are messages. Cannot be used together with <code>timers</code>. Value may only be <code>true</code>, as <code>false</code> is the default behavior.</td>
  </tr>
  <tr>
    <td>dueDates</td>
    <td>Only select jobs where the due date is lower or higher than the given date.
    Due date expressions are given in an array of objects that have two properties `operator` and `value`.<br/>
    <code>operator</code> is the comparison operator to be used and <code>value</code> the date value as string.<br/>
    <br/>
    Valid operator values are: <code>gt</code> - greater than; <code>lt</code> - lower than.<br/>
    <code>value</code> may not contain underscore or comma characters.
    </td>
  </tr>
  <tr>
    <td>createTimes</td>
    <td>Only select jobs created before or after the given date.
    Create time expressions are given in an array of objects that have two properties `operator` and `value`.<br/>
    <code>operator</code> is the comparison operator to be used and <code>value</code> the date value as string.<br/>
    <br/>
    Valid operator values are: <code>gt</code> - greater than; <code>lt</code> - lower than.<br/>
    <code>value</code> may not contain underscore or comma characters.
    </td>
  </tr>
  <tr>
    <td>withException</td>
    <td>Only select jobs that failed due to an exception. Value may only be <code>true</code>, as <code>false</code> is the default behavior.</td>
  </tr>
  <tr>
    <td>exceptionMessage</td>
    <td>Only select jobs that failed due to an exception with the given message.</td>
  </tr>
  <tr>
    <td>failedActivityId</td>
    <td>Only select jobs that failed due to an exception at an activity with the given id.</td>
  </tr>
  <tr>
    <td>noRetriesLeft</td>
    <td>Only select jobs which have no retries left. Value may only be <code>true</code>, as <code>false</code> is the default behavior.</td>
  </tr>
  <tr>
    <td>active</td>
    <td>Only include active jobs. Value may only be <code>true</code>, as <code>false</code> is the default behavior.</td>
  </tr>
  <tr>
    <td>suspended</td>
    <td>Only include suspended jobs. Value may only be <code>true</code>, as <code>false</code> is the default behavior.</td>
  </tr>
  <tr>
    <td>priorityLowerThanOrEquals</td>
    <td>Only include jobs with a priority lower than or equal to the given value. Value must be a valid <code>long</code> value.</td>
  </tr>
  <tr>
    <td>priorityHigherThanOrEquals</td>
    <td>Only include jobs with a priority higher than or equal to the given value. Value must be a valid <code>long</code> value.</td>
  </tr>
  <tr>
    <td>tenantIdIn</td>
    <td>Only include jobs which belong to one of the given list a JSON array of tenant ids.</td>
  </tr>
  <tr>
    <td>withoutTenantId</td>
    <td>Only include jobs which belong to no tenant. Value may only be <code>true</code>, as <code>false</code> is the default behavior.</td>
  </tr>
  <tr>
    <td>includeJobsWithoutTenantId</td>
    <td>Include jobs which belong to no tenant. Can be used in combination with <code>tenantIdIn</code>. Value may only be <code>true</code>, as <code>false</code> is the default behavior.</td>
  </tr>
</table>


# Result

A JSON object that contains the count as the only property.

<table class="table table-striped">
  <tr>
    <th>Name</th>
    <th>Type</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>count</td>
    <td>Number</td>
    <td>The number of matching executions.</td>
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
    <td>Returned if some of the query parameters are invalid, for example, if an invalid operator for due date comparison is used. See the <a href="../../reference/rest/overview/_index.md#error-handling" >}}">Introduction</a> for the error response format.</td>
  </tr>
</table>


# Example

## Request

POST `/job/count`

Request Body:

    {
      "dueDates":
        [
          {
            "operator": "gt",
            "value": "2012-07-17T17:00:00.000+0200"
          },
          {
            "operator": "lt",
            "value": "2012-07-17T18:00:00.000+0200"
          }
        ],
      "createTimes":
        [
          {
            "operator": "gt",
            "value": "2012-05-05T10:00:00.000+0200"
          },
          {
            "operator": "lt",
            "value": "2012-07-16T15:00:00.000+0200"
          }
        ]
    }

## Response

    {"count": 2}
