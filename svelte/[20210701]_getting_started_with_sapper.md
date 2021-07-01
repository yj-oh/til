# 시작하기 (with Sapper)
- https://sapper.svelte.dev/

## 프로젝트 생성
```
// rollup
npx degit sveltejs/sapper-template#rollup {project_name}
// or webpack
npx degit sveltejs/sapper-template#webpack {project_name}

cd {project_name}

npm install

npm run dev
```

## 💡 TypeScript
```
node scripts/setupTypeScript.js
```

## Sapper App Structure
```
│-- package.json
│-- src
│   │--routes
│   │   │-- # your routes here
│   │   │-- _error.svelte
│   │   `-- index.svelte
│   │-- client.js
│   │-- server.js
│   │-- service-worker.js
│   `-- template.html
│-- static
│   `-- # your files here
`-- rollup.config.js / webpack.config.js
```
