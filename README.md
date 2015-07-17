## Requesting Remote Help

We send the Server the url of our media,
and the hook where we wish to receive the events.

- Request:
    - URL: `server.com/api/help/image`
    - Type: `POST`
    - Content:

    ```javascript
    {
            "media": {
                "type": url | raw,
                "content": any
            },
            "eventsURL": url
    }
    ```

The server responds with the unique URL served to the user,
and a specific 'done' route where the server is listening,
waiting for us to hit him in that route
to signal that the helping job is done.

- Response:
    - Status: `200`
    - Body:

        ```javascript
        {
            "userURL": url,
            "doneURL": url
        }
        ```

## Sending events to the client

- Request:
    - URL: `eventsURL`
    - Type: `POST`
    - Body:

    ```javascript
    {
        "type": String,
        "content": {},
        "timestamp": Integer
    }
    ```

- Response:
    - Status: `100`

## Telling the Server that we are done

- Request:
    - URL: `doneURL`
    -  Type: `POST`
    -  Body:

    ```javascript
    {
        "authURL": userUrl
    }
    ```

- Response:
    - Status: `200` | `403`