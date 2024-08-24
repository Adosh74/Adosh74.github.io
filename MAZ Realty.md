# Table of Contents

- [Introduction](#introduction)

- [Core Features](#core-features)

- [Installation](#installation)

- [Technologies](#technologies)

- [APIs](#apis)

- [Documentation](#documentation)
  - [Class Diagram](#class-diagram)
  - [Authentication Process](#authentication-process)
  - [Property Management Process](#property-management-process)
  - [Chat Process](#chat-process)
  - [Contract Validation Process](#contract-validation-process)
  - [Lawyer Services Process](#lawyer-services-process)

# Introduction

This is the source code for the website of Maz Realty, a real estate based in Egypt. The application is based on client/server architecture, where the client is a web browser and mobile device, and the server is a Node.js server. The server is responsible for serving the client with the website's content and handling the requests from the client.
[Live](https://mazrealty.live)
<https://mazrealty.live>

# Core Features

- User can register and login.
- User can view the properties.
- Users can search for properties with advanced search options.
- User can contact the property owner via WhatsApp, email and phone.
- User can view the property location on Google Maps.
- Users can view the property images in a gallery.
- User can view the property details.
- User can chat with the property owner via **MAZ Realty** chat.
- The user can book lawyer services to check the property documents.
- The user can upload his property for sale or rent.
- The user receives a welcome  email when registering.
- The user receives an email when booking lawyer services.
- User receives email for lawyer services feedback about the property documents.

# Installation

```bash
# Clone the repository
git clone https://github.com/Adosh74/mazrealty.live

# Change the directory
cd mazrealty.live

# Install the dependencies
npm install

# Install the client and server dependencies
npm run build

# Create .env file in the root directory like .env.example file

# Start the whole application
npm run start

# Now the application is running on http://localhost:<the port in the .env file> 
```

# Technologies

- Node.js
- Express.js
- TypeScript
- MongoDB
- Mongoose
- Validator
- Redis (for caching)
- JWT (for authentication)
- multer (for file uploading)
- sharp (for image processing)
- nodemailer (for sending emails)
- Pino (for logging)
- React.js
- Vite
- Axios
- SCSSk
- Flutter
- Dart
- WhatsApp API

# APIs

**users:**

- `POST /api/v1/users/` - Create a new user
- `GET /api/v1/users/` - Get all users
- `GET /api/v1/users/:id` - Get a user
- `PATCH /api/v1/users/:id` - Update a user (only for admin)
- `DELETE /api/v1/users/:id` - Delete a user (only for admin)
- `GET /api/v1/users/me` - Get the current user (only for authenticated users)
- `PATCH /api/v1/users/updateMe` - Update the current user (only for authenticated users)
- `PATCH /api/v1/users/updateMyPassword` - Update the current user's password (only for authenticated users)

**auth:**

- `POST /api/v1/auth/signup` - Sign up and get a token
- `POST /api/v1/auth/login` - Log in and get a token
- `GET /api/v1/auth/logout` - Log out and clear the token from the cookie

**properties:**

- `POST /api/v1/properties/` - Create a new property
- `GET /api/v1/properties/` - Get all properties
- `GET /api/v1/properties/:id` - Get a property
- `PATCH /api/v1/properties/:id` - Update a property (only for admin and property owner)
- `DELETE /api/v1/properties/:id` - Delete a property
- `PATCH api/v1/properties/add-images/:id` - Add images to a property (only for admin and property owner)
- `PATCH /api/v1/properties/delete-image/:id` - Delete an image from a property (only for admin and property owner)

- get all properties query options:
  - `GET /api/v1/properties/?sort=-price` - Sort by price descending
  - `GET /api/v1/properties/?fields=name,price` - Select only name and price fields
  - `GET /api/v1/properties/?limit=5` - Limit the number of results to 5
  - `GET /api/v1/properties/?page=2&limit=5` - Pagination, get the second page with 5 results

**user favorites:**

- `POST /api/v1/users/favorites/:id` - Add a property to favorites (only for authenticated users)
- `DELETE /api/v1/users/favorites/:id` - Remove a property from favorites (only for authenticated users)
- `GET /api/v1/users/favorites` - Get all favorite properties of the current user (only for authenticated users)

**lawyer:**

- `GET /api/v1/lawyers/not-approved` - Get all lawyers that are not approved (only for lawyer and admin)
- `PATCH api/v1/lawyers/approve-property/:id` - Approve a lawyer (only for lawyer and admin)

**cities:**

- `GET /api/v1/cities/` - Get all cities

**socket events:**

`newUser` - when is connected and authenticated (pass the userId)

`sendMessage` - when a user sends a message (
  pass the object having {
  **receiverId**: receiverId from response,
  **data**: all response
}
  
)

# Documentation

## Class Diagram

![](/public/1620e419e2057b53a1f6ce6efa2cb37e56eca2cf96a91c0d407262e6581aa577.png)

## Authentication Process

![](/public/e7e6a1e48becd1bccc13e762701e7c229a566fe17f98929708df7243ec49a326.png)

## Property Management Process

![](/public/f5d069aecb5beab86bba564729afb0edc84b6f48eb1332d9835cc53e655232ca.png)

## Chat Process

![](/public/80e41fa928f45160831a4dd4bc04cd2121520a564024708b525fe96a7167dce8.png)

## Contract Validation Process

![](/public/38986a93a522148716c4c8852a3b7f0e748072b7cb091863dabb934541af390b.png)

## Lawyer Services Process

![](/public/87977a7f91476a340156533d0087616826412cc3047ba69b4f659e5de912867f.png)

#projects 
#nodejs