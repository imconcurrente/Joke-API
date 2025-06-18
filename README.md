# Joke-API

**Description:**
JokeAPI is a RESTful web service built using Express.js. It manages a collection of jokes, offering various endpoints for adding, retrieving, updating, and deleting jokes. The API can be tested using Postman. 

**Implementation Details:**

1. **Setup and Dependencies:**
   - Uses Express.js to handle routing and middleware.
   - Body-parser middleware to parse incoming request bodies, particularly for POST and PUT requests.

   ```javascript
   import express from "express";
   import bodyParser from "body-parser";

   const app = express();
   const port = 3000;

   app.use(bodyParser.urlencoded({ extended: true }));
   ```

2. **Endpoints:**
   
   - **GET /random:** Returns a random joke from the jokes array.
   
     ```javascript
     app.get('/random', (req, res) => {
       const randomJoke = Math.floor(Math.random() * jokes.length);
       res.json(jokes[randomJoke]);
     });
     ```

   - **GET /jokes/:id:** Retrieves a joke by its ID.
   
     ```javascript
     app.get('/jokes/:id', (req, res) => {
       const userId = parseInt(req.params.id);
       const foundJoke = jokes.find((joke) => joke.id === userId);
       res.json(foundJoke);
     });
     ```

   - **GET /filter:** Retrieves jokes filtered by type using query parameters.
   
     ```javascript
     app.get('/filter', (req, res) => {
       const typeJoke = req.query.type;
       const filteredJokes = jokes.filter(joke => joke.jokeType === typeJoke);
       res.json(filteredJokes);
     });
     ```

   - **POST /jokes:** Adds a new joke to the collection.
   
     ```javascript
     app.post('/jokes', (req, res) => {
       const newJoke = {
         id: jokes.length + 1,
         jokeText: req.body.text,
         jokeType: req.body.type
       };
       jokes.push(newJoke);
       res.json(newJoke);
     });
     ```

   - **PUT /jokes/:id:** Replaces a joke’s text and type by its ID.
   
     ```javascript
     app.put('/jokes/:id', (req, res) => {
       const id = parseInt(req.params.id);
       const replacementJoke = {
        id :  id,
       jokeText = req.body.text,
       jokeType = req.body.type,
      };
       const searchIndex = jokes.findIndex((joke) => joke.id === id);
      jokes[searchIndex] = replacementJoke;
      res.json(replacementJoke);
     });
     ```

   - **PATCH /jokes/:id:** Partially updates a joke’s text or type by its ID.
   
     ```javascript
     app.patch('/jokes/:id', (req, res) => {
       const id = parseInt(req.params.id);
       const joke = jokes.find((joke) => joke.id === id);
       const replacementJoke = {
      id: id,
      jokeText: req.body.text || existingJoke.jokeText,
      jokeType: req.body.type || existingJoke.jokeType,
      };
       res.json(replacementJoke);
     });
     ```

   - **DELETE /jokes/:id:** Deletes a specific joke by its ID.
   
     ```javascript
     app.delete('/jokes/:id', (req, res) => {
       const userId = parseInt(req.params.id);
       const jokeIndex = jokes.findIndex(j => j.id === userId);

       if (jokeIndex > -1) {
         jokes.splice(jokeIndex, 1);
         res.sendStatus(200);
       } else {
         res.status(404).json({ error: `No jokes deleted!` });
       }
     });
     ```

   - **DELETE /all:** Deletes all jokes if the correct admin key is provided.
   
     ```javascript
     const masterKey = "enter_key_here";
     app.delete('/all', (req, res) => {
       if (req.query.key === masterKey) {
         jokes = [];
         res.sendStatus(200);
       } else {
         res.status(404).json({ error: 'You do not have deletion rights' });
       }
     });
     ```

3. **Data:**
   - The jokes are stored in an array, with each joke having an `id`, `jokeText`, and `jokeType`.

   ```javascript
   var jokes = [
     { id: 1, jokeText: "Why don't scientists trust atoms? Because they make up everything.", jokeType: "Science" },
     // additional jokes here
   ];
   ```

4. **Server Initialization:**
   - The server listens on port 3000.

   ```javascript
   app.listen(port, () => {
     console.log(`Successfully started server on port ${port}.`);
   });
   ```

"By providing these endpoints, JokeAPI offers comprehensive functionality for managing a jokes database, ensuring a versatile and user-friendly experience for joke enthusiasts."
