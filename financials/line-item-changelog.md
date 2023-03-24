# Financial line items change log (Currently in development)

`GET /api/financials/line-item/changelog/`

Currently in development is the functionality to have eRezLife generate
financial charges for housing and meal plan assignments.

This end point will return details of any line items created since the
timestamp passed as part of the request. The timestamp is a required field. 

### Required argument - timestamp

All requests to this endpoint must include `timestamp`.

`https://example.erezlife.com/api/financials/line-item/changelog/?timestamp=2023-03-23T00:00:00+00:00`

### Example output

```json
{
    "pages": [
        {
            "page": 1,
            "url": "/api/financials/line-item/changelog/?timestamp=2023-03-23T00%3A00%3A00.000-00%3A00&page=1"
        }
    ],
    "item_count": 2,
    "content": [
        {
            "student_id": "EREZ0055",
            "session_id": "FALL23",
            "meal_plan": "ALLMEALS",
            "price_type": null,
            "due_date": "2023-08-01",
            "description": "Unlimited Meal Plan Fee",
            "amount": "2500.00",
            "line_item_id": 20,
            "timestamp": "2023-03-24T18:20:29.926+00:00"
        },
        {
            "student_id": "EREZ0055",
            "session_id": "FALL23",
            "meal_plan": null,
            "price_type": "TH_DOUBLE",
            "due_date": "2023-08-01",
            "description": "Double Room Fee",
            "amount": "6500.00",
            "line_item_id": 21,
            "timestamp": "2023-03-24T18:20:52.979+00:00"
        }
    ]
}
```

### Field descriptions

`student_id` : The primary key for the student commonly called "student id"
`session_id` : The external id of the session as configured in eRezLife.
`meal_plan` : If the item is related to a meal plan, this contains the external id for that meal plan.
`price_type` : If the item is related to a housing assignment, this contains the external id for that price type.
`due_date` : The due date set for this line item.
`description` : The description set for this line item on the payment schedule.
`amount` : The dollar amount of the line item.
`line_item_id` : A unique identifier for this line item.
`timestamp` : The timestamp of this item.

## Filtering the returned data.

There are several different filters that can be included as part of your API
request to this end point. None of them are required, but you can use any
combination of them for your request. 

### Pagination

If there are over 500 records for your API request, the data returned will be
paginated. The returned json will always contain all possible pages and their
URLs if the request is large enough to require pagination. 

`https://example.erezlife.com/api/financials/line-item/changelog/?timestamp=2023-03-23T00:00:00+00:00&page=1`

### Student ID

By passing a student id in your request, the API will return just items
for that student.

`https://example.erezlife.com/api/financials/line-item/changelog/?timestamp=2023-03-23T00:00:00+00:00&student_id=EREZ0007`

### Session ID

By passing a session id in your request, the API will return just items
for any Sessions with that external id.

`https://example.erezlife.com/api/financials/line-item/changelog/?timestamp=2023-03-23T00:00:00+00:00&session_id=FALL2023`

### Session dates

By passing session dates, the API will return only line items for any sessions
whose occupancy dates are part of the data range. 

If you only pass a `session_start_date` the API will return sessions and their
items for that date and beyond. 

If you only pass a `session_end_date` the API will return sessions and their
items that date and all sessions prior.

If you pass both dates, the API will return sessions and their items that
overlap with these dates.

`https://example.erezlife.com/api/financials/line-item/changelog/?timestamp=2023-03-23T00:00:00+00:00&session_start_date=2023-08-30&session_end_date=2023-12-29`
