# API

The Universal API can be used to manage the platform from any compatible REST client. You will need a valid App Token to access the API.

## Invoking the API

To invoke the API, you can send an HTTP request with the Bearer token set for authorization.

```powershell
Invoke-RestMethod http://localhost:5000/api/v1/script -Headers @{ Authorization = "Bearer myAppToken" }
```

## API Documentation

You can access the API documentation by navigating to Security \ Tokens  and click the API Documentation button.&#x20;

The URL for the API documentation can be found at the following location. You will need to be authenticated before accessing this URL: `http://localhost:5000/swagger/index.html`
