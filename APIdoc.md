

# Surfreport API Reference 

## Resource Description
Contains information about the surfing conditions, including the surf height, water temperature, wind, and tide. Also provides an overall recommendation about whether to go surfing or not in a particular day.

## Endpoints and Methods

### Endpoints
**_GET_** surfreport/`{beachId}`

Gets the surf conditions for a specific beach ID.

**_POST_**

**_PUT_**

**_PATCH_**

**_DELETE_**

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
    <td>days</td>
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
<br>

## Request Example



### Request sample

```
curl -I -X GET "https://api.openweathermap.org/data/2.5/surfreport?zip=95050&appid=APIKEY&units=imperial&days=2"
```

(In the above code, replace `APIKEY` with your actual API key.)

## Response Example and Schema
### Sample response

```
 {
    "surfreport": [
        {
            "beach": "Santa Cruz",
            "monday": {
                "1pm": {
                    "tide": 5,
                    "wind": 15,
                    "watertemp": 80,
                    "surfheight": 5,
                    "recommendation": "Go surfing!"
                },
                "2pm": {
                    "tide": -1,
                    "wind": 1,
                    "watertemp": 50,
                    "surfheight": 3,
                    "recommendation": "Surfing conditions are okay, not great."
                },
                "3pm": {
                    "tide": -1,
                    "wind": 10,
                    "watertemp": 65,
                    "surfheight": 1,
                    "recommendation": "Not a good day for surfing."
                }
                ...
            }
        }
    ]
}
```

#### Response definition

<table>
<thead>
  <tr>
    <th>Response item</th>
    <th>Description</th>
    <th>Data</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>beach</td>
    <td>The beach you selected based on the beach ID in the request. The beach name is the official name as described in the National Park Service Geodatabase.</td>
    <td>String</td>
  </tr>
  <tr>
    <td>{day}</td>
    <td>The day of the week selected. A maximum of 3 days gets returned in the response.</td>
    <td>Object</td>
  </tr>
  <tr>
    <td>{time}</td>
    <td>The time for the conditions. This item is included only if you include a time parameter in the request.</td>
    <td>Object</td>
  </tr>
  <tr>
    <td>{day}/{time}/tide</td>
    <td>The level of tide at the beach for a specific day and time. Tide is the distance inland that the water rises to, and can be a positive or negative number. When the tide is out, the number is negative. When the tide is in, the number is positive. The 0 point reflects the line when the tide is neither going in nor out but is in transition between the two states.</td>
    <td>Integer</td>
  </tr>
  <tr>
    <td>{day}/{time}/wind</td>
    <td>The wind speed at the beach, measured in knots (nautical miles per hour). Wind affects the surf height and general wave conditions. Wind speeds of more than 15 knots make surf conditions undesirable because the wind creates white caps and choppy waters</td>
    <td>Integer</td>
  </tr>
  <tr>
    <td>{day}/{time}/watertemp</td>
    <td>The temperature of the water, returned in Fahrenheit or Celsius depending upon the units you specify. Water temperatures below 70 F usually require you to wear a wetsuit. With temperatures below 60, you will need at least a 3mm wetsuit and preferably booties to stay warm.</td>
    <td>Integer</td>
  </tr>
  <tr>
    <td>{day}/{time}/surfheight</td>
    <td>The height of the waves, returned in either feet or centimeters depending on the units you specify. A surf height of 3 feet is the minimum size needed for surfing. If the surf height exceeds 10 feet, it is not safe to surf.</td>
    <td>Integer</td>
  </tr>
  <tr>
    <td>{day}/{time}/recommendation</td>
    <td>An overall recommendation based on a combination of the various factors (wind, watertemp, surfheight). Three responses are possible: (1) "Go surfing!", (2) "Surfing conditions are okay, not great", and (3) "Not a good day for surfing." Each of the three factors is scored with a maximum of 33.33 points, depending on the ideal for each element. The three elements are combined to form a percentage. 0% to 59% yields response 3, 60% - 80% and below yields response 2, and 81% to 100% yields response 1</td>
    <td>String</td>
  </tr>
</tbody>
</table>

