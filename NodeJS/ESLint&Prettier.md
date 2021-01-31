# ESLint와 Prettier 적용하기



```shell
# JS 문제 감지 모듈
npm installl eslint -D

# 코드 정리 모듈
npm install eslint-config-prettier

# prettier를 eslint 규칙으로 실행 시켜는 모듈
npm install eslint-plugin-prettier

# prettier와 eslint의 충돌점을 보완하는 모듈
npm install prettier -D
```



**.eslintrc.json**

```json
{
    "env": {
        "browser": true,
        "es2021": true
    },
    "extends": ["airbnb-base", "plugin:prettier/recommended"],
    "parserOptions": {
        "ecmaVersion": 12,
        "sourceType": "module"
    },
    "rules": {
        "prettier/prettier": "off",
        "no-console":"off",
        "spaced-comment":"off",
        "no-else-return":"off"
    }
}
```

