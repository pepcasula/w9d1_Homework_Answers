# Homework: Full Stack Games Hub App

### Questions

1. What is responsible for defining the routes of the `games` resource?

        The server app: in server.js, app.use('api/games) defines the route.

2. What do you notice about the folder structure?  Whats the client responsible for? Whats the server responsible for?

        A server app runs in the 'server' folder, while the client app files are into 'client'.
        The client sends GET requests to render the game cards through GamesGrid(>GamesCard) when the app initialises, and whenever the 'games' state changes. The server processes the requests and passes them to the db via the 'games' route. The db sends the data requested to the server, and then the data are sent back to the client app for rendering in the browser.
        When new documents are passed through the client form (GamesForm component) with a POST request, the server communicates with the db to pass a new 'game' object. Then a response is sent back to the server, and the server passes it to the client for rendering through the GamesGrid(>GamesCard) component.

3. What are the the responsibilities of server.js?

        Mamaging the client requests (GET/POST) and send them to the db so the data can be retrieved for rendering or passed to be added as a new 'game' object of the collection (and this will trigger a response sending updated data for rendering).

4. What are the responsibilities of the `gamesRouter`?

        It defines the routes for the server app to communicate with the db through the Mongo driver.

5. What process does the the client (front-end) use to communicate with the server?

        The following two processes in GamesContainer.js:
        1. 'createGame', called by 'GameForm', sends a POST request to the server to add a new 'savedGame' to the db.
        2. 'GamesService.getGames()' is called by the useEffect hook to send a GET request for rendering when the app initialises,
            and whenever a new instance is added to the collection in the db so that an updated list of game cards can be rendered.

6. What optional second argument does the `fetch` method take? And what is it used for in this application? Hint: See [Using Fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch) on the MDN docs

        An init object. This allows to specify the options to use when initialising the fetch method. In this application, the GamesService method 'postGame()' includes this argument in order to specify what 'method' we're passing (POST), the type of content (in 'headers': application/json) and the object data type(in 'body': a JSON string).

7. Which of the games API routes does the front-end application consume (i.e. make requests to)?

        /api/games

8. What are we using the [MongoDB Driver](http://mongodb.github.io/node-mongodb-native/) for?

        So we can store, retrieve and manage no matter how large amounts of data and still maintain the application readable with DRY code. 

## Extension

Why do we need to use [`ObjectId`](https://mongodb.github.io/node-mongodb-native/api-bson-generated/objectid.html) from the MongoDB driver?

        To create a unique ID for every new object instance.