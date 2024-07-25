Chat App

Code Structure:-

Directory Layout: models/: Contains the Mongoose models for users and messages. public/: Contains the static files (HTML, CSS, JavaScript) served to the client. server.js: The main server-side script that handles HTTP and WebSocket requests. .env: File for environment variables (not included in the repository for security reasons). package.json: Lists dependencies and scripts for the project.

Models:- User Model: Defines the schema for user data in MongoDB, including username, password, and email. Message Model: Defines the schema for messages in MongoDB, including sender, text, and timestamp.

Public:- index.html: The main HTML file that contains the structure of the registration, login, and chat interfaces. style.css: The CSS file that styles the application, ensuring a neat and responsive design. script.js: The JavaScript file that handles client-side interactions such as registration, login, and sending/receiving messages.

Authentication Implementation:-

Registration: Users register by providing a username, password, and email. The password is hashed using bcrypt before being stored in the database. The registration endpoint (/register) handles the POST request, validates the input, hashes the password, and saves the user to the database.

Login: Users log in by providing their username and password. The login endpoint (/login) handles the POST request, verifies the user's credentials, and generates a JWT token if the credentials are valid. The JWT token is sent back to the client and used to authenticate WebSocket connections.

WebSocket Implementation:-

WebSocket Server Setup: A WebSocket server is created using the ws module and is attached to the HTTP server. The WebSocket server listens for incoming connections and messages from clients.

Connection Handling: When a WebSocket connection is established, the server extracts the JWT token from the query parameters. The server verifies the JWT token and extracts the user ID. If the token is invalid, the connection is closed.

Message Handling: When a message is received, the server parses the message, saves it to the database, and broadcasts it to all connected clients. The message event is used to handle incoming messages, ensuring they are stored and propagated to other users in real-time.

Additional Notes:

Error Handling: The server includes basic error handling to manage issues such as database connection failures and invalid user input. Environment Variables: Sensitive information like the MongoDB URI and JWT secret are stored in environment variables for security. 3).env file: MONGO_URI=your_mongo_connection_string JWT_SECRET=your_jwt_secret
