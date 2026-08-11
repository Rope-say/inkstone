---

# Inkstone → G笔记 品牌替换修改记录

## 📋 修改概览

| 序号 | 文件路径                                  | 修改内容                       | 行号/位置                            |
| :--- | :---------------------------------------- | :----------------------------- | :----------------------------------- |
| 1    | `index.html`                              | `<title>` 标签                 | 第 10 行                             |
| 2    | `index.html`                              | `apple-mobile-web-app-title`   | 第 11 行                             |
| 3    | `index.html`                              | `document.title`（JS 部分）    | 第 23 行                             |
| 4    | `src/client/components/primitives.tsx`    | `Logo` 组件 SVG 图形           | 第 6-20 行                           |
| 5    | `src/shared/locales/zh-CN.ts`             | `app.document_title`           | 第 3 行                              |
| 6    | `src/shared/locales/zh-CN.ts`             | `common.product_name`          | 约第 110 行                          |
| 7    | `src/shared/locales/en-US.ts`             | `app.document_title`           | 第 3 行                              |
| 8    | `src/shared/locales/en-US.ts`             | `common.product_name`          | 约第 110 行                          |
| 9    | `src/client/features/auth/LoginPage.tsx`  | `{t("common.product_name")}`   | 第 78 行（已有语言文件控制，可不改） |
| 10   | `src/client/features/share/SharePage.tsx` | 备用名称 `?? 'Inkstone'`       | 第 144 行                            |
| 11   | Cloudflare 变量                           | `APP_NAME`                     | 控制台 → 变量和密钥                  |
| 12   | public                                    | 静态资源文件PNG以及SVG文件替换 | manifest.webmanifest内容             |

---