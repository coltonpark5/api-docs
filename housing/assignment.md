# Housing assignments

`GET /api/housing/assignment/`

By default, this end point will return all housing assignments for your current
and future sessions in eRezLife. You can use the various filters detailed below
to return other past sessions, or return assignments for only a specific session
or student.

### Example output

```json
{
    "pages": [
        {
            "page": 1,
            "url": "/api/housing/assignment/?page=1"
        }
    ],
    "item_count": 1,
    "content": [
        {
            "session_id": "FA2023",
            "student_id": "EREZ0009",
            "email": "demosite+EREZ0009@erezlife.com",
            "application_status": "accepted offer",
            "start_date": "2023-08-15",
            "end_date": "2023-12-31",
            "building_id": "CH",
            "room_id": "105",
            "price_type_id": "TRAD_DB_BATH"
        }
    ]
}
```

### Field descriptions

`session_id` : The external id of the session as configured in eRezLife.
`student_id` : The primary key for the student commonly called "student id"
`email` :  The email address of the student.
`application_status` : The application status for the returned assignment.
`start_date` : The reservation start date of the assignment.
`end_date` :  The reservation end date of the assignment.
`building_id`: The external id for the building that the student is assigned.
`room_id` : The external id for the room that the student is assigned.
`price_type_id` : The external id for the price type of the assignment.

## Filtering the returned data.

There are several different filters that can be included as part of your API
request to this end point. None of them are required, but you can use any
combination of them for your request. 

### Pagination

If there are over 500 records for your API request, the data returned will be
paginated. The returned json will always contain all possible pages and their
URLs if the request is large enough to require pagination. 

`https://example.erezlife.com/api/housing/assignment/?page=1`

### Student ID

By passing a student id in your request, the API will return all assignments
for that student.

`https://example.erezlife.com/api/housing/assignment/?student_id=EREZ0007`

### Session ID

By passing a session id in your request, the API will return all assignments
for any Sessions with that external id.

`https://example.erezlife.com/api/housing/assignment/?page=1&session_id=FALL2023`

### Session dates

By passing session dates, the API will return all assignments for any sessions
whose occupancy dates are part of the data range. 

If you only pass a `session_start_date` the API will return sessions and their
assignments for that date and beyond. 

If you only pass a `session_end_date` the API will return sessions and their
assignments that date and all sessions prior.

If you pass both dates, the API will return sessions and their assignments that
overlap with these dates.

`https://example.erezlife.com/api/housing/assignment/?page=1&session_start_date=2023-08-30&session_end_date=2023-12-29`
