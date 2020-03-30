# Errors

The Mekari Payment API uses the following error codes:

Status | Name | Description
---------- | ------- | ------
401 | Unauthorized | Your API key is wrong.
403 | Forbidden | You are not authorized to make the request.
404 | RecordNotFound | The specified record could not be found.
422 | RecordInvalid | You're inputs failing validation.
500 | InternalServerError | We had a problem with our server. Try again later.
