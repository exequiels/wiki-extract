# HTTP Status Code Guide

### Table of Contents

- [Successful Responses (2xx)](#successful-responses-2xx)
- [Client Error Codes (4xx)](#client-error-codes-4xx)
- [Server Error Codes (5xx)](#server-error-codes-5xx)
- [Authentication and Authorization Errors](#authentication-and-authorization-errors)
- [Best Practices](#best-practices)

## Successful Responses (2xx)

### Common 2xx Status Codes

- `200 OK`:

  - Standard successful HTTP response
  - Indicates the request was successful
  - Most common successful response code
  - Used for GET, PUT, PATCH, and DELETE requests that complete successfully

- `201 Created`:

  - Successful resource creation
  - Typically used after POST requests
  - Server has fulfilled the request and created a new resource
  - Often includes the location of the newly created resource in the response headers

- `204 No Content`:
  - Successful request with no content to return
  - Often used for DELETE operations
  - Indicates the server has successfully processed the request
  - No response body is sent back

#### Example Response Structure Best Practices

```json
{
  "status": "success",
  "code": 200,
  "data": {
    "message": "Request processed successfully",
    "resource": {}
  }
}
```

### Common Use Cases

- `200 OK`: Retrieving data, updating existing resources
- `201 Created`: Creating new database entries, user registrations
- `204 No Content`: Deleting resources, successful updates with no return data

## Client Error Codes (4xx)

### Common 4xx Error Codes

- `400`: Bad Request

  - Malformed request syntax
  - Invalid request message framing
  - Deceptive request routing

- `401`: Unauthorized

  - Authentication is required and has failed
  - No valid credentials provided

- `403`: Forbidden

  - Server understands the request
  - Refuses to authorize the request
  - User does not have necessary permissions

- `404`: Not Found

  - Requested resource cannot be found
  - No matching endpoint or resource exists

- `405`: Method Not Allowed

  - HTTP method not supported for the endpoint
  - Example: Using POST on a GET-only endpoint

- `410`: Gone
  - Resource has been permanently deleted
  - Indicates the resource is no longer available

## Server Error Codes (5xx)

### Common 5xx Error Codes

- `500`: Internal Server Error

  - Unexpected condition preventing request fulfillment
  - Generic server-side error message
  - Unhandled exceptions or programming errors

- `501`: Not Implemented

  - Server does not support the functionality needed
  - Feature or method not supported

- `502`: Bad Gateway

  - Invalid response from an upstream server
  - Proxy or gateway issues

- `503`: Service Unavailable

  - Server temporarily overloaded
  - Under maintenance
  - Temporary condition

- `504`: Gateway Timeout
  - Server did not receive timely response from upstream server
  - Connection timeout

## Authentication and Authorization Errors

### Error Code Usage Guidelines

- `401 (Unauthorized)`:

  - Use when authentication is required but has failed
  - No valid credentials provided
  - Authentication token is invalid or expired

- `403 (Forbidden)`:

  - Use when authentication exists
  - User does not have permission to access the resource
  - Authenticated but lacks necessary privileges

- `410 (Gone)`:
  - Specific semantic meaning
  - Resource permanently deleted
  - Should not be used for generic authentication errors

## Best Practices

### Error Handling Recommendations

- Use the most specific error code possible
- Provide clear, concise error messages
- Avoid exposing sensitive system details
- Log detailed error information server-side
- Return user-friendly error responses
- Implement consistent error response format

#### Example Error Response Format

```json
{
  "error": "Descriptive error message",
  "code": 401,
  "details": "Optional additional information"
}
```

#### Common Pitfalls to Avoid

- Using generic error codes
- Exposing system internals in error messages
- Inconsistent error handling across endpoints
- Not logging server-side errors
- Providing too much or too little error information
