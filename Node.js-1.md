On this page, we begin to initiate environment node.js (Typescript)

/alert Note: ensure you installed **Node** on your machine

To download typescript global  
``` bash
 npm i typescript -g
```
# initialization
## My node setup 
  *  [node-env](https://github.com/Adosh74/Node-Env)
## initiate node porject
``` bash
  npm init 
```
## Add dependencies for format and analyzes your code 
``` bash
npm i @trivago/prettier-plugin-sort-imports @types/express "@typescript-eslint/eslint-plugin @typescript-eslint/parse eslint eslint-config-prettie eslint-plugin-prettier nodemon prettier ts-node typescript -D
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

