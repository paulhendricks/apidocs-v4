Scheduling
----------

> Example scheduling request to fetch all schedulers:

```shell
curl -s -H "Authorization: Bearer $ACCESS_TOKEN" https://platform.pokitdok.com/api/v4/schedule/schedulers/     
```

```python
client.schedulers()
```

```csharp
client.schedulers();
```

```ruby
client.schedulers
```

```java
client.schedulers();
```

> Response:

```json
[
      {
        "description": "The PokitDok scheduling system",
        "scheduler_uuid": "967d207f-b024-41cc-8cac-89575a1f6fef",
        "name": "PokitDok"
      },
      {
        "description": "Greenway EHR and PM",
        "scheduler_uuid": "d8f38f08-8530-11e4-9a71-0800272e8da1",
        "name": "Greenway"
      },
      {
        "description": "Athena EHR and PM",
        "scheduler_uuid": "d8f46c7a-8530-11e4-9a71-0800272e8da1",
        "name": "Athena"
      }
]
```

> Example scheduling request to fetch a specific scheduler:

```shell
curl -s -H "Authorization: Bearer $ACCESS_TOKEN" "https://platform.pokitdok.com/api/v4/schedule/schedulers/967d207f-b024-41cc-8cac-89575a1f6fef"
```

```python
client.schedulers(scheduler_uuid='967d207f-b024-41cc-8cac-89575a1f6fef')
```

```csharp
client.schedulers("967d207f-b024-41cc-8cac-89575a1f6fef");
```

```ruby
client.schedulers({scheduler_uuid: '967d207f-b024-41cc-8cac-89575a1f6fef'})
```

```java
client.schedulers("967d207f-b024-41cc-8cac-89575a1f6fef");
```

> Response:

```json
[
      {
        "description": "The PokitDok scheduling system",
        "scheduler_uuid": "967d207f-b024-41cc-8cac-89575a1f6fef",
        "name": "PokitDok"
      }
]
```

> Example scheduling request to fetch all appointment types:

```shell
curl -s -H "Authorization: Bearer $ACCESS_TOKEN" https://platform.pokitdok.com/api/v4/schedule/appointmenttypes/
```

```python
client.appointment_types()
```

```csharp
client.appointmentTypes();
```

```ruby
client.appointment_types
```

```java
client.appointmentTypes();
```

> Response:

```json
[
      {
        "type": "OV1",
        "appointment_type_uuid": "ef987691-0a19-447f-814d-f8f3abbf4860",
        "description": "Office Visit",
        "scheduler_uuid": "967d207f-b024-41cc-8cac-89575a1f6fef",
        "duration": 30
      },
      {
        "type": "PC1",
        "appointment_type_uuid": "ef987692-0a19-447f-814d-f8f3abbf4860",
        "description": "Routine Preventive Care",
        "scheduler_uuid": "967d207f-b024-41cc-8cac-89575a1f6fef",
        "duration": 15
      }
]
```

> Example scheduling request to fetch a specific appointment type:

```shell
curl -s -H "Authorization: Bearer $ACCESS_TOKEN" "https://platform.pokitdok.com/api/v4/schedule/appointmenttypes/ef987691-0a19-447f-814d-f8f3abbf4860"
```

```python
client.appointment_types(appointment_type_uuid='ef987693-0a19-447f-814d-f8f3abbf4860')
```

```csharp
client.appointmentTypes("a3a45130-4adb-4d2c-9411-85a9d9ac4aa2");
```

```ruby
client.appointment_types({appointment_type_uuid: 'ef987693-0a19-447f-814d-f8f3abbf4860'})
```

```java
client.appointmentTypes('ef987693-0a19-447f-814d-f8f3abbf4860');
```

> Response:

```json
[
    {
      "type": "OV1",
      "appointment_type_uuid": "ef987693-0a19-447f-814d-f8f3abbf4860",
      "description": "Office Visit",
      "scheduler_uuid": "967d207f-b024-41cc-8cac-89575a1f6fef",
      "duration": 35
    }
]
```

> Example scheduling request which registers an existing patient with a provider's scheduling system:

```shell
curl -s -H "Authorization: Bearer $ACCESS_TOKEN" -H "Content-Type: application/json" -XPOST -d '{
    "pd_patient_uuid": "2773f6ff-00cb-460f-823f-5ff2208511e7",
    "pd_provider_uuid": "b691b7f9-bfa8-486d-a689-214ae47ea6f8",
    "location": [32.788110, -79.932364]
}' https://platform.pokitdok.com/api/v4/schedule/patient/
```

```python
client.post('/schedule/patient/', data={
    "pd_patient_uuid": "2773f6ff-00cb-460f-823f-5ff2208511e7",
    "pd_provider_uuid": "b691b7f9-bfa8-486d-a689-214ae47ea6f8",
    "location": [32.788110, -79.932364]
})
```

```ruby
# Currently not supported in this language.
```

```csharp
string endpoint = "/schedule/patient/";
string method = "POST";
Dictionary<string, object> data = new Dictionary<string, object> {
  {"pd_patient_uuid", "2773f6ff-00cb-460f-823f-5ff2208511e7"},
  {"pd_provider_uuid", "b691b7f9-bfa8-486d-a689-214ae47ea6f8"},
  {"location", new string[] { "32.788110", "-79.932364"}}
};
client.request(endpoint, method, data);
```

```java
// Currently not supported in this language.
```

> Response:

```json
{   "uuid": "2773f6ff-00cb-460f-823f-5ff2208511e7",
    "email": "peg@emailprovider.com",
    "phone": "5553331122",
    "birth_date": "1990-01-13",
    "first_name": "Peg",
    "last_name": "Patient",
    "member_id": "PD20150001"
}
```

> Example scheduling request to create an open slot:

```shell
curl -s -XPOST -H "Authorization: Bearer $ACCESS_TOKEN" - H "Content-Type: application/json" -XPOST -d '{
    "pd_provider_uuid": "b691b7f9-bfa8-486d-a689-214ae47ea6f8",
    "location": [32.788110, -79.932364],
    "appointment_type": "AT1",
    "start_date": "2014-12-16T15:09:34.197709",
    "end_date": "2014-12-16T16:09:34.197717"
    }' https://platform.pokitdok.com/api/v4/schedule/slots/
```

```python
client.schedule_slots({
    "pd_provider_uuid": "b691b7f9-bfa8-486d-a689-214ae47ea6f8",
    "location": [32.788110, -79.932364],
    "appointment_type": "AT1",
    "start_date": "2014-12-16T15:09:34.197709",
    "end_date": "2014-12-16T16:09:34.197717"
})
```

```csharp
client.createSlot(
    new Dictionary<string, object> {
        {"pd_provider_uuid", "b691b7f9-bfa8-486d-a689-214ae47ea6f8"},
        {"location", new Object[] {32.78811, -79.932364}},
        {"appointment_type", "AT1"},
        {"start_date", "2014-12-16T15:09:34.197709"},
        {"end_date", "2014-12-16T16:09:34.197717"}
    });
```

```ruby
client.schedule_slots({
    "pd_provider_uuid": "b691b7f9-bfa8-486d-a689-214ae47ea6f8",
    "location": [32.788110, -79.932364],
    "appointment_type": "AT1",
    "start_date": "2014-12-16T15:09:34.197709",
    "end_date": "2014-12-16T16:09:34.197717"
})
```

```java
StringBuffer buf = new StringBuffer();

buf.append("{");
buf.append("    \"pd_provider_uuid\": \"b691b7f9-bfa8-486d-a689-214ae47ea6f8\",");
buf.append("    \"location\": [32.788110, -79.932364],");
buf.append("    \"appointment_type\": \"AT1\",");
buf.append("    \"start_date\": \"2014-12-16T15:09:34.197709\",");
buf.append("    \"end_date\": \"2014-12-16T16:09:34.197717\"");
buf.append("}");

JSONObject query = (JSONObject) JSONValue.parse(buf.toString());
Map<String, Object> results = client.scheduleSlots(query);
```

> Response:

```json
{
    "pd_appointment_uuid": "ab21e95b-8fa6-41d4-98b9-9a1f6fcff0d2",
    "provider_scheduler_uuid": "8b21efa4-8535-11e4-a6cb-0800272e8da1",
    "appointment_id": "W4MEM00001",
    "appointment_type": "AT1",
    "start_date": "2014-12-16T15:09:34.197709",
    "end_date": "2014-12-16T16:09:34.197717",
    "booked": false
}
```

> Example scheduling request to delete an open slot:

```shell
curl -s -XDELETE -H "Authorization: Bearer $ACCESS_TOKEN" "https://platform.pokitdok.com/api/v4/schedule/slots/ab21e95b-8fa6-41d4-98b9-9a1f6fcff0d2"
```

```python
client.delete('/schedule/slots/ab21e95b-8fa6-41d4-98b9-9a1f6fcff0d2')
```

```ruby
# Currently not supported in this language.
```

```csharp
string endpoint = "/schedule/slots/ab21e95b-8fa6-41d4-98b9-9a1f6fcff0d2";
string method = "DELETE";
client.request(endpoint, method);
```

```java
// Currently not supported in this language.
```

> Example scheduling request used to query for open slots and booked appointments:

```shell
curl -s -H "Authorization: Bearer $ACCESS_TOKEN" "https://platform.pokitdok.com/api/v4/schedule/appointments/?appointment_type=SS1&start_date=2015-01-14T08:00:00&end_date=2015-01-16T17:00:00&patient_uuid=8ae236ff-9ccc-44b0-8717-42653cd719d0"
```

```python
client.appointments(appointment_type='SS1', start_date='2015-01-14T08:00:00',
    end_date='2015-01-16T17:00:00', patient_uuid='8ae236ff-9ccc-44b0-8717-42653cd719d0')
```

```csharp
client.appointments(
    new Dictionary<string, string> {
        {"appointment_type", "SS1"},
        {"start_date", "2015-01-14T08:00:00"},
        {"end_date", "2015-01-16T17:00:00"},
        {"patient_uuid", "8ae236ff-9ccc-44b0-8717-42653cd719d0"}
    });
```

```ruby
client.appointments({appointment_type: 'SS1', start_date: '2015-01-14T08:00:00',
    end_date: '2015-01-16T17:00:00', patient_uuid: '8ae236ff-9ccc-44b0-8717-42653cd719d0'})
```

```java
HashMap<String, String> query = new HashMap<String, String>();
query.put("appointment_type", "SS1");
query.put("start_date", "2015-01-14T08:00:00");
query.put("end_date", "2015-01-16T17:00:00");
query.put("patient_uuid", "8ae236ff-9ccc-44b0-8717-42653cd719d0");

client.appointments(query);
```

> Response:

```json
[
    {
      "pd_appointment_uuid": "ef987691-0a19-447f-814d-f8f3abbf4859",
      "appointment_id": "UYQDUHSMIRCA",
      "appointment_type": "OV1",
      "patient": {
        "first_name": "John",
        "last_name": "Doe",
        "_uuid": "8b21f7b0-8535-11e4-a6cb-0800272e8da1",
        "phone": "800-555-1212",
        "member_id": "M000001",
        "birth_date": "1970-01-01",
        "email": "john@johndoe.com"
      },
      "booked": true,
      "provider_scheduler_uuid": "8b21efa4-8535-11e4-a6cb-0800272e8da1",
      "start_date": "2014-12-16T15:09:34.197709",
      "end_date": "2014-12-16T16:09:34.197717"
    }
]
```

> Example scheduling request to query for a specific open slot or booked appointment

```shell
curl -s -H "Authorization: Bearer $ACCESS_TOKEN" "https://platform.pokitdok.com/api/v4/schedule/appointments/ef987691-0a19-447f-814d-f8f3abbf4859"
```

```python
client.appointments(appointment_uuid='ef987691-0a19-447f-814d-f8f3abbf4859')
```

```csharp
client.appointments("bf8440b1-fd20-4994-bb28-e3981833e796");
```

```ruby
client.appointments({appointment_uuid: 'ef987691-0a19-447f-814d-f8f3abbf4859'})
```

```java
client.appointments("bf8440b1-fd20-4994-bb28-e3981833e796");
```

> Response:

```json
[
    {
      "client_appointment_uuid": "ef987691-0a19-447f-814d-f8f3abbf4859",
      "appointment_id": "UYQDUHSMIRCA",
      "appointment_type": "OV1",
      "patient": {
        "first_name": "John",
        "last_name": "Doe",
        "_uuid": "8b21f7b0-8535-11e4-a6cb-0800272e8da1",
        "phone": "800-555-1212",
        "member_id": "M000001",
        "birth_date": "1970-01-01",
        "email": "john@johndoe.com"
      },
      "booked": true,
      "provider_scheduler_uuid": "8b21efa4-8535-11e4-a6cb-0800272e8da1",
      "start_date": "2014-12-16T15:09:34.197709",
      "end_date": "2014-12-16T16:09:34.197717"
    }
]
```

> Example scheduling request to book an appointment:

```shell
curl -s -XPUT -H "Authorization: Bearer $ACCESS_TOKEN" -H "Content-Type: application/json" -d '{
    "patient": {
        "_uuid": "500ef469-2767-4901-b705-425e9b6f7f83",
        "email": "john@hondoe.com",
        "phone": "800-555-1212",
        "birth_date": "1970-01-01",
        "first_name": "John",
        "last_name": "Doe",
        "member_id": "M000001"
        },
    "description": "Welcome to M0d3rN Healthcare"}' "https://platform.pokitdok.com/api/v4/schedule/appointments/ef987691-0a19-447f-814d-f8f3abbf4859"
```

```python
client.book_appointment('ef987691-0a19-447f-814d-f8f3abbf4859', {
    "patient": {
        "_uuid": "500ef469-2767-4901-b705-425e9b6f7f83",
        "email": "john@hondoe.com",
        "phone": "800-555-1212",
        "birth_date": "1970-01-01",
        "first_name": "John",
        "last_name": "Doe",
        "member_id": "M000001"
    },
    "description": "Welcome to M0d3rN Healthcare"
})
```

```csharp
 client.bookAppointment(
    "ef987691-0a19-447f-814d-f8f3abbf4859",
    new Dictionary<string, object> {
        {"patient", new Dictionary<string, object> {
            {"uuid", "500ef469-2767-4901-b705-425e9b6f7f83"},
            {"email", "john@johndoe.com"},
            {"phone", "800-555-1212"},
            {"birth_date", "1970-01-01"},
            {"first_name", "John"},
            {"last_name", "Doe"},
            {"member_id", "M000001"}}}
    });
```

```ruby
client.book_appointment('ef987691-0a19-447f-814d-f8f3abbf4859', {
    "patient": {
        "_uuid": "500ef469-2767-4901-b705-425e9b6f7f83",
        "email": "john@hondoe.com",
        "phone": "800-555-1212",
        "birth_date": "1970-01-01",
        "first_name": "John",
        "last_name": "Doe",
        "member_id": "M000001"
    },
    "description": "Welcome to M0d3rN Healthcare"
})
```

```java
StringBuffer buf = new StringBuffer();
buf.append("{");
buf.append("\"patient\": {");
buf.append("    \"_uuid\": \"500ef469-2767-4901-b705-425e9b6f7f83\",");
buf.append("    \"email\": \"john@hondoe.com\",");
buf.append("    \"phone\": \"800-555-1212\",");
buf.append("    \"birth_date\": \"1970-01-01\",");
buf.append("    \"first_name\": \"John\",");
buf.append("    \"last_name\": \"Doe\",");
buf.append("    \"member_id\": \"M000001\"");
buf.append("},");
buf.append("\"description\": \"Welcome to M0d3rN Healthcare\"");
buf.append("}");

JSONObject query = (JSONObject) JSONValue.parse(buf.toString());
Map<String, Object> results = client.bookAppointment("ef987691-0a19-447f-814d-f8f3abbf4859", query);
```

> Response:

```json
{
    "appointment_id": "IIJBNRGBKMGC",
    "appointment_type": "OV1",
    "patient": {
      "first_name": "John",
      "last_name": "Doe",
      "_uuid": "500ef469-2767-4901-b705-425e9b6f7f83",
      "phone": "800-555-1212",
      "member_id": "M000001",
      "birth_date": "1970-01-01",
      "email": "john@hondoe.com"
    },
    "booked": true,
    "description": "Welcome to M0d3rN Healthcare",
    "provider_scheduler_uuid": "e781c97c-8535-11e4-b0b3-0800272e8da1",
    "start_date": "2014-12-16T15:12:09.176207",
    "end_date": "2014-12-16T16:12:09.176215"
}
```

> Example scheduling request to update an appointment description:

```shell
curl -s -XPUT -H "Authorization: Bearer $ACCESS_TOKEN" -H "Content-Type: application/json" -d '{"description": "Welcome to M0d3rN Healthcare"}' "https://platform.pokitdok.com/api/v4/schedule/appointments/ef987691-0a19-447f-814d-f8f3abbf4859"
```

```python
client.book_appointment('ef987691-0a19-447f-814d-f8f3abbf4859', {"description": "Welcome to M0d3rN Healthcare"})
```

```ruby
client.book_appointment('ef987691-0a19-447f-814d-f8f3abbf4859', { "description": "Welcome to M0d3rN Healthcare" })
```

```csharp
 client.updateAppointment(
            "ef987691-0a19-447f-814d-f8f3abbf4859",
            new Dictionary<string, object> {
                {"description", "Welcome to M0d3rN Healthcare"}
            });
```

```java
HashMap<String, String> query = new HashMap<String, String>();
query.put("description", "Welcome to M0d3rN Healthcare");

client.book_appointment('ef987691-0a19-447f-814d-f8f3abbf4859', query);
```

> Response:

```json
{
    "appointment_id": "AAMWKTXGVGWB",
    "appointment_type": "OV1",
    "booked": false,
    "description": "Welcome to M0d3rN Healthcare",
    "provider_scheduler_uuid": "956a9e10-8536-11e4-ba5d-0800272e8da1",
    "start_date": "2014-12-16T15:17:00.948099",
    "end_date": "2014-12-16T16:17:00.948117"
}
```

> Example scheduling request to cancel an appointment:

```shell
curl -i -XDELETE -H "Authorization: Bearer $ACCESS_TOKEN"  "https://platform.pokitdok.com/api/v4/schedule/appointments/ef987691-0a19-447f-814d-f8f3abbf4859"
```

```python
client.cancel_appointment('ef987691-0a19-447f-814d-f8f3abbf4859')
```

```ruby
client.cancel_appointment('ef987691-0a19-447f-814d-f8f3abbf4859')
```

```csharp
client.cancelAppointment("ef987691-0a19-447f-814d-f8f3abbf4859");
```

```java
client.cancelAppointment("ef987691-0a19-447f-814d-f8f3abbf4859");
```

*Available modes of operation: real-time*

The PokitDok Scheduling API performs schedule aggregation to multiple third party scheduling
applications, typically commercial off-the-shelf Practice Management (PM) software, for private
practices, provider networks, hospital systems, etc. The PokitDok Scheduling API also provides a
built-in scheduling system for providers without a PM. The API provides consumers a means to
schedule appointments in a manner independent of the provider's PM system. OAuth scopes are used to
restrict access to provider's PM systems and user's personal information.

Available Scheduling Endpoints:

| Endpoint                            | HTTP Method | Description                                                                                       | Scope                     | 
|:------------------------------------|:------------|:--------------------------------------------------------------------------------------------------|:--------------------------|
| /schedule/schedulers/               | GET         | Get a list of supported scheduling systems and their UUIDs and descriptions.                      |                           |
| /schedule/schedulers/{uuid}         | GET         | Retrieve the data for a specified scheduling system.                                              |                           |
| /schedule/appointmenttypes/         | GET         | Get a list of appointment types, their UUIDs, and descriptions.                                   |                           |
| /schedule/appointmenttypes/{uuid}   | GET         | Retrieve the data for a specified appointment type.                                               |                           |

The /schedule/schedulers response includes the following fields:

| Field            | Type           | Description                                             |
|:-----------------|:---------------|:--------------------------------------------------------|
| scheduler_uuid   | {uuid}         | The scheduler's unique identifier.                      |
| name             | {string}       | The name of the provider.                               |
| description      | {string}       | Brief description of the scheduling system.             |

The /schedule/appointmenttypes/ response includes the following fields:

| Field                   | Type           | Description                                                                        |
|:------------------------|:---------------|:-----------------------------------------------------------------------------------|
| appointment_type_uuid   | {uuid}         | The appointment type unique identifier.                                            |
| scheduler_uuid          | {uuid}         | The scheduler's unique identifier.                                                 |
| type                    | {string}       | The appointment type used to identify a specific appointment procedure/category.   |
| description             | {string}       | Brief description of the appointment.                                              |
| category_id             | {string}       | The category identifier associated with the appointment type                       |
| duration                | {int}          | Duration of the appointment in minutes.                                            |


| Endpoint                            | HTTP Method | Description                                                                                       | Scope                     | 
|:------------------------------------|:------------|:--------------------------------------------------------------------------------------------------|:--------------------------|
| /schedule/patient/                  | POST        | Registers an existing PokitDok user as a patient within a provider's scheduling system.           | user_schedule             |

The /schedule/patient/ endpoint accepts the following parameters:

| Parameter        | Type           | Description                                                                           |
|:-----------------|:---------------|:--------------------------------------------------------------------------------------|
| pd_patient_uuid  | {uuid}         | The PokitDok unique identifier for the user record.                                   |
| pd_provider_uuid | {uuid}         | The PokitDok unique identifier for the provider record.                               |
| location         | {geo-location} | The geo-location of the provider's physical address, formatted [latitude, longitude]. |

The /schedule/patient/ endpoint response returns a patient [object](#scheduling_patient_object).

| Endpoint                              | HTTP Method | Description                      | Scope                                                                             |
|:--------------------------------------|:------------|:---------------------------------|:----------------------------------------------------------------------------------|
| /schedule/slots/                      | POST        | Creates an open scheduling slot. | business_schedule                                                                 |
| /schedule/slots/{pd_appointment_uuid} | DELETE      | Deletes an open scheduling slot. | business_schedule                                                                 |

The /schedule/slots/ POST endpoint accepts the following parameters:

| Parameter        | Type           | Description                                                                           |
|:-----------------|:---------------|:--------------------------------------------------------------------------------------|
| pd_provider_uuid | {uuid}         | The PokitDok unique identifier for the provider record.                               |
| location         | {geo-location} | The geo-location of the provider's physical address, formatted [latitude, longitude]. |
| appointment_type | {string}       | The "appointment_type" used to identify a specific appointment procedure/category.    |
| start_date       | {datetime}     | The beginning date and UTC time of the appointment query, formatted as ISO8601.       |
| end_date         | {datetime}     | The ending date and UTC time of the appointment query, formatted as ISO8601.          |

| Endpoint                                      | HTTP Method | Description                                                                                                                                       | Scope          |
|:----------------------------------------------|:------------|:--------------------------------------------------------------------------------------------------------------------------------------------------|:---------------|
| /schedule/appointments/                       | GET         | Query for open appointment slots (using pd_provider_uuid and location) or booked appointments (using patient_uuid) given query parameters.        | user_schedule  |
| /schedule/appointments/{pd_appointment_uuid}  | GET         | Query for an open appointment slot or a booked appointment given a specific {pd_appointment_uuid}, the (PokitDok unique appointment identifier).  | user_schedule  |
| /schedule/appointments/{pd_appointment_uuid}  | PUT         | Book appointment for an open slot. Post data contains patient attributes and description.                                                         | user_schedule  |
| /schedule/appointments/{pd_appointment_uuid}  | PUT         | Update appointment description.                                                                                                                   | user_schedule  |
| /schedule/appointments/{pd_appointment_uuid}  | DELETE      | Cancel appointment given its {pd_appointment_uuid}.                                                                                               | user_schedule  |

The /schedule/appointments/ endpoint accepts the following parameters:

| Field            | Type           | Description                                                                                                                     |
|:-----------------|:---------------|:--------------------------------------------------------------------------------------------------------------------------------|
| appointment_type | {string}       | The "appointment_type" used to identify a specific appointment procedure/category.                                              |
| start_date       | {datetime}     | The beginning date and UTC time of the appointment query, formatted as ISO8601.                                                 |
| end_date         | {datetime}     | The ending date and UTC time of the appointment query, formatted as ISO8601.                                                    |
| patient_uuid     | {uuid}         | The PokitDok unique identifier for the patient that has booked an appointment.                                                  |
| pd_provider_uuid | {uuid}         | The PokitDok unique identifier for the provider that has an open appointment slot.                                              |
| location         | {geo-location} | The geo-location of the physical address where the provider that has an open appointment slot, formatted [latitude, longitude]. |

The /schedule/appointments/{pd_appointment_uuid} endpoint for booking an appointment accepts the following parameters:

| Field                   | Type           | Description                                                                                    |
|:------------------------|:---------------|:-----------------------------------------------------------------------------------------------|
| pd_appointment_uuid     | {uuid}         | The PokitDok unique identifier for the appointment.                                            |
| booked                  | {boolean}      | Whether or not the appointment has been booked.                                                |
| patient                 | {object}       | Patient associated with the appointment. Uses the patient [object](#scheduling_patient_object).| 
| description             | {string}       | Brief description of the appointment.                                                          |

The /schedule/appointments/{pd_appointment_uuid} endpoint for updating an appointment description accepts the following parameters:

| Field                   | Type           | Description                                                                                    |
|:------------------------|:---------------|:-----------------------------------------------------------------------------------------------|
| pd_appointment_uuid     | {uuid}         | The PokitDok unique identifier for the appointment.                                            |
| description             | {string}       | Brief description of the appointment.                                                          |

Both the /schedule/slots/ (POST) and /schedule/appointments (GET/PUT) endpoints' response includes the following fields:

| Field                   | Type           | Description                                                                                    |
|:------------------------|:---------------|:-----------------------------------------------------------------------------------------------|
| pd_appointment_uuid     | {uuid}         | The PokitDok unique identifier for the appointment.                                            |
| provider_scheduler_uuid | {string}       | The provider's scheduler unique identifier.                                                    |
| appointment_id          | {string}       | The appointment identifier.                                                                    | 
| appointment_type        | {string}       | The "appointment_type" used to identify a specific appointment procedure/category.             |
| start_date              | {datetime}     | The beginning date and UTC time of the appointment query, formatted as ISO8601.                |
| end_date                | {datetime}     | The ending date and UTC time of the appointment query, formatted as ISO8601.                   |
| booked                  | {boolean}      | Whether or not the appointment has been booked.                                                |
| patient                 | {object}       | Patient associated with the appointment. Uses the patient [object](#scheduling_patient_object).| 
| description             | {string}       | Brief description of the appointment.                                                          |


<a name="scheduling_patient_object"></a>
###Patient object:

| Field            | Type           | Description                                             |
|:-----------------|:---------------|:--------------------------------------------------------|
| uuid             | {uuid}         | The patient's unique identifier.                        |
| email            | {email}        | The patient's email.                                    |
| phone            | {string}       | The patient's phone number.                             |
| birth_date       | {date}         | The patient's date of birth.                            |
| first_name       | {string}       | The patient's first name.                               |
| last_name        | {string}       | The patient's last name.                                |
| member_id        | {string}       | The patient's member id.                                |

