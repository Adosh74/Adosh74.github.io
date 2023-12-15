# Auth-using-OTP

1. [Description](#description)


2. [GitHub repo](https://github.com/Adosh74/Auth-using-OTP) 

3. [Postman Collection APIs](https://lively-astronaut-351758.postman.co/workspace/Team-Workspace~c51b6aa5-67a5-46bc-82e7-11cc3b1ff0c7/collection/22825654-abb654f7-8e46-477a-a155-e23d28d63bc8?action=share&creator=22825654&active-environment=22825654-2e965a94-cec4-4a02-9023-6da3733177ba)

4. [Postman Collection Json](https://github.com/Adosh74/Auth-using-OTP/blob/main/Technical_Test.postman_collection.json)

5. [How to run](#how-to-run)

6. [APIs](#apis)

7. [ERD](#erd)

## Description
Auth-using-OTP is a project developed using Node.js, Express, and Sequelize. It provides an authentication system with OTP (One-Time Password) functionality. The project includes APIs for user registration, login, and verification.

## How to run

1. clone the repo

```bash
git clone https://github.com/Adosh74/Auth-using-OTP
```

2. change directory

```bash
cd Auth-using-OTP
```

3. install dependencies

```bash
npm install
```

3. open your DBMS and create database on mySql

```sql
   create DATABASE auth_using_otp;
```

4. create new file called **.env** like **.env.example** and fill all configurations

5. import **How Found Us** data using

```bash
npm run import:data
```

6. run the server and test APIs

```bash
npm run start
```

## APIs

/api/register [POST]

**body:**

```json
{
    "firstName": "newUser",
    "lastName": "two",
    "password": "test1234",
    "mobile": "011111",
    "age": 22,
    "howFoundUs_id": 1
}
```

---

api/login [POST]

**body:**

```json
{
    "user_id": 1,
    "otp": ":otp from sms or database:"
}
```

---

/api/verify [POST]

**body:**

```json
{
    "user_id": 1,
    "otp": ":otp from sms or database:"
}
```

## ERD

**users:**
| Column | Type | Validation/Options |
| ------------------ | -------- | ------------------------------------------------------------------- |
| id | INTEGER | Auto Increment, Primary Key |
| firstName | STRING | Required |
| lastName | STRING | Required |
| age | INTEGER | Required |
| howFoundUs_id | INTEGER | Required, References 'howFoundUs' model, 'User' must be found in 'howFoundUs' model |
| verified_boolean | BOOLEAN | Required, Default: false |
| mobile | STRING | Required |
| password | STRING | Required |
| createdAt | DATE | Required, Default: Current date

**OTP:**
| Column | Type | Validation/Options |
| --------- | --------------- | --------------------------------------------------------------- |
| id | INTEGER | Auto Increment, Primary Key |
| user_id | INTEGER | Required, References 'users' model, 'id' must be found in 'users' model with CASCADE onDelete and onUpdate |
| OTP | STRING | Required |
| status | ENUM | Values: 'used', 'unused', Default: 'unused', Required |
| createdAt | DATE | Default: Current date, Required

**howFoundUs:**
| Column | Type | Validation/Options |
| ------ | ------- | ---------------------------------------- |
| id | INTEGER | Primary Key |
| value | STRING | Required, Unique |