# Housing assignment change log

`GET /api/housing/changelog/`

This end point will return details of any new, changes, or removals of housing
assignments that occurred prior to the timestamp that you pass as part of the
request. The timestamp is a required field. 

This end point required new updates to eRezLife to ensure that all changes
would be captured. As a result, all historical change data is not available.
The endpoint will only return sessions that have history logs after the release
date of PUBLISHDATE.

### Required argument - timestamp

All requests to this endpoint must include `timestamp`.

`https://example.erezlife.com/api/housing/changelog/?timestamp=2023-05-01T00:00:00+00:00`

### Example output

```json
{
    "pages": [
        {
            "page": 1,
            "url": "/api/housing/changelog/?page=1&timestamp=2023-01-21T21%3A35%3A46.606%2B00%3A00"
        }
    ],
    "item_count": 1,
    "content": [
        {
            "session_id": "FALL23",
            "student_id": "EREZ0018",
            "email": "demosite+EREZ0018@erezlife.com",
            "start_date": "2023-08-14",
            "end_date": "2023-12-30",
            "building_id": "SA",
            "room_id": "103B2",
            "price_type_id": "APT_DB",
            "timestamp": "2023-03-15T15:19:02.796+00:00",
            "change_type": "ADD"
        }
    ]
}
```

### Field descriptions

`session_id` : The external id of the session as configured in eRezLife.
`student_id` : The primary key for the student commonly called "student id"
`email` :  The email address of the student.
`start_date` : The reservation start date of the assignment.
`end_date` :  The reservation end date of the assignment.
`building_id`: The external id for the building that the student is assigned.
`room_id` : The external id for the room that the student is assigned.
`price_type_id` : The external id for the price type of the assignment.
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

`https://example.erezlife.com/api/housing/assignment/?page=1&timestamp=2023-01-21T21%3A35%3A46.606%2B00%3A00`

### Student ID

By passing a student id in your request, the API will return all assignments
for that student.

`https://example.erezlife.com/api/housing/assignment/?timestamp=2023-01-21T21%3A35%3A46.606%2B00%3A00&student_id=EREZ0007`

### Session ID

By passing a session id in your request, the API will return all assignments
for any Sessions with that external id.

`https://example.erezlife.com/api/housing/assignment/?timestamp=2023-01-21T21%3A35%3A46.606%2B00%3A00&session_id=FALL2023`
