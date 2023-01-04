#Node


## fs
 #### read file
  
  ```
  const fs = require('fs')
  const text = fs.readFileSync('./test.txt', 'utf-8')
  console.log(text);
  ```
  
  
  #### read and write in file
  
  ```
  const fs = require('fs')

  const textIn = fs.readFileSync('./test.txt', 'utf-8')


  const textOut =  `After writing * ${textIn} 
  Date: ${Date()}`
  fs.writeFileSync('./out.txt', textOut)
```