# BUG-001 | Incorrect Status Code on DELETE

## Title

DELETE endpoint returns wrong status code

## Severity

High

## Steps to Reproduce

1. Send DELETE request to:
   https://reqres.in/api/users/999

## Expected Result

Server returns:
200 OK or proper error message

## Actual Result

404 Not Found with empty body
