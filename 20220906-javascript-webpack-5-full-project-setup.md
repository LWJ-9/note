[video](https://www.youtube.com/watch?v=TOb1c39m64A)

command

```pwsh
npm init -y
npm i -D webpack webpack-cli webpack-dev-server
```

create a .gitignore file

```config
node_modules
dist
```

trim packate.json

```json
{
    "private": true,
    "scripts": {
        "start": "webpack serve",
        "watch": "webpack --watch",
        "build": "webpack"
    },
    "devDependancies": {}
}
```
