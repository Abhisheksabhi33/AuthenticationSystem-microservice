
---

# JWT Authentication and Microservices Integration in Node.js

## Overview

 This project focuses on creating a JWT-based authentication system within a Node.js environment.
 It also involves integrating microservices Creating a Gateway API to interact with the microservices and implementing a public API with endpoints using an API key.
 It mainly focuses on two microservices, one for user authentication (main-service) and another for a public API service.

 ### Installation Steps

 To run the application, you need to have Node.js and npm installed on your system. You can download Node.js </br>
   - for Windows from [Click here...](https://nodejs.org/en/download/) </br>
   - for Linux from [Click here...](https://nodejs.org/en/download/package-manager/). </br>
   - for Mac from [Click here...](https://nodejs.org/en/download/package-manager/). </br>
   - and MongoDB atlas from [Click here...](https://www.mongodb.com/cloud/atlas/register). </br>
   - also, you need to have npm installed on your system. </br>

 check if node and npm are installed on your system by running the following commands in your terminal.

 ```bash
  node -v
  npm -v
  ```
  if you get the version of node and npm installed on your system then you are good to go.

## Follow if Using Github
- Clone the repository:  `git clone https://github.com/Abhisheksabhi33/authSystem-microservice.git`
- Install dependencies: `npm install`
- Create a `.env` file in the root directory and add the following environment variables:
  - `PORT`: The port number for the Gateway server to run on. The default is `8000`.
  - `PORT1`: The port number for the main server to run on. The default is `8001`.
  - `PORT2`: The port number for the public API server to run on. The default is `8002`.
  - `MONGO_URI`: The MongoDB connection string.
  - `JWT_SECRET`: The secret key for JWT token generation.
  - `baseurl`:  The base url.
  
- Start the server: `npm start`

## Follow If having Zip File
- Just extract the zip file and open it in any code editor.
- Open the terminal and run the following command to install all the dependencies.
  
  ```bash
  npm install
  ```
  ```bash
   npm start
  ```

- I have used concurrently to run all three servers at the same time.
- our main server will run on port 8001, the public API server will run on port 8002 and the gateway server will run on port 8000.  

### API Endpoints

For using the API endpoints, you can use Postman or any other API testing tool of your choice. The base URL for the API is `http://localhost:8000`.

 ## Main Service

 - `/api/user/register`
      - **Method**: POST
      - **Description**: Register users and generate JWT tokens.
      - **Request**:
      ```json
      {
        "firstName": "manish",
        "lastName": "yadav",
        "email": "manish@email.com",
        "password": "manish12345"
      }
      ```
    - **Response**:
      - I have displayed the hash Password for showing hash functionality.
      
      ```json
      {
      "message": "User registered successfully",
      "firstName": "manish",
      "lastName": "yadav",
      "email": "manish@email.com",
      "apiKey": "635815fb7c234dd8930578c49a11e1f3",
      "password": "$2b$10$.b2aiXM85v7rcLGXJjfqAej70DWT1CjfMa3yfdKjgtK55Kt1Qjvd."
      }
      ```
      ![Screenshot 2023-12-24 132416](https://github.com/Abhisheksabhi33/AuthenticationSystem-microservice/assets/87107030/c4fb3c61-8082-44c4-9aaa-1534d1ed9f98)


- `/api/user/login`
     - **Method**: POST
     - **Description**: Authenticate users and generate JWT tokens.
     - **Request**:
     ```json
       {
       "email": "manish@email.com",
       "password": "manish12345"
       }
     ```
 - **Response**:
  ```json
       {
       "message": "User logged in successfully",
       "apiKey": "635815fb7c234dd8930578c49a11e1f3"
       }
   ```



![Screenshot 2023-12-24 132436](https://github.com/Abhisheksabhi33/AuthenticationSystem-microservice/assets/87107030/2a06afb7-6a3a-4f2d-8b59-841e7da80972)

- Auth Token is saved in the cookie section



![Screenshot 2023-12-24 132458](https://github.com/Abhisheksabhi33/AuthenticationSystem-microservice/assets/87107030/495d8933-9bee-4e42-9dcd-9a7c3a0352fc)


 - `/api/user/add-candidate`
      - **Method**: POST
      - **Description**: Add candidate details to the database.
      - **Request**:
        ```json
        {
        "firstName" : "mohan",
        "lastName" : "mishra",
        "email" : "mohan@email.com"
        }
        ```
      - **Response**:
        ```json 
        {
        "message": "Candidate added successfully",
        "firstName": "mohan",
        "lastName": "mishra",
        "email": "mohan@email.com"
        }
        ```


  ![Screenshot 2023-12-24 132540](https://github.com/Abhisheksabhi33/AuthenticationSystem-microservice/assets/87107030/1f3da33a-5bea-488a-bf5c-a3d15e4c3d86)


  - If we remove the auth token from cookie the we log out and can not access protected routes

    
![Screenshot 2023-12-24 132638](https://github.com/Abhisheksabhi33/AuthenticationSystem-microservice/assets/87107030/bbab8860-c858-44b7-a2e5-c4c3cda3f3eb)



  - `/api/user/get-candidate`
  - **Method**: GET
  - **Description**: Get candidate details from the database for the current user.
  - **Request**:

  - **Response**:
    ```json
    {
    "message": "Candidate fetched successfully",
    "candidates": [
        {
            "_id": "6587dabaaf17f3276d63e400",
            "firstName": "mohan",
            "lastName": "mishra",
            "email": "mohan@email.com",
            "__v": 0
        }
    ]
    }
    ```


    
![Screenshot 2023-12-24 132704](https://github.com/Abhisheksabhi33/AuthenticationSystem-microservice/assets/87107030/9abc17ca-4f09-4dd2-a1cb-d3f168398c9f)


## Public API Microservice
   - `/api/public/profile/:apikey`
     
  - **Method**: POST
  - **Description**: Get user profile details from the database for the current user using public api key.
  - **Request**:
  - **Response**:
    ```json
    {
    "userProfile": {
        "firstName": "manish",
        "lastName": "yadav",
        "email": "manish@email.com",
        "apikey": "635815fb7c234dd8930578c49a11e1f3"
       }
      }
    ```


![Screenshot 2023-12-24 132719](https://github.com/Abhisheksabhi33/AuthenticationSystem-microservice/assets/87107030/e148c079-6005-4c64-bcc4-d929f782aecf)


- `/api/public/candidate/:apikey`
   - **Method**: GET
   - **Description**: Get All candidate details from the database for the current user using public api key.
   - **Request**:
   - **Response**:
     ```json
      {
      "candidates": [
        {
            "_id": "6587dabaaf17f3276d63e400",
            "firstName": "mohan",
            "lastName": "mishra",
            "email": "mohan@email.com",
            "__v": 0
        }
      ]
     }
       ```

     
![Screenshot 2023-12-24 132733](https://github.com/Abhisheksabhi33/AuthenticationSystem-microservice/assets/87107030/e2620b45-44e7-4605-a776-4e0e377f9a15)

### Main Service

The core service handles user authentication and authorization using JWT tokens. It includes functionalities to:

- **User Registration**: Generate JWT tokens upon successful registration.
- **User Login**: Authenticate users for protected routes.

- **Protected Routes**: Implement protected routes that require user authentication and authorization.
- **add-candidate**: Add candidate details to the database.
- **get-candidate**: Get All candidate details from the database for the current user.

### Public API Microservice

This microservice provides a public API key to access main service routes without requiring email and password authentication. Key functionalities include:

- **Authorization with API Key**: Implemented a public API with endpoints authorized using an API key.
- **API Key Generation**: Generate API keys for users upon successful registration.
- **profile**: Getting user profile details from the database for the current user using the public API key.
- **get-candidate**: Getting All candidate details from the database for the current user using the public API key.


## Project Components

### User Authentication

The main service employs JWT for user authentication, ensuring secure login and authorization for accessing protected endpoints.
for the public API microservice, it uses public API key authorization to access the endpoints.

### Database Management

The main service interacts with a database to store user information and manage candidate data. The database schema includes fields for users, public API keys, and candidate details.

## Database Schema
In the database, there are three collections, users, apikeys, and candidates.
- **users**: This collection stores the user details.
  - **apiKey**:  A string field to store an API key associated with the user.
  - **candidates**:  An array of references to Candidate models using their ObjectIds.
  - **firstName**:  The first name of the user. It's a required string with a minimum length of 3 characters.
  - **lastName**:  The last name of the user. Also required with a minimum length of 3 characters.
  - **email**:  The email address of the user. It's required, unique, and trimmed.
  - **password**: The password for the user account, which is required and must have a minimum length of 8 characters.

  ``` bash
   {
  apiKey: {
    type: String,
  },
  candidates: [
    {
      type: mongoose.Schema.Types.ObjectId,
      ref: "Candidate",
    },
  ],
  firstName: {
    type: String,
    required: true,
    trim: true,
    minlength: 3,
  },
  lastName: {
    type: String,
    required: true,
    trim: true,
    minlength: 3,
  },
  email: {
    type: String,
    required: true,
    trim: true,
    unique: true,
  },
  password: {
    type: String,
    required: true,
    minlength: 8,
  },
  }
  ```

- **apikeys**: This collection stores the public API keys for the users.
    - **key**:  A string field to store an API key associated with the user.
    - **user**:  A reference to the User model using its ObjectId.
    
    ``` bash
    {
    key: {
        type: String,
        required: true,
        unique: true,
    },
    user: {
        type: mongoose.Schema.Types.ObjectId,
        ref: 'User',
        unique: true,
    },
    } 

    ```

- **candidates**: This collection stores the candidate details for the users.
    - **firstName**:  The first name of the candidate. It's a required string with a minimum length of 3 characters.
    - **lastName**:  The last name of the candidate. Also required with a minimum length of 3 characters.
    - **email**:  The email address of the candidate. It's required, unique, and trimmed.
    - **userId**: Reference to the User model using its ObjectId. This field establishes a relationship between a candidate and a user, indicating that a candidate belongs to
                   a specific user.

    ``` bash
    {
  firstName: {
    type: String,
    required: true,
    trim: true,
    minlength: 3,
  },
  lastName: {
    type: String,
    required: true,
    trim: true,
  },
  email: {
    type: String,
    required: true,
    unique: true,
    trim: true,
  },
  
  userId: {
    type: mongoose.Schema.Types.ObjectId,
    ref: "User",
  },

  } 
    ```

### Public API Microservice

The microservice offers a public API that doesn’t require traditional login credentials but operates based on public API key authorization. It provides access to functionalities by using the public API key.

### Interconnection

The main service communicates seamlessly using gateway API (proxy middleware) with the main service and public API microservice, accessing its functionalities to enhance user experience and interaction.

## Tools And Technologies Used

- Node.js
- Express
- MongoDB 
- Mongoose (for database interaction)
- JWT for authentication
- Bcrypt for password hashing
- Nodemon for development
- Postman for API testing

---
