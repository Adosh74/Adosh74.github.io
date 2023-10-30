On this page, we begin to initiate node.js (Typescript) with eslint, prettier, and ts-node-dev.

/alert Note: ensure you installed **Node** on your machine

- To download **typescript global** ` npm i typescript -g `
- To download **yarn** global ` npm i yarn -g `

# 🏃 Quick Start with My Node Config
```bash
# clone my repo
git clone https://github.com/Adosh74/Node-Env

# change directory to Node-Env
cd Node-Env

# install dependencies
yarn

# remove .git folder
rm -rf .git

## Now you can start project ✌
```

# Initialization
## Initiate node porject
``` bash
  npm init -y
```
## Add dependencies for format and analyzes your code 
``` bash
# add dependencies.
yarn add express typescript 

# add dev dependencies.
yarn add @trivago/prettier-plugin-sort-imports prettier eslint @types/express @typescript-eslint/eslint-plugin @typescript-eslint/parser eslint-config-prettier eslint-plugin-prettier ts-node ts-node-dev  -D
```
## Create JSON file for typescript configuration called **tsconfig.json**
**tsconfig.json**
``` json
{
  "compilerOptions": {
    "target": "es2016",                                  
    "module": "commonjs",                                
    "rootDir": "./src",                                  
    "outDir": "./dist",                                   
    "esModuleInterop": true,                            
    "forceConsistentCasingInFileNames": true,            
    "strict": true,                                            
    "skipLibCheck": true                               
  }
}

```

## Create JSON  file for a prettier configuration to formatter called .prettierrc.json
- This is my configuration you can make your form [prettier-site](https://prettier.io/playground/)
**.prettierrc.js**
``` json
{
	"trailingComma": "es5",
	"useTabs": true,
	"semi": true,
	"singleQuote": true,
	"quoteProps": "as-needed",
	"importOrder": [
		"^@core/(.*)$",
		"^@server/(.*)$",
		"^@ui/(.*)$",
		"^[./]"
	],
	"importOrderSeparation": true,
	"importOrderSortSpecifiers": true,
	"printWidth": 70
}
```

## Create file for eslint configuration to find and fix problems called .eslintrc.js
**.eslintrc.js**
``` javascript
module.exports = {
	env: {
		browser: true,
		es2021: true,
		node: true,
	},
	extends: [
		'eslint:recommended',
		'plugin:@typescript-eslint/recommended',
		'prettier',
	],
	overrides: [],
	parser: '@typescript-eslint/parser',
	parserOptions: {
		ecmaVersion: 'latest',
		sourceType: 'module',
	},
	plugins: ['@typescript-eslint', 'prettier'],
	rules: {
		'prettier/prettier': ['error', { endOfLine: 'auto' }],
		'no-console': 0,
		'no-var': 2,
		'prefer-const': 'off',
	},
};
```


#nodejs

