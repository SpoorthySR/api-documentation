# Errors



Latlong API gives below specified error codes depending on the criteria:


Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request sucks
401 | Unauthorized -- Your access_token is wrong or expired
403 | Forbidden -- The api requested is hidden for administrators only
404 | Not Found -- The specified resource could not be found
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarially offline for maintanance. Please try again later.
