   
# Eary-Syetem [GitHub](https://github.com/Adosh74/Eary-System)
* A project called **Eary** helps people check their hearing problems. 
* The backend should be in (node.js & Express.js) and the Frontend should be in React.js.

![](/public/5b46697c5e130bbae3ebd276cd277ec6525f4e033c20b7f4ae7ea00822d7ab15.png)


## ERD
![](/public/4400e659d3769b4eb2dec3733af03285a7f121ba3143937c9e11780a8253ac4a.png)

## Usage
1. download dependencies.
    ``` bash
        npm install
    ```
  2. create file **.env** like **.env_templete** and write your information.
  3. make sure you have MySQL on your machine.
  4. open MySQL and create a new database called **EARY_SYSTEM**.
      ```SQL
        CREATE DATABASE EARY_SYSTEM; 
      ```
  5. download [**Thunder Client**](https://www.thunderclient.com/) extinction on VS Code.
  6. import **[thunder-collection_EARY-SYSTEM.json](https://github.com/Adosh74/Eary-System/blob/main/Thunder%20Client/thunder-collection_EARY-SYSTEM.json)** from Thunder Client folder.
  7. test all endpoints in collections.
  8.  download front-end dependencies.
      ``` bash
        cd client
      ```
      ``` bash
        npm install
      ```
  9. Run back-end. open the terminal in a root **project folder** and write
       ``` bash
         npm run dev
       ````
10. Run front-end. open the terminal in a **client folder** and write
      ``` bash
        npm run start
      ```
## Show
<video controls src="/public/updated5.mp4"></video>
<video controls src="/public/eary-system-brave-2023-05-12-17-11-00_W2J9Pp1w.mp4"></video>






#projects