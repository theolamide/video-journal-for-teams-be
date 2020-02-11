# Video Journal For Teams Backend

## Code Climate

[![Maintainability](https://api.codeclimate.com/v1/badges/d1601cb84ad12ad579f2/maintainability)](https://codeclimate.com/github/Lambda-School-Labs/video-journal-for-teams-be/maintainability)
[![Test Coverage](https://api.codeclimate.com/v1/badges/d1601cb84ad12ad579f2/test_coverage)](https://codeclimate.com/github/Lambda-School-Labs/video-journal-for-teams-be/test_coverage)

## Test Coverage via Jest

![coverage:statements](badges/badge-statements.svg)
![coverage:branches](badges/badge-branches.svg)
![coverage:functions](badges/badge-functions.svg)
![coverage:lines](badges/badge-lines.svg)

# API Documentation

#### 1️⃣ Backend production deployment at heroku: https://video-journal.herokuapp.com/ <br>

#### 1️⃣ Backend staging deployment at heroku: https://video-journal-staging.herokuapp.com/ <br>

## 1️⃣ Getting started

To get the server running locally:

- Clone this repo
- **yarn install** to install all required dependencies
- **yarn server** to start the local server
- **yarn test** to start server using testing environment

### Backend framework goes here

🚫 Why did you choose this framework?

- Point One
- Point Two
- Point Three
- Point Four

## 2️⃣ Endpoints

#### Auth Routes

| No. | Method | Endpoint                   | Access Control | Description                             |
| --- | ------ | -------------------------- | -------------- | --------------------------------------- |
| 1.  | POST   | `/api/auth/login/email`    | unrestricted   | Returns a token.                        |
| 2.  | POST   | `/api/auth/login/username` | unrestricted   | Returns a token.                        |
| 3.  | POST   | `/api/auth/register`       | unrestricted   | Creates a new user and returns a token. |

#### User Routes

| No. | Method | Endpoint                | Access Control | Description                       |
| --- | ------ | ----------------------- | -------------- | --------------------------------- |
| 4.  | GET    | `/api/users/`           | restricted     | Returns all the users.            |
| 5.  | GET    | `/api/users/:id`        | restricted     | Returns single user by id.        |
| 6.  | GET    | `/api/users/:id/teams`  | restricted     | Returns all of the user's teams.  |
| 7.  | GET    | `/api/users/:id/videos` | restricted     | Returns all of the user's videos. |
| 8.  | PUT    | `/api/users/:id`        | restricted     | Updates a user's information.     |

#### Team Routes

| No. | Method | Endpoint                        | Access Control | Description                                          |
| --- | ------ | ------------------------------- | -------------- | ---------------------------------------------------- |
| 9.  | GET    | `/api/teams/`                   | restricted     | Returns all teams.                                   |
| 10. | GET    | `/api/teams/:id`                | restricted     | Returns single team by id.                           |
| 11. | GET    | `/api/teams/:id/users`          | restricted     | Returns team members by team id.                     |
| 12. | GET    | `/api/teams/:id/prompts`        | restricted     | Returns prompts by team id.                          |
| 13. | GET    | `/api/teams/:id/videos`         | restricted     | Returns prompts with nested videos array by team id. |
| 14. | POST   | `/api/teams/:id/prompts`        | restricted     | Creates a new team prompts.                          |
| 15. | POST   | `/api/teams/`                   | restricted     | Creates a new team.                                  |
| 16. | POST   | `/api/teams/:id/users`          | restricted     | Adds a user to a team.                               |
| 17. | PUT    | `/api/teams/:id`                | restricted     | Updates team information.                            |
| 18. | DELETE | `/api/teams/:id/users/:user_id` | restricted     | Deletes a user from a team.                          |

#### Video Routes

| No. | Method | Endpoint                   | Access Control | Description                                    |
| --- | ------ | -------------------------- | -------------- | ---------------------------------------------- |
| 19. | GET    | `/api/videos/`             | restricted     | Returns all videos.                            |
| 20. | GET    | `/api/videos/:id`          | restricted     | Returns single video by owner id, plus prompt. |
| 21. | GET    | `/api/videos/:id/feedback` | restricted     | Returns feedback by video id.                  |
| 22. | POST   | `/api/videos/feedback`     | restricted     | Adds new feedback to a video.                  |
| 23. | POST   | `/api/videos/`             | restricted     | Adds a new video.                              |
| 24. | PUT    | `/api/videos/`             | restricted     | Updates info on and existing video.            |

#### Invitation Routes

| No. | Method | Endpoint             | Access Control | Description                                        |
| --- | ------ | -------------------- | -------------- | -------------------------------------------------- |
| 25. | GET    | `/api/invites/:code` | open           | Returns team_id. -1==Invalid, -2==Expired          |
| 26. | POST   | `/api/invites/`      | open           | Returns Invite object with a simple status message |

#### Avatar Routes

| No. | Method | Endpoint        | Access Control | Description             |
| --- | ------ | --------------- | -------------- | ----------------------- |
| 27. | GET    | `/api/avatars/` | open           | Returns public avatars. |

---

# Data Model

#### ROLES

---

```
{
  id: AUTO INCREMENT ID
  name: STRING, NOT NULLABLE
}
```

#### USERS

---

```
{
  id: AUTO INCREMENT ID
  email: STRING, UNIQUE, NOT NULLABLE
  username: STRING, UNIQUE, NOT NULLABLE
  password: STRING, NOT NULLABLE
  first_name: STRING, NOT NULLABLE
  last_name: STRING, NOT NULLABLE
}
```

#### TEAMS

---

```
{
  id: AUTO INCREMENT ID
  name: STRING, NOT NULLABLE
  description: STRING, NOT NULLABLE
  created_at: TIME_STAMP, DEFAULTS_TO(knex.fn.now()), NOT NULLABLE
  updated_at: TIME_STAMP, DEFAULTS_TO(knex.fn.now()), NOT NULLABLE
}
```

#### TEAM_MEMBERS

---

```
{
  user_id: FOREIGN KEY
  team_id: FOREIGN KEY
  role_id: FOREIGN KEY
}
```

#### PROMPTS

---

```
{
  id: AUTO INCREMENT ID
  question: STRING, NOT NULLABLE
  description: STRING
  team_id: FOREIGN KEY
  created_at: TIME_STAMP, DEFAULTS_TO(knex.fn.now()), NOT NULLABLE
  updated_at: TIME_STAMP, DEFAULTS_TO(knex.fn.now()), NOT NULLABLE
}
```

#### VIDEOS

---

```
{
  id: AUTO INCREMENT ID
  owner_id: FOREIGN KEY
  title: STRING, NOT NULLABLE
  description: STRING
  created_at: TIME_STAMP, DEFAULTS_TO(knex.fn.now()), NOT NULLABLE
  updated_at: TIME_STAMP, DEFAULTS_TO(knex.fn.now()), NOT NULLABLE
  video_url: STRING, NOT NULLABLE
  prompt_id: FOREIGN KEY
}
```

#### FEEDBACK

---

```
{
  id: AUTO INCREMENT ID
  post: STRING
  video_id: FOREIGN KEY
  owner_id: FOREIGN KEY
  created_at: TIME_STAMP, DEFAULTS_TO(knex.fn.now()), NOT NULLABLE
  updated_at: TIME_STAMP, DEFAULTS_TO(knex.fn.now()), NOT NULLABLE
}
```

#### INVITATION CODE

---

```
{
	id: AUTO INCREMENT ID
	team_id: FOREIGN KEY
	link: STRING
	isValid: BOOL
	created_at: TIMESTAMP
	expires_at: TIMESTAMP.
}
```

#### AVATARS

---

```
{
	id: AUTO INCREMENT ID
	src: STRING
}
```

## 2️⃣ Actions

🚫 This is an example, replace this with the actions that pertain to your backend

`getOrgs()` -> Returns all organizations

`getOrg(orgId)` -> Returns a single organization by ID

`addOrg(org)` -> Returns the created org

`updateOrg(orgId)` -> Update an organization by ID

`deleteOrg(orgId)` -> Delete an organization by ID
<br>
<br>
<br>
`getUsers(orgId)` -> if no param all users

`getUser(userId)` -> Returns a single user by user ID

`addUser(user object)` --> Creates a new user and returns that user. Also creates 7 availabilities defaulted to hours of operation for their organization.

`updateUser(userId, changes object)` -> Updates a single user by ID.

`deleteUser(userId)` -> deletes everything dependent on the user

## 3️⃣ Environment Variables

In order for the app to function correctly, the user must set up their own environment variables.

create a .env file that includes the following:

🚫 These are just examples, replace them with the specifics for your app

_ STAGING_DB - optional development db for using functionality not available in SQLite
_ NODE\*ENV - set to "development" until ready for "production"

- JWT*SECRET - you can generate this by using a python shell and running import random''.join([random.SystemRandom().choice('abcdefghijklmnopqrstuvwxyz0123456789!@#\$%^&amp;*(-_=+)') for i in range(50)])
  _ SENDGRID_API_KEY - this is generated in your Sendgrid account \* stripe_secret - this is generated in the Stripe dashboard

## Contributing

When contributing to this repository, please first discuss the change you wish to make via issue, email, or any other method with the owners of this repository before making a change.

Please note we have a [code of conduct](./code_of_conduct.md). Please follow it in all your interactions with the project.

### Issue/Bug Request

**If you are having an issue with the existing project code, please submit a bug report under the following guidelines:**

- Check first to see if your issue has already been reported.
- Check to see if the issue has recently been fixed by attempting to reproduce the issue using the latest master branch in the repository.
- Create a live example of the problem.
- Submit a detailed bug report including your environment & browser, steps to reproduce the issue, actual and expected outcomes, where you believe the issue is originating from, and any potential solutions you have considered.

### Feature Requests

We would love to hear from you about new features which would improve this app and further the aims of our project. Please provide as much detail and information as possible to show us why you think your new feature should be implemented.

### Pull Requests

If you have developed a patch, bug fix, or new feature that would improve this app, please submit a pull request. It is best to communicate your ideas with the developers first before investing a great deal of time into a pull request to ensure that it will mesh smoothly with the project.

Remember that this project is licensed under the MIT license, and by submitting a pull request, you agree that your work will be, too.

#### Pull Request Guidelines

- Ensure any install or build dependencies are removed before the end of the layer when doing a build.
- Update the README.md with details of changes to the interface, including new plist variables, exposed ports, useful file locations and container parameters.
- Ensure that your code conforms to our existing code conventions and test coverage.
- Include the relevant issue number, if applicable.
- You may merge the Pull Request in once you have the sign-off of two other developers, or if you do not have permission to do that, you may request the second reviewer to merge it for you.

### Attribution

These contribution guidelines have been adapted from [this good-Contributing.md-template](https://gist.github.com/PurpleBooth/b24679402957c63ec426).

## Documentation

See [Frontend Documentation](🚫link to your frontend readme here) for details on the fronend of our project.
🚫 Add DS iOS and/or Andriod links here if applicable.
