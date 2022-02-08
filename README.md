# API Development and Documentation Final Project

## Trivia App

Udacity is invested in creating bonding experiences for its employees and students. A bunch of team members got the idea to hold trivia on a regular basis and created a webpage to manage the trivia app and play the game, but their API experience is limited and still needs to be built out.

That's where you come in! Help them finish the trivia app so they can start holding trivia and seeing who's the most knowledgeable of the bunch. The application must:

1. Display questions - both all questions and by category. Questions should show the question, category and difficulty rating by default and can show/hide the answer.
2. Delete questions.
3. Add questions and require that they include question and answer text.
4. Search for questions based on a text query string.
5. Play the quiz game, randomizing either all questions or within a specific category.

Completing this trivia app will give you the ability to structure plan, implement, and test an API - skills essential for enabling your future applications to communicate with others.

## Backend

### Working in your Local Environment

Step 1: Install Required Software
Python 3.7 - Follow instructions to install the latest version of python for your platform in the python docs

Virtual Environment - We recommend working within a virtual environment whenever using Python for projects. This keeps your dependencies for each project separate and organized. Instructions for setting up a virtual environment for your platform can be found in the python docs

Postgres - If you don't already have it installed, see installation instructions for your operating system here:PostgreSQL Downloads

Step 2: Set up and Populate the Database
With Postgres running, create a trivia database:
createdb trivia
From the backend folder in terminal, Populate the database using the trivia.psql file provided.run:
psql trivia < trivia.psql
Step 3: Install Dependencies
Once your virtual environment is setup and running, install the required dependencies by navigating to the /backend directory and running:

pip install -r requirements.txt
Step 4: Start the Server
Start the Server

In the backend directory, start the Flask server by running:

export FLASK_APP=flaskr
export FLASK_ENV=development
flask run

### Key Pip Dependencies
Flask is a lightweight backend microservices framework. Flask is required to handle requests and responses.
SQLAlchemy is the Python SQL toolkit and ORM we'll use to handle the lightweight SQL database. You'll primarily work in app.py and can referencemodels.py.
Flask-CORS is the extension we'll use to handle cross-origin requests from our frontend server.

### Setting Up Testing
This project is a great opportunity to practice Test-Driven Development (or TDD) . As a reminder, the process for TDD is:

Write a test for specific application behavior.
Run the test and watch it fail.
Write code to execute the required behavior.
Test the code and rewrite as necessary to pass the test
Refactor your code.
Repeat - write your next test.
For this project you need to write at least one test for the success and at least one error behavior of each endpoint using the unittest library. You should write the tests in backend/test_flaskr.py.

### Deploying Tests in your Local Enivronment
If you are working in a local environment, you'll need to manually set up and populate the testing database:

To deploy the tests, run

dropdb trivia_test
createdb trivia_test
psql trivia_test < trivia.psql
To deploy the tests, run:

python3 test_flaskr.py

> View the [Backend README](./backend/README.md) for more details.

## Frontend

### Working in your Local Environment
1. Install Node and NPM This project requires on Nodejs and Node Package Manager (NPM). If you haven't already installed Node on your local machine, see the instructions here: Before continuing, you must download and install Node (the download includes NPM) from Nodejs.com.
2. Install project dependencies After confirming you have NPM installed, navigate to the frontend directory of the project and run:
npm install

To start the app in development mode, run:

npm start
Open http://localhost:3000 to view it in the browser. The page will reload if you make edits.

> View the [Frontend README](./frontend/README.md) for more details.

## Endpoint Documentation

GET '/categories'

Fetches a dictionary of categories in which the keys are the ids and the value is the corresponding string of the category
Request Arguments: None
Returns: An object with a single key, categories, that contains an object of id: category_string key:value pairs.
{
    'categories': { '1' : "Science",
    '2' : "Art",
    '3' : "Geography",
    '4' : "History",
    '5' : "Entertainment",
    '6' : "Sports" }
}
GET '/questions?page=${integer}'

Fetches a paginated set of questions, a total number of questions, all categories and current category string.
Request Arguments: page - integer
Returns: An object with 10 paginated questions, total questions, object including all categories, and current category string
{
    'questions': [
        {
            'id': 1,
            'question': 'This is a question',
            'answer': 'This is an answer',
            'difficulty': 5,
            'category': 2
        },
    ],
    'totalQuestions': 100,
    'categories': { '1' : "Science",
    '2' : "Art",
    '3' : "Geography",
    '4' : "History",
    '5' : "Entertainment",
    '6' : "Sports" },
    'currentCategory': 'History'
}
GET '/categories/${id}/questions'

Fetches questions for a cateogry specified by id request argument
Request Arguments: id - integer
Returns: An object with questions for the specified category, total questions, and current category string
{
    'questions': [
        {
            'id': 1,
            'question': 'This is a question',
            'answer': 'This is an answer',
            'difficulty': 5,
            'category': 4
        },
    ],
    'totalQuestions': 100,
    'currentCategory': 'History'
}
DELETE '/questions/${id}'

Deletes a specified question using the id of the question
Request Arguments: id - integer
Returns: Does not need to return anything besides the appropriate HTTP status code. Optionally can return the id of the question. If you are able to modify the frontend, you can have it remove the question using the id instead of refetching the questions.
POST '/quizzes'

Sends a post request in order to get the next question
Request Body:
{
    'previous_questions': [1, 4, 20, 15]
    quiz_category': 'current category'
 }
Returns: a single new question object
{
    'question': {
        'id': 1,
        'question': 'This is a question',
        'answer': 'This is an answer',
        'difficulty': 5,
        'category': 4
    }
}
POST '/questions'

Sends a post request in order to add a new question
Request Body:
{
    'question':  'Heres a new question string',
    'answer':  'Heres a new answer string',
    'difficulty': 1,
    'category': 3,
}
Returns: Does not return any new data
POST '/questions'

Sends a post request in order to search for a specific question by search term
Request Body:
{
    'searchTerm': 'this is the term the user is looking for'
}

Returns: any array of questions, a number of totalQuestions that met the search term and the current category string
{
    'questions': [
        {
            'id': 1,
            'question': 'This is a question',
            'answer': 'This is an answer',
            'difficulty': 5,
            'category': 5
        },
    ],
    'totalQuestions': 100,
    'currentCategory': 'Entertainment'
}
