

# Surfreport API Reference Tutorial

## Resource Description
Contains information about the surfing conditions, including the surf height, water temperature, wind, and tide. Also provides an overall recommendation about whether to go surfing or not in a particular day.

## Endpoints and Methods

### Endpoints
_GET_ surfreport/`{beachId}`

Gets the surf conditions for a specific beach ID.

_POST_

_PUT_

_PATCH_

_DELETE_ 

## Parameters

<table>
<thead>
  <tr>
    <th>Query String </th>
    <th>Required / optional</th>
    <th>Description</th>
    <th>Type</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>`days`</td>
    <td>Optional</td>
    <td>The number of days to include in the API response. Default is 3.</td>
    <td>`Integer`</td>
  </tr>
  <tr>
    <td>time</td>
    <td>Optional</td>
    <td>If you include the time, then only the current hour will be returned in the response.</td>
    <td>Integer. Unix format (ms since 1970) in UTC.</td>
  </tr>
</tbody>
</table>

## Request example