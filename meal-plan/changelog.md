# Meal plan assignment change log

`GET /api/meal-plan/changelog/`

This end point will return details of any new, changes, or removals of
meal-plan assignments that occurred prior to the timestamp that you pass as
part of the request. The timestamp is a required field. 

This end point required new updates to eRezLife to ensure that all changes
would be captured. As a result, all historical change data is not available.
The endpoint will only return sessions that have history logs after the release
date of PUBLISHDATE.

### Required argument - timestamp

All requests to this endpoint must include `timestamp`.

`https://example.erezlife.com/api/meal-plan/changelog/?timestamp=2023-05-01T00:00:00+00:00`

### Example output

```json
{
    "pages": [
        {
            "page": 1,
            "url": "/api/meal-plan/changelog/?timestamp=2023-05-01T00:00:00+00:00"
        }
    ],
    "item_count": 1,
    "content": [
        {
            "student_id": "EREZ0009",
            "session_id": "FA2023",
            "email": "demosite+EREZ0009@erezlife.com",
            "meal_plan_id": "19MEALS"
            "start_date": "2023-08-15",
            "end_date": "2023-12-31",
            "timestamp": "2023-03-15T15:19:02.796+00:00",
            "change_type": "ADD"
        }
    ]
}
```

### Field descriptions

`student_id` : The primary key for the student commonly called "student id"
`session_id` : The external id of the session as configured in eRezLife.
`email` :  The email address of the student.
`meal_plan_id` : The external id for the meal plan of the assignment.
`start_date` : The reservation start date of the assignment.
`end_date` :  The reservation end date of the assignment.
`timestamp` : The timestamp of this log.
`change_type` : Contains ADD, UPDATE, or REMOVE depending on the state of this change.

## Filtering the returned data.

There are several different filters that can be included as part of your API
request to this end point. None of them are required, but you can use any
combination of them for your request. 

### Pagination

If there are over 500 records for your API request, the data returned will be
paginated. The returned json will always contain all possible pages and their
URLs if the request is large enough to require pagination. 

`https://example.erezlife.com/api/meal-plan/changelog/?timestamp=2023-05-01T00:00:00+00:00&page=1`

### Student ID

By passing a student id in your request, the API will return all assignments
for that student.

`https://example.erezlife.com/api/meal-plan/changelog/?timestamp=2023-05-01T00:00:00+00:00&student_id=EREZ0007`

### Session ID

By passing a session id in your request, the API will return all assignments
for any Sessions with that external id.

`https://example.erezlife.com/api/meal-plan/changelog/?timestamp=2023-05-01T00:00:00+00:00&page=1&session_id=FALL2023`
