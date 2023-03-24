# eRezLife Public API Documentation

This repository contains documentation overviewing eRezLife's Public APIs. Here
you will find explainations on each endpoint, as well as Postman Collection
that will showcase how each endpoint can be used.

## Authentication

All of the eRezLife Public APIs can be accessed using an API Key. Keys can be
obtained by submitting a request to service@erezlife.com.

This key will be contained in the header of all requests to the API endpoints,
as a `x-api-key`. 

Example in cURL:

```
curl --location 'https://example.erezlife.com/api/housing/assignment/' \
--header 'x-api-key: THISISANEXAMPLEKEY'
```

## Endpoints

* [Housing assignments](housing/assignment.md) : `GET /api/housing/assignment/`
* [Housing assignment changelogs](housing/changelog.md) : `GET /api/housing/changelog/`
* [Meal plan assignments](meal-plan/assignment.md) : `GET /api/meal-plan/assignment/`
* [Meal plan assignment changelogs](meal-plan/changelog.md) : `GET /api/meal-plan/changelog/`
* [(In development) Financial line item changelog](financials/line-item-changelog.md) : `GET /api/financials/line-item/changelog/`

## Postman Collection

The Postman Collection found in this directory shows how each endpoint can be
used. Simply install Postman, and import the Collection. After importing,
update the variables to use your eRezLife URL and your API Key. 
