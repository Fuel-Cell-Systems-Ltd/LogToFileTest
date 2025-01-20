# BeckhoffLogging
A application to run from beckhoff to expand logging using REST:API

---
<br> <br> <br>

# Example Schemas for Logging and Data Transmission

## ProcessValveData (Cyclic, 1s Update)
JSON format for sending process values every second (gzip compression recommended for performance and bandwidth optimization):

```json
{
  "timestamp": "2024-12-24T10:00:00Z",
  "Values": [
    { "k": "PT01", "v": 10.5 },
    { "k": "PT02", "v": 12.3 },
    { "k": "PT03", "v": 9.8 },
    { "k": "PT04", "v": 11.0 },
    { "k": "PT05", "v": 13.4 }
  ]
}
```

# ApplicationLogs
Buffered, asynchronous log messages:

```json
{
  "timestamp": "2024-12-24T10:01:00Z",
  "k": "Error",
  "v": "An error occurred during bootup: LINE 53"
}
```

# AlarmLogs
Buffered, asynchronous alarm events:

```json
[
  {
    "timestamp": "2024-12-24T10:02:00Z",
    "k": "Raised",
    "v": "PT-05 warning raised, value: 5555"
  },
  {
    "timestamp": "2024-12-24T10:03:00Z",
    "k": "Cleared",
    "v": "PT-05 warning cleared"
  },
  {
    "timestamp": "2024-12-24T10:04:00Z",
    "k": "System",
    "v": "Clear all alarms pressed"
  }
]
```

# UserAuditLogs
Buffered, asynchronous user activity logs (consider emphasizing the use of encryption, e.g., HTTPS or data encryption, to ensure data confidentiality and integrity during transmission, particularly for protecting sensitive information like user login activities and password changes):

```json
[
  {
    "timestamp": "2024-12-24T10:05:00Z",
    "k": "LogOn",
    "v": "User 1235 has logged on"
  },
  {
    "timestamp": "2024-12-24T10:06:00Z",
    "k": "LogOff",
    "v": "User 1235 has logged off"
  },
  {
    "timestamp": "2024-12-24T10:07:00Z",
    "k": "PwdChange",
    "v": "User 1235 has changed password"
  }
]
```

# RefuellingData
Details of a refuelling session (consider recommending encryption, e.g., HTTPS or data encryption, to ensure data confidentiality and integrity during transmission, particularly for user and cost-related details):

```json
{
  "timestamp": "2024-12-24T10:08:00Z",
  "Details": [
    { "k": "User", "v": "1234" },
    { "k": "Amount", "v": 32 },
    { "k": "Price", "v": 15.2 },
    { "k": "Cost", "v": 152 },
    { "k": "Complete", "v": true }
  ]
}
```

# Comments on Improvements

## Consistency in Timestamp:

Using timestamp with ISO 8601 ensures standardized time representation across systems. This format avoids ambiguity, supports internationalization, and ensures compatibility across various programming languages and systems.

## Key-Value Pair for Flexibility:

The use of k and v makes the schema extensible and adaptable to new attributes without modifying the structure.

## Buffering Logs:

Logs are buffered for asynchronous transmission, optimizing network usage and improving system performance.

## RESTful API Integration:

These schemas align with REST principles, making it straightforward to integrate with RESTful endpoints.

## Scalability:

The structured format supports horizontal scaling, making it easier to handle increased data loads.

# Suggestions for Further Improvements

## Validation: 
Implement schema validation at the API level to ensure data consistency and guard against malformed input.

## Compression:
Gzip compression is recommended for high-frequency data like process values to optimize bandwidth and reduce latency. This can be set via the FB_IotHttpRequest function block in Beckhoff TF6760.

## Error Handling: 
Include fields for error codes, statuses, and recovery steps in logs to improve debugging and maintainability.

# Other
Add a basic page to allow debug
Add a reset with auth
Add a shutdown with auth
Add a check to the PLC [log start, stop, PLC not ON].
Add a check from the PLC


## Security: 
Always use HTTPS or equivalent encryption for all log transmissions, particularly for sensitive logs such as audit and refuelling data, to ensure data confidentiality, integrity, and protection against interception.

## Standardization: 
Define a common schema repository or documentation for all JSON payloads to ensure consistency across teams and systems


# Other
Add Home page for debug
Add shutdown with auth
Add restart with auth
Add check to PLC [Log start, stop, pause, PLC not running]
Add check from PLC

Add in setting, log when and what changed
add in user auth, returns role, name, price
