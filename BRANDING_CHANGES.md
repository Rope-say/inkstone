##一、logo与显示名称修改
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
##二、Inkstone 云端 Worker（Cloudflare Workers AI）环境变量配置文档

> 用途：对接 Cloudflare Workers AI 实现RAG知识库 适用：Obsidian + Inkstone 异地云端备用方案 注意：所有密钥建议设置为【保密环境变量 Secret】

| 环境变量名              | 填写内容模板                                                            | 说明                                                  |
| ------------------ | ----------------------------------------------------------------- | --------------------------------------------------- |
| LLM_BASE_URL       | `https://api.cloudflare.com/client/v4/accounts/{AccountID}/ai/v1` | {AccountID} 替换为 Cloudflare 账户ID；对话接口基础地址            |
| LLM_API_KEY        | `{账户API令牌}`                                                       | 创建账户API令牌后一次性复制的密钥本体，**不要添加Bearer前缀**               |
| LLM_MODEL          | `@cf/qwen/qwen3-8b-instruct`                                      | 云端对话大模型；可更换为`@cf/qwen/qwen3-14b-instruct`，切换无需重建向量库 |
| EMBEDDING_BASE_URL | `https://api.cloudflare.com/client/v4/accounts/{AccountID}/ai/v1` | 和LLM_BASE_URL保持完全一致，向量嵌入接口地址                        |
| EMBEDDING_API_KEY  | `{账户API令牌}`                                                       | 与 LLM_API_KEY 使用同一个令牌，无需单独创建                        |
| EMBEDDING_MODEL    | `@cf/baai/bge-m3`                                                 | 中文向量嵌入模型；**不建议随意更换，更换后知识库向量必须全部重建**                 |
| EMBEDDING_PROVIDER | `openai`                                                          | 固定值；程序以OpenAI兼容格式调用Workers AI接口，禁止修改                |

## 关键概念释义（可一并写入文档）

1. **AccountID（账户ID）** 位置：Cloudflare 控制面板右上角头像菜单复制；拼接在URL路径中，作用定位账户资源。
2. **账户API令牌（Bearer Token）** 自行创建，授予「账户级 Workers AI 编辑权限」，作为接口调用鉴权凭证； URL提供访问地址，令牌提供访问权限，二者必须归属同一个Cloudflare账户。

## 部署操作规范

1. 全部变量录入完成后点击【保存】；
2. 执行【重新部署Worker】，环境变量方可生效；
3. 正式导入知识库前，使用curl命令测试对话接口、嵌入接口连通性；

## 重要约束备注

1. 修改 `LLM_MODEL`：自由切换模型，**无需重建知识库向量索引**；
2. 修改 `EMBEDDING_MODEL`：向量维度变更，**必须清空知识库，重新全部向量化**；
