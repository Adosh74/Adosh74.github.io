# Documentation-System

1. [Introduction](#introduction)
2. [Core Features](#core-features)
4. [Note](#note)
5. [Getting Started](#getting-started)
6. [Technologies and Tools](#technologies-and-tools)
7. [ERD](#erd)
8. [GitHub repo](#repo)

## Introduction

This app is where you will store your Software Development Life Cycle Documentation. This application includes some common phases of software development: Project Initiation, Planning, Requirements (Analysis), Design, Development, Testing, Deployment, and Maintenance. Each phase will have its documentation. Each documentation will have its files. Each file will have its version. Each version will have its content. Each content will have its author. Each author will have its name.

## note:
> - I tried uploading files with the main server but it's not working because apollo/server v4 has an issue and restriction with file upload, so I created another server for uploading files.

> - If apollo/server v4 fixes this issue, I will update this app.

## Core Features

-   Create, Read, Update, and Delete (CRUD) documentation for each software development life cycle phase.

-   Get a list of all documentation for each software development life cycle phase.

-   Get all files for each documentation.

-   Best practices for GraphQL API design.

-   Scalable folder structure for GraphQL API design.

## Getting Started
``` bash
# clone the repo
git clone https://github.com/Adosh74/Documentation-System

# Move to the project directory
cd Documentation-System

# install all dependencies.
npm run build

# sync prisma with database
npm run prisma:deploy
npm run prisma:generate
# After that, fill the .env file with your database credentials

# Start all processes with one command
npm start
```
- Now, you can access the Next.js app on 
    ```http
    http://localhost:3000
    ```
- And GraphQL Playground on 
    ```http 
    http://localhost:3001/graphql
    ```

## Technologies and Tools

-   Node.js
-   Express.js
-   TypeScript
-   GraphQL
-   Apollo Server
-   Apollo Client
-   PostgreSQL
-   Prisma
-   Next.js

## Repo
https://github.com/Adosh74/Documentation-System

## ERD

### Entity Relationship Diagram

### Table of Contents

**Project:**

| Column          | Type         |
| --------------- | ------------ |
| id              | string: uuid |
| title           | string       |
| startIn         | Date         |
| endIn           | Date         |
| objective       | string       |
| project_manager | string       |
| budget          | number       |
| scope           | string       |

**SRS:**

| Column            | Type         |
| ----------------- | ------------ |
| id                | string: uuid |
| p_id              | string: uuid |
| introduction      | string       |
| purpose           | string       |
| intended_audience | string       |
| description       | string       |
| requirements      | string       |
| use_case          | string       |

**SDD:**

| Column | Type         |
| ------ | ------------ |
| id     | string: uuid |
| p_id   | string: uuid |
| uml    | string[]     |
