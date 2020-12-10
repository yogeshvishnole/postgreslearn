## JOins and aggregations

When to use join

When need data from multiple tables then think of using join.

when to use aggregation

When we need a single value derived from lot of data then we use aggregation.
example --> when we have to find average.

First join query
`SELECT contents,username FROM comments JOIN users ON users.id = comments.user_id`
