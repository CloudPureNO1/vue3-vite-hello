## 配置IP
package.json 中添加ip 地址
```json
  "scripts": {
    "dev": "vite --host 192.168.179.137",  // 添加 --host Ip
    "build": "run-p type-check build-only",
    "preview": "vite preview --port 4173",
    "build-only": "vite build",
    "type-check": "vue-tsc --noEmit",
    "lint": "eslint . --ext .vue,.js,.jsx,.cjs,.mjs,.ts,.tsx,.cts,.mts --fix --ignore-path .gitignore"
  },
```