# Separation of Concerns

This is a repository to demonstrate proper separation of concerns in a Golang web program.
The program is separated into three parts, an access layer, the business logic, and the action layer.

## Access Layer

The access layer is how you interact with the program.
In a command line program, this would be the code that parses the command line flags and prints the output.
Some programs may have multiple access layers.

In this web program, the access layer is JSON over HTTP.
The access layer parses HTTP requests with JSON bodies, and passes the parameters into the business logic.
It then takes the response from the business logic, and translates it into a proper HTTP response.
This layer also does validation on any user input, making sure that the input follows the requirements of the request.

## Business Logic

The business logic determines what is happening for a request.
It assumes that all input is correct, but does checking on whether it is semantically correct.
For example: it will check if the user making a request is allowed to make the request.
The business logic is responsible for determining what will happen for a request.
It will not actually perform any actions that affect the system itself.

In this web program, the business logic is the user service.
The business logic checks if an email is already in use in the register action, and if not, saves the new user.

## Action Layer

The action layer actually performs actions.
It should prefer specific functions over more generic functions.
For example: a function to save a user over a function to save a row to a database.
The action layer should make as few decisions as possible, and just perform actions.
It may use generic internal functions to do things.
For example: the save a user function may use a package-private generic function that saves a row to a database.
Most programs will have multiple systems in the action layer.

In this web program, the action layer is the user storage.
It just uses an in-memory map to store the users, but it could just as easily saved to a database somewhere.
