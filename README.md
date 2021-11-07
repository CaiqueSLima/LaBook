# LaBook

## Install

```sh
npm install
```

## Run Build

```sh
npm run build
```

## Run Dev

```sh
npm run dev
```

## Data Structure  
  
* ## Users
  * id
  * name
  * email
  * password 

* ## Posts 
  * id
  * picture
  * creationDate
  * type: `"normal" || "evento"`
  * userId
   
---

## Table Creation - MySql

```sql
CREATE TABLE labook_users(
  id VARCHAR(50) NOT NULL PRIMARY KEY,
  name VARCHAR(255) NOT NULL,
  email VARCHAR(255) NOT NULL UNIQUE,
  password VARCHAR(255) NOT NULL
);
```
```sql
CREATE TABLE labook_posts(
  id VARCHAR(50) NOT NULL PRIMARY KEY,
  picture VARCHAR(255) NOT NULL,
  description VARCHAR(255) NOT NULL,
  creation_date DATE NOT NULL,
  type ENUM("normal", "evento"),
  user_id VARCHAR(50) NOT NULL,
  FOREIGN KEY (user_id) REFERENCES labook_users(id)
);
```
---

## ENDPOINTS 

* ## User SignUp
  * Method: POST
  * Path: `/signup`
  * Body:
    * name (obrigatório)
    * email (obrigatório)
    * password (obrigatório)
  * Response:
    * message
    * token

* ## User Login
  * Method: POST
  * Path: `/login`
  * Body:
    * email (obrigatório)
    * password (obrigatório)
  * Response:
    * token

* ## Create post
  * Method: POST
  * Path: `/post`
  * headers:
    * authorization: token
  * Body:
    * picture (obrigatório)
    * creationDate (obrigatório)
    * type: `"normal" || "evento"` (obrigatório)


* ## Get post by id
  * Method: GET
  * Path: `/post/:id`
  * Response: (return an error if nothing is found)
    * id
    * picture
    * description
    * creationDate
    * type
    * userId

* ## Get task by id
  * Method: GET
  * Path: `/task/:id`
  * Response: (return an error if nothing is found)
    * id
    * picture 
    * description
    * creationDate (formato `DD-MM-YYYY`)
    * type
    * userId
