# my_microservices_app
Description: 
A PHP Symfony-based microservices application comprising two distinct services—Users and Notifications—that communicate seamlessly via a message broker using Symfony Messenger and RabbitMQ. The Users service handles user creation, storing data in a MySQL database, and dispatching events to the Notifications service, which consumes these events and logs the information.

Users Service (users):

Exposes a POST /users endpoint.
Accepts JSON payloads containing email, firstName, and lastName.
Stores user data in a MySQL database.
Dispatches a UserCreatedMessage event to RabbitMQ upon successful user creation.

Notifications Service (notifications):

Listens to UserCreatedMessage events from RabbitMQ.
Consumes these events and logs the user data to a notifications.log file.
Communication between services is facilitated by RabbitMQ, managed through Docker containers.


Prerequisites:

Docker & Docker Compose: For containerizing and orchestrating services.
Git: To clone the repository.
Composer: PHP dependency manager.
PHP 8.1+: Required for Symfony applications.
Symfony CLI (optional but recommended): Facilitates Symfony project management.

Folder: 

docker/: Contains Dockerfiles for each service and the Docker Compose configuration.
users/: Symfony project for the Users service.
notifications/: Symfony project for the Notifications service.
README.md: Project documentation.


git clone https://github.com/your-username/my_microservices_app.git
cd my_microservices_app

Build and Start Services with Docker

cd docker
docker-compose up --build -d



Endpoint: POST /users
URL: http://localhost:8001/users

Method: POST

Headers: Content-Type: application/json

Request Body: {
  "email": "test@example.com",
  "firstName": "John",
  "lastName": "Doe"
}

Request :

curl -X POST http://localhost:8001/users \
  -H "Content-Type: application/json" \
  -d '{"email":"john.doe@example.com","firstName":"John","lastName":"Doe"}'

  

Response:
Body: json
{
  "status": "User created"
}

URL: http://localhost:15672
Username: guest
Password: guest
