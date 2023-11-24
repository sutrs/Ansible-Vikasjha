# Launch a Job Template with AWX Rest APIs
- Generate an authentication token by making below request:
Make sure you replace username and password's value to your awx username and password value.
```
curl --location 'http://192.168.1.19/api/v2/users/1/tokens/' \
--header 'Content-Type: application/json' \
--data '{"username": "admin", "password": "admin"}'
```

You are going to receive JSON response which contains token. Example is shown below:
```
{
    "id": 3,
    "type": "o_auth2_access_token",
    "url": "/api/v2/tokens/3/",
    "related": {
        "user": "/api/v2/users/1/",
        "activity_stream": "/api/v2/tokens/3/activity_stream/"
    },
    "summary_fields": {
        "user": {
            "id": 1,
            "username": "admin",
            "first_name": "",
            "last_name": ""
        }
    },
    "created": "2023-11-02T02:57:06.527444Z",
    "modified": "2023-11-02T02:57:06.540513Z",
    "description": "",
    "user": 1,
    "token": "**zzghA1107f5SbKovtqj5Gbrgtqm9dy**",
    "refresh_token": null,
    "application": null,
    "expires": "3023-03-05T02:57:06.523309Z",
    "scope": "write"
}
```


- Get list of job templates
Replace the bearer token with the token generated in previous steps.
```
curl --location 'http://192.168.1.19/api/v2/job_templates/' \
--header 'Authorization: Bearer _zzghA1107f5SbKovtqj5Gbrgtqm9dy_'
```

- Launch Job Tempalate

```
curl --location --request POST 'http://192.168.1.19/api/v2/job_templates/31/launch/' \
--header 'Authorization: Bearer _zzghA1107f5SbKovtqj5Gbrgtqm9dy_'
```
