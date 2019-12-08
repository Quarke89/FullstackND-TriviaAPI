# Full Stack API Final Project

## Trivia app description

The webpage is a Trivia app that can display questions and allows you to play a game with the questions. The app supports an API that can 

1) Display questions - both all questions and by category. 
2) Delete questions.
3) Add questions and require that they include question and answer text.
4) Search for questions based on a text query string.
5) Play the quiz game, randomizing either all questions or within a specific category. 

The project also supports unit testing for the API

## Setting up the Backend

### Installing Dependencies

#### Python 3.7

Follow instructions to install the latest version of python for your platform in the [python docs](https://docs.python.org/3/using/unix.html#getting-and-installing-the-latest-version-of-python)

#### Virtual Enviornment

Setup virtual environment within project folder using 

```
python3 -m venv env
```

Activate virtual environment using 

```
source env/bin/activate
```

#### PIP Dependencies

Once you have your virtual environment setup and running, install dependencies by naviging to the `/backend` directory and running:

```bash
pip3 install -r requirements.txt
```

This will install all of the required packages we selected within the `requirements.txt` file.

##### Key Dependencies

- [Flask](http://flask.pocoo.org/)  is a lightweight backend microservices framework. Flask is required to handle requests and responses.

- [SQLAlchemy](https://www.sqlalchemy.org/) is the Python SQL toolkit and ORM we'll use handle the lightweight sqlite database. You'll primarily work in app.py and can reference models.py. 

- [Flask-CORS](https://flask-cors.readthedocs.io/en/latest/#) is the extension we'll use to handle cross origin requests from our frontend server. 

## Database Setup
With Postgres running, restore a database using the trivia.psql file provided. From the backend folder in terminal run:
```bash
dropdb trivia
createdb trivia
psql trivia < trivia.psql
```

## Running the server

From within the `backend` directory first ensure you are working using your created virtual environment.

To run the server, execute:

```bash
export FLASK_APP=flaskr
export FLASK_ENV=development
flask run
```

Setting the `FLASK_ENV` variable to `development` will detect file changes and restart the server automatically.

Setting the `FLASK_APP` variable to `flaskr` directs flask to use the `flaskr` directory and the `__init__.py` file to find the application. 

## Setting up the Frontend

### Installing Dependencies

#### Installing Node and NPM

This project depends on Nodejs and Node Package Manager (NPM). Before continuing, you must download and install Node (the download includes NPM) from [https://nodejs.com/en/download](https://nodejs.org/en/download/).

#### Installing project dependencies

This project uses NPM to manage software dependencies. NPM Relies on the package.json file located in the `frontend` directory of this repository. After cloning, open your terminal and run:

```bash
npm install
```

>_tip_: **npm i** is shorthand for **npm install**

### Running in Dev Mode

The frontend app was built using create-react-app. In order to run the app in development mode use ```npm start```. You can change the script in the ```package.json``` file. 

Open [http://localhost:3000](http://localhost:3000) to view it in the browser. The page will reload if you make edits.<br>

```bash
npm start
```


## Testing
To run the tests, run
```
dropdb trivia_test
createdb trivia_test
psql trivia_test < trivia.psql
python test_flaskr.py
```

## Endpoints

GET `/categories`
- Fetches a dictionary of categories in which the keys are the ids and the value is the corresponding string of the category
- Request Arguments: None
- Returns: An object with 2 keys. status and categories an object of id: category_string key:value pairs. 

Example response
```
{
  "categories": {
    "1": "Science",
    "2": "Art",
    "3": "Geography",
    "4": "History",
    "5": "Entertainment",
    "6": "Sports"
  },
  "success": true
}
```

GET `/questions`
- Fetches paginated questions in groups of 10
- Request Arguments: page. Page index for the paginated questions. Default 1. Usage: `/questions?page=1`
- Returns an object with the paginated questions, categories, and total number of questions

Example response
```
{
  "categories": [
    "Science",
    "Art",
    "Geography",
    "History",
    "Entertainment",
    "Sports"
  ],
  "current_category": [],
  "questions": [
    {
      "answer": "Apollo 13",
      "category": 5,
      "difficulty": 4,
      "id": 2,
      "question": "What movie earned Tom Hanks his third straight Oscar nomination, in 1996?"
    },

    ...

    {
      "answer": "The Palace of Versailles",
      "category": 3,
      "difficulty": 3,
      "id": 14,
      "question": "In which royal palace would you find the Hall of Mirrors?"
    }
  ],
  "success": true,
  "total_questions": 19
}
```

GET `/categories/<int:category_id>/questions`

- Fetches paginated questions in groups of 10 for a specific category
- Request Arguments: page. Page index for the paginated questions. Default 1. Usage: `/categories/1/questions?page=1`
- Returns an object with the paginated questions for the specified category, categories, and total number of questions

Example response
```
{
  "categories": [
    "Science",
    "Art",
    "Geography",
    "History",
    "Entertainment",
    "Sports"
  ],
  "current_category": {
    "id": 6,
    "type": "Sports"
  },
  "questions": [
    {
      "answer": "Brazil",
      "category": 6,
      "difficulty": 3,
      "id": 10,
      "question": "Which is the only team to play in every soccer World Cup tournament?"
    },
    {
      "answer": "Uruguay",
      "category": 6,
      "difficulty": 4,
      "id": 11,
      "question": "Which country won the first ever soccer World Cup in 1930?"
    }
  ],
  "success": true,
  "total_questions": 2
}
```

DELETE `/questions/<int:question_id>'`

- Deletes the question speicified by the question id
- Request Arguments: None
- Returns an object that returns success status and the id of the deleted question

Example response
```
{
  "deleted": 5,
  "success": true
}
```

POST `/questions`

- Searches the database for questions with the given search term in the payload
- Request Payload: JSON object that contains a key `"searchTerm"` with the search phrase
  ```
  {
      "searchTerm": "title"
  }
  ```
- Returns an object that contains a question key with all the questions with the search term, a success key, and total questions

Example response
```
{
  "current_category": [],
  "questions": [
    {
      "answer": "Edward Scissorhands",
      "category": 5,
      "difficulty": 3,
      "id": 6,
      "question": "What was the title of the 1990 fantasy directed by Tim Burton about a young man with multi-bladed appendages?"
    }
  ],
  "success": true,
  "total_questions": 1
}
```

POST `/questions`

- Adds a question to the database using data from the request payload
- Request Payload: contains a JSON object with the question text, answer text, category, and difficulty rating
  ```
  { 
    "question": "Who is the strongest avenger?",
    "answer" : "hulk",
    "category": 5,
    "difficulty": 2
  }
  ```
- Returns an object that contains paginated questions, success key, and the total questions

Example response
```
{
  "questions": [
    {
      "answer": "Apollo 13",
      "category": 5,
      "difficulty": 4,
      "id": 2,
      "question": "What movie earned Tom Hanks his third straight Oscar nomination, in 1996?"
    },
  ...
    {
      "answer": "Agra",
      "category": 3,
      "difficulty": 2,
      "id": 15,
      "question": "The Taj Mahal is located in which Indian city?"
    }
  ],
  "success": true,
  "total_questions": 20
}
```

POST `/quizzes`

- Gets questions to play the quiz
- Request Payload: A JSON object that contains
  -  `previous_questions` : list of previous question ids
  -  `quiz_category` : category of questions to pick from
```
{ 
	"previous_questions": [4, 15],
	"quiz_category" : {
        "type":"Science",
        "id":"1"
    }
}
```
- Returns an object that contains a question which has been picked randomly based on the category and which hasnt already been played (not part of previous_questions)
```
{
  "question": {
    "answer": "The Liver",
    "category": 1,
    "difficulty": 4,
    "id": 20,
    "question": "What is the heaviest organ in the human body?"
  },
  "success": true
}
```