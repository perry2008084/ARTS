[搭建React的eslint配置](https://medium.com/@RossWhitehouse/setting-up-eslint-in-react-c20015ef35f7)

1. 使用`create-react-app app-name`创建项目
2. `npm install -g eslint`安装eslint
3. 运行`eslint --init`创建一个配置文件`.eslintrc.json`
4. 修改配置

.eslintrc.json
```
"extends": [
  "eslint:recommended",
  "plugin:react/recommended"
]
```

5. 修改npm脚本

```bash
"script": {
  "lint": "eslint src/**/*.js src/**/*.jsx"
}
```
