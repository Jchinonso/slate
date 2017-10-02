# Errors

The PostIt API uses the following error codes:


Error Code | Meaning
---------- | -------
400 | Bad Request --  You sent invalid url parameters.
401 | Unauthorized -- You are not authenticated or authentication fails.
403 | Forbidden -- You are not a member of the group you are trying to access 
    |        or you tried to perform an operation that can only be done by the creator of the group.
404 | Not Found -- The specified User or Group could not be found..
500 | Internal Server Error -- We had a problem with our server. Try again later.

