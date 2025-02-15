# Maneka
## User Routes (/user)

- `GET /user/`
- `POST /user/register`
- `POST /user/login`
- `POST /user/path`

## Article Routes (/article)

- `GET /article/`
- `GET /article/:ArticleId`
- `GET /article/recommended-articles`
- `POST /article/generate/:CategoryAlias/:ContentType`

## Attempt Routes (/attempt)

- `GET /attempt/`
- `POST /attempt/initial-attempt`

## Answer Routes (/answer)

- `GET /answer/`
- `GET /answer/:AttemptId/:QuestionId`
- `POST /answer/:AttemptId/:QuestionId`

## Score Routes (/score)

- `GET /score/`
- `POST /score/:AttemptId`

## Plan Routes (/plan)

- `GET /plan/`
- `POST /plan/`
- `PUT /plan/:PlanId`
- `DELETE /plan/:PlanId`
- `GET /plan/:PlanId/tasks`

## Task Routes (/task)

- `GET /task/`
- `GET /task/:PlanId`
- `POST /task/:PlanId`
- `GET /task/:PlanId/:TaskId`
- `PUT /task/:PlanId/:TaskId`
- `DELETE /task/:PlanId/:TaskId`

<br>

# Details Endpoints

## Endpoints

### `GET /`

- **Description**: Returns a simple message indicating the API is running.
- **Response**:
  - `200 OK`: Returns the message "TalentDiscovery API".

## User Routes

- **Base URL**: `/user`

### `GET /user`

- **Response**:
  - `200 OK`: Returns the message "User".

### `POST /user/register`

- **Description**: Registers a new user.
- **Request Body**:
  - `email` (string): The email of the new user.
  - `username` (string): The username of the new user.
  - `password` (string): The password of the new user.
- **Response**:
  - `201 Created`:
    ```json
    {
      "username": "String",
      "email": "String"
    }
    ```
  - `400 Bad Request`:
    - Email already exists
    - Username already exists
    - Email is required
    - Username is required
    - Password is required
    - Invalid email format
    - Password minimum character is 5

### `POST /user/login`

- **Description**: Logs in an existing user.
- **Request Body**:
  - `username` (string): The username of the user.
  - `password` (string): The password of the user.
- **Response**:

  - `200 OK`:

    ```json
    {
      "access_token": "string" // The token for the user
    }
    ```

  - `400 Bad Request`:
    - Username is required
    - Password is required
    - Username or password is incorrect
  - `401 Unauthorized`: Invalid token

### `POST /user/path`

- **Description**: Generates paths for the user. This route is protected and requires authentication.
- **Response**:
  - `200 OK`: Paths successfully generated.
  - `401 Unauthorized`: Invalid token

## Article Routes

- **Base URL**: `/article`

### `GET /article/`

- **Response**:
  - `200 OK`: Returns the message "Article route".

### `GET /article/:ArticleId`

- **Description**: Retrieves the details of a specific article.
- **Response**:
  - `200 OK`:

    ```json
    {
      "_id": "String",
      "title": "String",
      "url": "String",
      "imageUrl": "String",
      "imagesUrl": ["String"],
      "snippet": "String",
      "publishedDate": "Date or Null",
      "rawContent": "String",
      "source": "String",
      "contentType": "String",
      "category": "String",
      "score": "Number",
      "relatedAreas": ["String"],
      "industries": ["String"],
      "programLevel": "String"
    }
    ```

  - `404 Not Found`: Article not found

### `GET /article/recommended-articles`

- **Description**: Retrieves recommended articles for the authenticated user.
- **Response**:
  - `200 OK`:
    ```json
    [
        {
            "_id": "String",
            "title": "String",
            "url": "String",
            "imageUrl": "String",
            "imagesUrl": ["String"],
            "snippet": "String",
            "publishedDate": "Date or Null",
            "rawContent": "String",
            "source": "String",
            "contentType": "String",
            "category": "String",
            "score": "Number",
            "relatedAreas": ["String"],
            "industries": ["String"],
            "programLevel": "String"
        },
        ...more articles
    ]
    ```
  - `401 Unauthorized`: Invalid token.

### `POST /article/generate/:CategoryAlias/:ContentType`

- **Description**: Generates articles based on category and content type.
- **Response**:
  - `201 OK`: Successfully generated articles

## Attempt Routes

- **Base URL**: `/attempt`

### `GET /attempt/`

- **Description**: Retrieves user active attempts.
- **Response**:

  - `200 OK`:

    ```json
    [
        {
            "_id": "String",
            "UserId": "String",
            "PackageName": "String",
            "status": "String",
            "QuestionType": "String",
            "Package":
            {
                "_id": "String",
                "name": "String",
                "title": "String",
                "type": "String",
            },
            "questions": [
                {
                    "_id": "String",
                    "IntelligenceType": "String",
                    "QuestionType": "String",
                    "QuestionPackage": "String",
                    "question": "String",
                },
                ...more questions
            ]
        },
        ...more attempts
    ]
    ```

### `POST /attempt/initial-attempt`

- **Description**: Creates an initial attempt.
- **Response**:
  - `201 Created`: Initial attempt created

## Answer Routes

- **Base URL**: `/answer`

### `GET /answer/`

- **Response**:
  - `200 OK`: Returns the message "Answer route".

### `GET /answer/:AttemptId/:QuestionId`

- **Description**: Retrieves the answer for a specific attempt and question.
- **Response**:
  - `200 OK`:

        ```json
        {
            "_id": "String",
            "UserId": "String",
            "AttemptId": "String",
            "QuestionId": "String",
            "answer": "Number",
            "isCorrect": "Boolean",
        }
        ```

### `POST /answer/:AttemptId/:QuestionId`

- **Description**: Creates and Update an answer for a specific attempt and question.
- **Response**:
  - `201 Created`: Answer submitted/updated.

## Score Routes

- **Base URL**: `/score`

### `GET /score/`

- **Description**: Retrieves the score.
- **Response**:
  - `200 OK`:

    ```json
    [
      {
        "_id": "String",
        "UserId": "String",
        "IntelligenceType": "String",
        "score": "Number"
      }
    ]
    ```

### `POST /score/:AttemptId`

- **Description**: Submits the score for a specific attempt.
- **Response**:
  - `201 Created`: Score submitted

## Plan Routes

- **Base URL**: `/plan`

### `GET /plan/`

- **Description**: Retrieves all plans for the authenticated user.
- **Response**:
  - `200 OK`:

    ```json
    [
        {
            "_id": "String",
            "UserId": "String",
            "title": "String",
            "description": "String",
            "path": "String",
            "type": "String",
            "campus": "String",
            "duration": "Number",
            "startDate": "Number"
        },
        ...more plans
    ]
    ```

### `POST /plan/`

- **Description**: Creates a new plan for the authenticated user.
- **Response**:
  - `201 Created`: Plan successfully created

### `PUT /plan/:PlanId`

- **Description**: Edits a specific plan for the authenticated user.
- **Response**:
  - `200 OK`: Plan successfully updated

### `DELETE /plan/:PlanId`

- **Description**: Deletes a specific plan for the authenticated user.
- **Response**:
  - `200 OK`: Plan successfully deleted.

### `GET /plan/:PlanId/tasks`

- **Description**: Retrieves tasks for a specific plan.
- **Response**:
  - `200 OK`:

    ```json
    {
        "_id": "String",
        "title": "String",
        "description": "String",
        "path": "String",
        "type": "String",
        "campus": "String",
        "duration": "Number",
        "startDate": "String",
        "Tasks": [
            {
                "month": "String",
                "month_num": "Number",
                "tasks": [
                    {
                        "_id": "String",
                        "title": "String",
                        "task": "String",
                        "date": "String",
                        "time": "String",
                        "UserId": "String",
                        "PlanId": "String",
                        "month": "String",
                        "month_num": "Number",
                        "week": "Number",
                        "isFinished": "Boolean"
                    },
                    ...more tasks
                ]
            },
            ...more months
        ]
    }
    ```

## Task Routes

- **Base URL**: `/task`

### `GET /task/`

- **Response**:
  - `200 OK`: Returns the message "Task route".

### `GET /task/:PlanId`

- **Description**: Retrieves tasks for a specific plan.
- **Response**:
  - `200 OK`:

    ```json
    [
        {
            "_id": "String",
            "title": "String",
            "task": "String",
            "date": "String",
            "time": "String",
            "UserId": "String",
            "PlanId": "String",
            "month": "String",
            "month_num": "Number",
            "week": "Number",
            "isFinished": "Boolean"
        },
    ...more tasks
    ]
    ```

### `POST /task/:PlanId`

- **Description**: Creates a task for a specific plan.
- **Request Body**:
  - `title` (string): The title of the task.
  - `task` (string): The task description.
  - `date` (string): The date of the task.
  - `time` (string): The time of the task.
- **Response**:
  - `201 Created`: Task successfully created.

### `GET /task/:PlanId/:TaskId`

- **Description**: Retrieves details of a specific task.
- **Response**:
  - `200 OK`:

    ```json
    {
      "_id": "String",
      "UserId": "String",
      "PlanId": "String",
      "title": "String",
      "task": "String",
      "date": "String",
      "time": "String",
      "month": "String",
      "month_num": "Number",
      "week": "Number",
      "isFinished": "Boolean"
    }
    ```

### `PUT /task/:PlanId/:TaskId`

- **Description**: Edits details of a specific task.
- **Request Body**:
  - `title` (string): The title of the task.
  - `task` (string): The task description.
  - `date` (string): The date of the task.
  - `time` (string): The time of the task.
- **Response**:
  - `200 OK`: Task successfully updated.

### `DELETE /task/:PlanId/:TaskId`

- **Description**: Deletes a specific task.
- **Response**:
  - `200 OK`: Task successfully deleted.
