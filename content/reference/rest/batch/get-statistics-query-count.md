---

title: "Get Batch Statistics Count"
weight: 70

menu:
  main:
    name: "Get Statistics Count"
    identifier: "rest-api-batch-get-query-statistics-count"
    parent: "rest-api-batch"
    pre: "GET `/batch/statistics/count`"

---


Requests the number of batch statistics that fulfill the query criteria.  Takes
the same filtering parameters as the [Get Batch Statistics](../../reference/rest/batch/get-statistics-query.md) method.


# Method

GET `/batch/statistics/count`


# Parameters


## Query Parameters

<table class="table table-striped">
  <tr>
    <th>Name</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>batchId</td>
    <td>Filter by batch id.</td>
  </tr>
  <tr>
    <td>type</td>
    <td>Filter by batch type. See the <a href="../../user-guide/process-engine/batch.md#creating-a-batch" >}}">User Guide</a> for more information about batch types.</td>
  </tr>
  <tr>
    <td>tenantIdIn</td>
    <td>Filter by a comma-separated list of tenant ids. A batch matches if it has one of the given tenant ids.</td>
  </tr>
  <tr>
    <td>withoutTenantId</td>
    <td>Only include batches which belong to no tenant. Value can effectively only be <code>true</code>, as <code>false</code> is the default behavior.</td>
  </tr>
  <tr>
    <td>suspended</td>
    <td>
      A <code>Boolean</code> value which indicates whether only active or
      suspended batches should be included. When the value is set to
      <code>true</code>, only suspended batches will be returned and when the
      value is set to <code>false</code>, only active batches will be returned.
    </td>
  </tr>
  <tr>
    <td>createdBy</td>
    <td>Only include batches that were started by this user id.</td>
  </tr>
  <tr>
    <td>startedBefore</td>
    <td>
      Only include batches that were started before the given date.
      By default*, the date must have the format <code>yyyy-MM-dd'T'HH:mm:ss.SSSZ</code>, e.g., <code>2013-01-23T14:42:45.000+0200</code>.
    </td>
  </tr>
  <tr>
    <td>startedAfter</td>
    <td>
      Only include batches that were started after the given date.
      By default*, the date must have the format <code>yyyy-MM-dd'T'HH:mm:ss.SSSZ</code>, e.g., <code>2013-01-23T14:42:45.000+0200</code>.
    </td>
  </tr>
  <tr>
    <td>withFailures</td>
    <td>
      Only include batches having jobs with failures.
      Value can only be <code>true</code>.
    </td>
  </tr>
  <tr>
    <td>withoutFailures</td>
    <td>
      Only include batches having jobs without failures. Also returns batches without jobs.
      Value can only be <code>true</code>.
    </td>
  </tr>
</table>

\* For further information, please see the <a href="../../reference/rest/overview/date-format.md" >}}"> documentation</a>.

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
    <td>The number of matching batches.</td>
  </tr>
</table>


## Response codes

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
    <td>
      Returned if some of the query parameters are invalid, for example if a <code>sortOrder</code> parameter is supplied, but no <code>sortBy</code>.
      See the <a href="../../reference/rest/overview/_index.md#error-handling" >}}">Introduction</a> for the error response format.
    </td>
  </tr>
</table>


# Example

## Request

GET `/batch/statistics/count?type=aBatchType`

## Response

Status 200.

```json
{
  "count": 1
}
```
