# What is PM2?
`PM2` is a production process manager for Node.js applications with a built-in load balancer. It allows you to keep applications alive forever, to reload them without downtime and to facilitate common system admin tasks. It is a cluster manager, and it will handle the clustering for us. [PM2](https://pm2.keymetrics.io/) [Github](https://github.com/Unitech/pm2)

## How to use PM2?
- we can install `PM2` globally by using the following command:

  ```bash
  npm install pm2 -g
  ```

- now we can run our code by using `PM2` by using the following command:

  ```bash
  pm2 start <filename>.js -i 0
  ```
  `-i` flag means that we want to run as many instances as we have CPU cores.

- now we can see the status of our instances by using the following command:

  ```bash
  pm2 list
  ```

- we can monitor all instances by using the following command:

  ```bash
  pm2 monit
  ```

- we can stop all instances by using the following command:

  ```bash
  pm2 delete <app name>
  ```

## CheatSheet
| **Command** | **Description** |
| --------------|-------------------|
| `pm2 start server.js --name <my-api>` | Start process with specific name. | 
| `pm2 list` | Display all processes status. | 
| `pm2 describe <PID>` | Display all information about a specific process. | 
| `pm2 stop all` | Stop all processes. |
| `pm2 stop <PName>` | Stop specific process. |
| `pm2 delete <PID>` | Remove process from pm2 list. |
