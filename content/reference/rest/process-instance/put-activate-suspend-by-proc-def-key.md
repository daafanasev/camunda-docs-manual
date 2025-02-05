---

title: 'Activate/Suspend Process Instance By Process Definition Key'
weight: 170

menu:
  main:
    name: "Activate/Suspend By Process Definition Key"
    identifier: "rest-api-process-instance-suspend-by-process-definition-key"
    parent: "rest-api-process-instance"
    pre: "PUT `/process-instance/suspended`"

---


Activates or suspends process instances with the given process definition key.

# Method

PUT `/process-instance/suspended`

# Parameters

## Request Body

A JSON object with the following properties:

<table class="table table-striped">
  <tr>
    <th>Name</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>processDefinitionKey</td>
    <td>The process definition key of the process instances to activate or suspend.</td>
  </tr>
  <tr>
    <td>processDefinitionTenantId</td>
    <td>Only activate or suspend process instances of a process definition which belongs to a tenant with the given id.</td>
  </tr>
  <tr>
    <td>processDefinitionWithoutTenantId</td>
    <td>Only activate or suspend process instances of a process definition which belongs to no tenant. Value may only be <code>true</code>, as <code>false</code> is the default behavior.</td>
  </tr>  
  <tr>
    <td>suspended</td>
    <td>A <code>Boolean</code> value which indicates whether to activate or suspend all process instances with the given process definition key. When the value is set to <code>true</code>, all process instances with the given process definition key will be suspended and when the value is set to <code>false</code>, all process instances with the given process definition key will be activated.</td>
  </tr>
</table>


# Result

This method returns no content.

  
# Response Codes

<table class="table table-striped">
  <tr>
    <th>Code</th>
    <th>Media type</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>204</td>
    <td></td>
    <td>Request successful.</td>
  </tr>
  <tr>
    <td>400</td>
    <td>application/json</td>
    <td>Returned if some of the request parameters are invalid, for example if the provided <code>processDefinitionKey</code> parameter is null. See the <a href="../../reference/rest/overview/_index.md#error-handling" >}}">Introduction</a> for the error response format.</td>
  </tr>
</table>

  
# Example

## Request

PUT `/process-instance/suspended`
  
    {
      "processDefinitionKey" : "aProcDefKey",
      "suspended" : true
    }
     
## Response
    
Status 204. No content.