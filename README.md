# local_todo_api
local_api with todo list
...................
# Local REST API

Use this to have a locally running REST API that accepts JSON.

This was made as a simple replacement for JSONBox.io.

## Pre-installation steps

In the installation process your shell will try to run a certain command. This
command needs to be able to clone repositories from Github using an SSH key.

To check if you can already do this try to run the following command from your terminal:

`git clone git@github.com:MathysL/local_todo_api.git`

If this works you can continue on to installation.
....
If this does _not_ work you'll get an error like `Could not read from remote repository`. This means you need to take the following steps:
1. [generate an SSH key pair](https://docs.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent#generating-a-new-ssh-key)
2. [add your private key to your SSH agent](https://docs.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent#adding-your-ssh-key-to-the-ssh-agent)
3. give your _public key_ [to Github](https://github.com/settings/keys)
....

This command should now work:
`git clone git@github.com:MathysL/local_todo_api.git`

[More info on how to clone a repository using the command
line.](https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/cloning-a-repository#cloning-a-repository-using-the-command-line)

## Installation

When you've done that take the following steps:

- make sure you're using node >= 14
- git clone this repository
- `cd local_todo_api`
- `npm install`
- `npm start`

The app will start on port 3000. Make sure the port is part of the URL you send
requests to. For example: a GET request to
`http://localhost:3000/`

## Sending HTTP requests to this API

You can send 4 kinds of HTTP requests to this app.

All but the `delete` requests need to have the content-type header set to
`application/json`.

### POST

To create an item send a POST request with a JSON object in the body to `/`. The
return value will be the newly created object and HTTP status 201.

```json
{
  "name": "Ernie",
  "color": "orange",
  "mood": "happy",
  "_id": "f5408a45-b4d0-4aee-8530-c2250481b131",
  "_createdOn": "2021-01-25T14:53:49.322Z"
}
```

Each item gets an auto generated id and a `_createdOn` attribute.

### GET

To read all items send a GET request to `/`. The return value will be the list
of all created objects and HTTP status 200.

```json
[
  {
    "name": "Ernie",
    "color": "orange",
    "mood": "happy",
    "_id": "f8636d68-e656-4c2e-ac99-a625f35a25f9",
    "_createdOn": "2021-01-25T14:59:50.834Z"
  },
  {
    "name": "Bert",
    "color": "yellow",
    "mood": "grumpy",
    "_id": "b0092da7-363f-4c20-859b-b6d4c008dcb3",
    "_createdOn": "2021-01-25T15:00:02.403Z"
  }
]
```

To read a single item send a GET request to `/{id_of_the_item}`. The return
value will be the item, if it exists, and HTTP status 200.

```json
{
  "name": "Bert",
  "color": "yellow",
  "mood": "grumpy",
  "_id": "b0092da7-363f-4c20-859b-b6d4c008dcb3",
  "_createdOn": "2021-01-25T15:00:02.403Z"
}
```

### PUT

To update an item send a PUT request with a body to `/{id_of_the_item}`. The
body should contain the updated item. The return value will be the updated item
and HTTP status 200.

```json
{
  "name": "Groover",
  "color": "green",
  "mood": "hungry",
  "_id": "b0092da7-363f-4c20-859b-b6d4c008dcb3",
  "_createdOn": "2021-01-25T15:00:02.403Z",
  "_updatedOn": "2021-01-25T15:04:04.194Z"
}
```

An updated item gets an `_updatedOn` attribute.

### DELETE

To delete an item send a DELETE request to `/{id_of_the_item}`. The return value
will be HTTP 204.

## Deleting the database

If you want to start over:

- stop the app
- delete the files in `db/`
- restart the app


#todo list
a TODO list in Vanilla JavaScript, the Todo list islinked to a RESTful API (that is a module and already built).
So you are not going to store any of the data in the front-end of the application.
You will get all the data from the "back-end" where you get your own endpoint.

#data of todo
To get the first item in your endpoint you can send a POST request to the URL, do
this first with Postman and then also from JavaScript. Send as the body a
JavaScript object with a description and a "done" key that is set to "false". See this
example:

const data = {description: "buy oatmeal", done: false};
fetch(baseUrl, {
 method: "POST",
 body: JSON.stringify(data),
 headers: {
 "Content-Type": "application/json",
 },
});

##GET
Check with GET what is in the endpoint.
You will find that the endpoint works with hashes that it generates itself from
your data every time you make a request. Your data will look like this:
{
 "_id": "skdjfhskdjfhsdfk",
 "description": "buy oat milk",
 "done": false,
 "_createdOn": "2020-10-20et etc"
}

As you can see, you will receive an id of the endpoint for free, which you will
need later to refer to that specific task.
##POST: 
Update the task list with 1 new task. Send only 
{description: "blah", done:false}
@@DELETE:
Delete a task from the database. Use the id you get back as an identifier.

If needed change the file called api-client.js as you please for all your requests.
