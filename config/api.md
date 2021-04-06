# API

The Universal API can be used to manage the platform from any compatible REST client. You will need a valid App Token to access the API.

## Invoking the API

To invoke the API, you can send an HTTP request with the Bearer token set for authorization.

```text
Invoke-RestMethod http://localhost:5000/api/v1/script -Headers @{ Authorization = "Bearer myAppToken" }
```

## API Documentation

API documentation is provided as interactive Swagger documentation that you can access directly within your Universal instance. The URL for the Swagger documentation can be found at: `http://localhost:5000/swagger/index.html`

