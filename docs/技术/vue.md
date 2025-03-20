卡在第一步折戟

### 导入element-plus'的时候报错

```ts
import 'element-plus/dist/index.css';
import ElementPlus from 'element-plus';

app.use(ElementPlus)
```

Cannot find module 'element-plus' or its corresponding type declarations.ts(2307)

需要在某一个，比如tsconfig.app.json里面的compilerOptions下加上这句话

"types": ["element-plus/global"]


![ArgoCD Health](https://img.shields.io/endpoint?url=https://argocd-dev.southeastasia.azure.wistron.com/api/v1/applications/avtsdm-psc-ssmapi&label=Health&query=$.status.health.status&color=green)
![ArgoCD Sync](https://img.shields.io/endpoint?url=https://argocd-dev.southeastasia.azure.wistron.com/api/v1/applications/avtsdm-psc-ssmapi&label=Sync&query=$.status.sync.status&color=blue)
