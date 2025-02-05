---

title: "Fetch and Lock External Tasks"
weight: 60

menu:
  main:
    name: "Fetch and Lock"
    identifier: "rest-api-external-task-fetch-lock"
    parent: "rest-api-external-task"
    pre: "POST `/external-task/fetchAndLock`"

---

Fetches and locks a specific number of external tasks for execution by a worker. Query can be restricted to specific task topics and for each task topic an individual lock time can be provided.

# Method

POST `/external-task/fetchAndLock`


# Parameters

## Request Body

A JSON object with the following properties:

<table class="table table-striped">
  <tr>
    <th>Name</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>workerId</td>
    <td><b>Mandatory.</b> The id of the worker on which behalf tasks are fetched. The returned tasks are locked for that worker and can only be completed when providing the same worker id.</td>
  </tr>
  <tr>
    <td>maxTasks</td>
    <td><b>Mandatory.</b> The maximum number of tasks to return.</td>
  </tr>
  <tr>
    <td>usePriority</td>
    <td>A boolean value, which indicates whether the task should be fetched based on its priority or arbitrarily.</td>
  </tr>
  <tr>
    <td>asyncResponseTimeout</td>
    <td>The <a href="../../user-guide/process-engine/external-tasks.md#long-polling-to-fetch-and-lock-external-tasks" >}}">Long Polling</a> timeout in milliseconds.<br>
    <strong>Note:</strong> The value cannot be set larger than 1.800.000 milliseconds (corresponds to 30 minutes).</td>
  </tr>
  <tr>
    <td>topics</td>
    <td>
      <p>
        A JSON array of topic objects for which external tasks should be fetched. The returned tasks may be arbitrarily distributed among these topics. Each topic object has the following properties:
      </p>
      <table class="table table-striped">
        <tr>
          <th>Name</th>
          <th>Description</th>
        </tr>
        <tr>
          <td>topicName</td>
          <td><b>Mandatory.</b> The topic's name.</td>
        </tr>
        <tr>
          <td>lockDuration</td>
          <td><b>Mandatory.</b> The duration to lock the external tasks for in milliseconds.</td>
        </tr>
        <tr>
          <td>variables</td>
          <td>A JSON array of <code>String</code> values that represent variable names. For each result task belonging to this topic, the given variables are returned as well if they are accessible from the external task's execution. If not provided - all variables will be fetched.</td>
        </tr>
        <tr>
          <td>localVariables</td>
          <td>If <code>true</code> only local variables will be fetched.</td>
        </tr>
        <tr>
          <td>businessKey</td>
          <td>A <code>String</code> value which enables the filtering of tasks based on process instance business key.</td>
        </tr>
        <tr>
          <td>processDefinitionId</td>
          <td>Filter tasks based on process definition id.</td>
        </tr>
        <tr>
          <td>processDefinitionIdIn</td>
          <td>Filter tasks based on process definition ids.</td>
        </tr>
        <tr>
          <td>processDefinitionKey</td>
          <td>Filter tasks based on process definition key.</td>
        </tr>
        <tr>
          <td>processDefinitionKeyIn</td>
          <td>Filter tasks based on process definition keys.</td>
        </tr>
        <tr>
          <td>processDefinitionVersionTag</td>
          <td>Filter tasks based on process definition version tag.</td>
        </tr>
        <tr>
          <td>withoutTenantId</td>
          <td>Filter tasks without tenant id.</td>
        </tr>
        <tr>
          <td>tenantIdIn</td>
          <td>Filter tasks based on tenant ids.</td>
        </tr>
        <tr>
          <td>processVariables</td>
          <td>A <code>JSON</code> object used for filtering tasks based on process instance variable values. A property name of the object represents a process variable name, while the property value represents the process variable value to filter tasks by.</td>
        </tr>
        <tr>
          <td>deserializeValues</td>
          <td>
            <p>Determines whether serializable variable values (typically variables that store custom Java objects) should be deserialized on server side (default <code>false</code>).</p>

            <p>If set to <code>true</code>, a serializable variable will be deserialized on server side and transformed to JSON using Jackson's POJO/bean property introspection feature. Note that this requires the Java classes of the variable value to be on the REST API's classpath.</p>

            <p>If set to <code>false</code>, a serializable variable will be returned in its serialized format. For example, a variable that is serialized as XML will be returned as a JSON string containing XML.</p>
          </td>
        </tr>
        <tr>
          <td>includeExtensionProperties</td>
          <td>Determines whether custom extension properties defined in the BPMN activity of the external task (e.g. via the Extensions tab in the Camunda modeler) should be included in the response. Default: <code>false</code></td>
        </tr>
      </table>
    </td>
  </tr>
</table>


# Result

A JSON array of locked external task objects.
Each locked external task object has the following properties:

<table class="table table-striped">
  <tr>
    <th>Name</th>
    <th>Type</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>activityId</td>
    <td>String</td>
    <td>The id of the activity that this external task belongs to.</td>
  </tr>
  <tr>
    <td>activityInstanceId</td>
    <td>String</td>
    <td>The id of the activity instance that the external task belongs to.</td>
  </tr>
  <tr>
    <td>errorMessage</td>
    <td>String</td>
    <td>The full error message submitted with the latest reported failure executing this task;
    <br/><code>null</code> if no failure was reported previously or if no error message was submitted</td>
  </tr>
  <tr>
    <td>errorDetails</td>
    <td>String</td>
    <td>The error details submitted with the latest reported failure executing this task.
    <br/><code>null</code> if no failure was reported previously or if no error details was submitted</td>
  </tr>
  <tr>
    <td>executionId</td>
    <td>String</td>
    <td>The id of the execution that the external task belongs to.</td>
  </tr>
  <tr>
    <td>id</td>
    <td>String</td>
    <td>The id of the external task.</td>
  </tr>
  <tr>
    <td>lockExpirationTime</td>
    <td>String</td>
    <td>The date that the task's most recent lock expires or has expired.</td>
  </tr>
  <tr>
    <td>processDefinitionId</td>
    <td>String</td>
    <td>The id of the process definition the external task is defined in.</td>
  </tr>
  <tr>
    <td>processDefinitionKey</td>
    <td>String</td>
    <td>The key of the process definition the external task is defined in.</td>
  </tr>
  <tr>
    <td>processDefinitionVersionTag</td>
    <td>String</td>
    <td>The version tag of the process definition the external task is defined in.</td>
  </tr>
  <tr>
    <td>processInstanceId</td>
    <td>String</td>
    <td>The id of the process instance the external task belongs to.</td>
  </tr>
  <tr>
    <td>tenantId</td>
    <td>String</td>
    <td>The id of the tenant the external task belongs to.</td>
  </tr>
  <tr>
    <td>retries</td>
    <td>Number</td>
    <td>The number of retries the task currently has left.</td>
  </tr>
  <tr>
    <td>suspended</td>
    <td>boolean</td>
    <td>Whether the process instance the external task belongs to is suspended.</td>
  </tr>
  <tr>
    <td>workerId</td>
    <td>String</td>
    <td>The id of the worker that posesses or posessed the most recent lock.</td>
  </tr>
  <tr>
    <td>priority</td>
    <td>Number</td>
    <td>The priority of the external task.</td>
  </tr>
  <tr>
    <td>topicName</td>
    <td>String</td>
    <td>The topic name of the external task.</td>
  </tr>
  <tr>
    <td>businessKey</td>
    <td>String</td>
    <td>The business key of the process instance the external task belongs to.</td>
  </tr>
  <tr>
    <td>variables</td>
    <td>Object</td>
    <td><p>A JSON object containing a property for each of the requested variables. The key is the variable name, the value is a JSON object of serialized variable values with the following properties:</p>
      {{< rest-var-response >}}
    </td>
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
    <td>500</td>
    <td>application/json</td>
    <td>Returned if fetching is not successful, for example due to missing parameters. See the <a href="../../reference/rest/overview/_index.md#error-handling" >}}">Introduction</a> for the error response format.</td>
  </tr>
</table>


# Example

## Request

POST `/external-task/fetchAndLock`

Request Body:

```json
    {
      "workerId":"aWorkerId",
      "maxTasks":2,
	  "usePriority":true,
      "topics":
          [{"topicName": "createOrder",
          "lockDuration": 10000,
          "variables": ["orderId"]
          }]
    }
```

## Response

Status 200.

```json
    [{
      "activityId": "anActivityId",
      "activityInstanceId": "anActivityInstanceId",
      "errorMessage": "anErrorMessage",
      "errorDetails": "anErrorDetails",
      "executionId": "anExecutionId",
      "id": "anExternalTaskId",
      "lockExpirationTime": "2015-10-06T16:34:42.000+0200",
      "processDefinitionId": "aProcessDefinitionId",
      "processDefinitionKey": "aProcessDefinitionKey",
      "processInstanceId": "aProcessInstanceId",
      "tenantId": null,
      "retries": 3,
      "workerId": "aWorkerId",
      "priority": 4,
      "topicName": "createOrder",
      "variables": {
        "orderId": {
          "type": "String",
          "value": "1234",
          "valueInfo": {}
        }
      }
    },
    {
      "activityId": "anActivityId",
      "activityInstanceId": "anActivityInstanceId",
      "errorMessage": "anErrorMessage",
      "errorDetails": "anotherErrorDetails",
      "executionId": "anExecutionId",
      "id": "anExternalTaskId",
      "lockExpirationTime": "2015-10-06T16:34:42.000+0200",
      "processDefinitionId": "aProcessDefinitionId",
      "processDefinitionKey": "aProcessDefinitionKey",
      "processInstanceId": "aProcessInstanceId",
      "tenantId": null,
      "retries": 3,
      "workerId": "aWorkerId",
      "priority": 0,
      "topicName": "createOrder",
      "variables": {
        "orderId": {
          "type": "String",
          "value": "3456",
          "valueInfo": {}
        }
      }
    }]
```

# Example with all variables
 
## Request

POST `/external-task/fetchAndLock`

Request Body:

```json
    {
      "workerId":"aWorkerId",
      "maxTasks":2,
      "usePriority":true,
      "topics":
          [{"topicName": "createOrder",
            "lockDuration": 10000,
            "processDefinitionId": "aProcessDefinitionId",
            "tenantIdIn": "tenantOne"
          }]
    }
```


## Response

Status 200.

```json
    [{
      "activityId": "anActivityId",
      "activityInstanceId": "anActivityInstanceId",
      "errorMessage": "anErrorMessage",
      "errorDetails": "anErrorDetails",
      "executionId": "anExecutionId",
      "id": "anExternalTaskId",
      "lockExpirationTime": "2015-10-06T16:34:42.00+0200",
      "processDefinitionId": "aProcessDefinitionId",
      "processDefinitionKey": "aProcessDefinitionKey",
      "processInstanceId": "aProcessInstanceId",
      "tenantId": "tenantOne",
      "retries": 3,
      "workerId": "aWorkerId",
      "priority": 4,
      "topicName": "createOrder",
      "businessKey": "aBusinessKey",
      "variables": {
        "orderId": {
          "type": "String",
          "value": "1234",
          "valueInfo": {}
        }
      }
    },
    {
      "activityId": "anActivityId",
      "activityInstanceId": "anActivityInstanceId",
      "errorMessage": "anErrorMessage",
      "errorDetails": "anotherErrorDetails",
      "executionId": "anExecutionId",
      "id": "anExternalTaskId",
      "lockExpirationTime": "2015-10-06T16:34:42.000+0200",
      "processDefinitionId": "aProcessDefinitionId",
      "processDefinitionKey": "aProcessDefinitionKey",
      "processInstanceId": "aProcessInstanceId",
      "tenantId": null,
      "retries": 3,
      "workerId": "aWorkerId",
      "priority": 0,
      "topicName": "createOrder",
      "businessKey": "aBusinessKey",
      "variables": {
        "orderId": {
          "type": "String",
          "value": "3456",
          "valueInfo": {}
        }
      }
    }]
```

# Example with Extension Properties

Given the external task definition contains extension properties:

```xml
    <bpmn:serviceTask id="anActivityId" name="Some External Task" camunda:type="external" camunda:topic="createOrder">
      <bpmn:extensionElements>
        <camunda:properties>
          <camunda:property name="property1" value="value1" />
          <camunda:property name="property2" value="value2" />
        </camunda:properties>
      </bpmn:extensionElements>
    </bpmn:serviceTask>
```

## Request

POST `/external-task/fetchAndLock`

Request Body:

```json
    {
      "workerId":"aWorkerId",
      "maxTasks":1,
      "usePriority":true,
      "topics":
          [{"topicName": "createOrder",
          "lockDuration": 10000,
          "includeExtensionProperties": true
          }]
    }

```

## Response

Status 200.

```json
  [{
      "activityId": "anActivityId",
      "activityInstanceId": "anActivityInstanceId",
      "errorMessage": "anErrorMessage",
      "errorDetails": "anErrorDetails",
      "executionId": "anExecutionId",
      "id": "anExternalTaskId",
      "lockExpirationTime": "2015-10-06T16:34:42.000+0200",
      "processDefinitionId": "aProcessDefinitionId",
      "processDefinitionKey": "aProcessDefinitionKey",
      "processInstanceId": "aProcessInstanceId",
      "retries": null,
      "suspended": false,
      "workerId": "aWorkerId",
      "topicName": "createOrder",
      "tenantId": null,
      "variables": {},
      "priority": 0,
      "businessKey": "default",
      "extensionProperties": {
          "property2": "value2",
          "property1": "value1"
      }
    }
]
```
