# Backend - Trivia API

## Setting up the Backend

### Install Dependencies

1. **Python 3.7** - Follow instructions to install the latest version of python for your platform in the [python docs](https://docs.python.org/3/using/unix.html#getting-and-installing-the-latest-version-of-python)

2. **Virtual Environment** - We recommend working within a virtual environment whenever using Python for projects. This keeps your dependencies for each project separate and organized. Instructions for setting up a virual environment for your platform can be found in the [python docs](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/)

3. **PIP Dependencies** - Once your virtual environment is setup and running, install the required dependencies by navigating to the `/backend` directory and running:

```bash
pip install -r requirements.txt
```

#### Key Pip Dependencies

- [Flask](http://flask.pocoo.org/) is a lightweight backend microservices framework. Flask is required to handle requests and responses.

- [SQLAlchemy](https://www.sqlalchemy.org/) is the Python SQL toolkit and ORM we'll use to handle the lightweight SQL database. You'll primarily work in `app.py`and can reference `models.py`.

- [Flask-CORS](https://flask-cors.readthedocs.io/en/latest/#) is the extension we'll use to handle cross-origin requests from our frontend server.

### Set up the Database

With Postgres running, create a `trivia` database:

```bash
createdb trivia
```

Populate the database using the `trivia.psql` file provided. From the `backend` folder in terminal run:

```bash
psql trivia < trivia.psql
```

### Run the Server

From within the `./src` directory first ensure you are working using your created virtual environment.

To run the server, execute:

```bash
flask run --reload
```

The `--reload` flag will detect file changes and restart the server automatically.

## To Do Tasks

These are the files you'd want to edit in the backend:

1. `backend/flaskr/__init__.py`
2. `backend/test_flaskr.py`

One note before you delve into your tasks: for each endpoint, you are expected to define the endpoint and response data. The frontend will be a plentiful resource because it is set up to expect certain endpoints and response data formats already. You should feel free to specify endpoints in your own way; if you do so, make sure to update the frontend or you will get some unexpected behavior.

1. Use Flask-CORS to enable cross-domain requests and set response headers.
2. Create an endpoint to handle `GET` requests for questions, including pagination (every 10 questions). This endpoint should return a list of questions, number of total questions, current category, categories.
3. Create an endpoint to handle `GET` requests for all available categories.
4. Create an endpoint to `DELETE` a question using a question `ID`.
5. Create an endpoint to `POST` a new question, which will require the question and answer text, category, and difficulty score.
6. Create a `POST` endpoint to get questions based on category.
7. Create a `POST` endpoint to get questions based on a search term. It should return any questions for whom the search term is a substring of the question.
8. Create a `POST` endpoint to get questions to play the quiz. This endpoint should take a category and previous question parameters and return a random questions within the given category, if provided, and that is not one of the previous questions.
9. Create error handlers for all expected errors including 400, 404, 422, and 500.

## Documenting your Endpoints

You will need to provide detailed documentation of your API endpoints including the URL, request parameters, and the response body. Use the example below as a reference.

### Documentation Example

`GET '/api/v1.0/categories'`

- Fetches a dictionary of categories in which the keys are the ids and the value is the corresponding string of the category
- Request Arguments: None
- Returns: An object with a single key, `categories`, that contains an object of `id: category_string` key: value pairs.

```json
{
  "1": "Science",
  "2": "Art",
  "3": "Geography",
  "4": "History",
  "5": "Entertainment",
  "6": "Sports"
}
```

## Testing

Write at least one test for the success and at least one error behavior of each endpoint using the unittest library.

To deploy the tests, run

```bash
dropdb trivia_test
createdb trivia_test
psql trivia_test < trivia.psql
python test_flaskr.py
```

### Endpoints Documentation

`GET '/categories'`
- Fetches a dictionary of categories in which the keys are the ids and the value is the corresponding string of the category
- Request Arguments: None
- Returns: A multiple key/value pairs object with the following structure:
    - `success`: can take values `True` or `False`.
    - `categories`: dictionary of categories gotten from the database.

Example of return object:

```JSON
{
  "categories": {
    "1": "Science",
    "2": "Art",
    "3": "Geography",
    "4": "History",
    "5": "Entertainment",
    "6": "Sports"
  },
  "success": true,
}

```

`GET '/questions'`
- Fetches a dictionary of questions.
- Request Arguments: Page's number (optional)
- Returns: A multiple key/value pairs object with the following structure:
    - `success`: can take values `True` or `False`.
    - `questions`: contains a list of the fetched questions.
    - `total_questions`: the number of questions returned.
    - `categories`: dictionary of categories gotten from the database.
    - `current_category`: list of the categories of the returned questions list.

Example of return object:

```JSON
{
  "categories": {
    "1": "Science"
  },
  "current_category": [
    1
  ],
  "questions": [
    {
      "answer": "The Liver",
      "category": 1,
      "difficulty": 4,
      "id": 20,
      "question": "What is the heaviest organ in the human body?"
    },
    {...}
  ],
  "success": true,
  "total_questions": 5
}
```

`DELETE '/questions/<int:question_id>'`
- Deletes the question selected by `question_id`.
- Request Arguments: `question_id` (required)
- Returns: A key/value pair object with the following structure:
    - `success`: can take values `True` or `False`.

Example of return object:

```JSON
{
  "success": true
}
```

`POST '/questions'`
- Inserts a new question in the database.
- Request Arguments: a key/value pairs object whit the following content:
    - `question`: string containing the question itself.
    - `answer`: answer's string.
    - `category`: category ID field.
    - `difficulty`: difficulty level.

Example of the object:

```JSON
{
    answer: "Thomas Edison"
    category: 1
    difficulty: 3
    question: "Who invented the lightbulb?"
}
```

- Returns: A multiple key/value pairs object with the following structure:
    - `success`: can take values `True` or `False`.
    - `created`: Returns the value of the newly created question.id,
    - `questions`: contains a list of the fetched questions.
    - `total_questions`: the number of questions returned.


Example of return object:

```JSON
{
  "questions": [
    {
      "answer": "Thomas Edison",
      "category": 1,
      "difficulty": 3,
      "id": 12,
      "question": "Who invented the lightbulb?"
    },
    {...}
  ],
  "success": true,
  "created": 3
  "total_questions": 17
}
```

`POST '/questions_search'`
- Returns a set of questions based on a search term.
- Request Arguments:
    - `searchTerm`: string to search in questions string.
- Returns: A multiple key/value pairs object with the following structure:
    - `success`: can take values `True` or `False`.
    - `questions`: contains a list of the fetched questions.
    - `total_questions`: the number of questions returned.
    - `current_category`: category ID field.

Example of return object:

```JSON
{
  "questions": [
    {
      "answer": "Brazil",
      "category": 5,
      "difficulty": 4,
      "id": 4,
      "question": "Which is the only team to play in every soccer World Cup tournament?"
    }
  ],
  "success": true,
  "total_questions": 1,
  "current_category": 4
}

```

`GET '/categories/<int:category_id>/questions'`
- Returns a subset of questions that belong to a specific category.
- Request Arguments:
    - `category_id`: category id field.
- Returns: A multiple key/value pairs object with the following structure:
    - `success`: can take values `True` or `False`.
    - `questions`: contains a list of the fetched questions.
    - `total_questions`: the number of questions returned.

Example of return object:
```JSON
{
  "questions": [
    {
      "answer": "It depends",
      "category": 1,
      "difficulty": 1,
      "id": 77,
      "question": "Can birds fly?"
    },
    {
      "answer": "Brazil",
      "category": 3,
      "difficulty": 4,
      "id": 2,
      "question": "Which is the only team to play in every soccer World Cup tournament?"
    },
    {...}
  ],
  "success": true,
  "total_questions": 4
}
```


`POST '/quizzes'`
- Gets random questions for player.
- Request Arguments:
    - `category_id`: question's category id field.
    - `previous_quesion`: question in the previous iteration, first time it's an empty string.
- Returns: A multiple key/value pairs object with the following content:
    - `success`: can take values `True` or `False`.
    - `question`: contains the question.

Example of return object:
```JSON
{
  "success": true,
  "question": {
    "answer": "Alexander Fleming",
    "category": 1,
    "difficulty": 3,
    "id": 16,
    "question": "Who discovered penicillin?"
  }
}
```

## Errors handling:
Endpoints are written for error handlers. They return key/value pairs as follows:
- `success`: False.
- `error`: error code_number.
- `message`: description of error.

Example of return object:

```JSON
{
    "success": False,
    "error": 404,
    "message": "Resource Not Found"
}
```
