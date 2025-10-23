# 第三方许可证声明（Third-Party Notices)

本项目以“单文件、纯前端”的方式，通过 CDN 在运行时加载以下第三方库。它们的许可证分别如下：

---

## 1) Marked
- 名称：Marked（Markdown 渲染器）
- 使用方式：CDN 引入（`https://cdn.jsdelivr.net/npm/marked@16.4.1/lib/marked.umd.min.js`）
- 版本：16.4.1（以 `index.html` 中的 CDN 版本为准）
- 仓库：https://github.com/markedjs/marked
- 许可证：MIT License
- 许可证原文（链接）：https://github.com/markedjs/marked/blob/master/LICENSE.md

MIT 摘要（非完整文本）：
- 允许自由使用、复制、修改、合并、出版、分发、再许可、销售软件副本；
- 需在软件的所有副本或重要部分中包含版权声明与许可声明；
- 本软件按“现状”提供，不提供任何担保或责任。

如需将 Marked 与本项目一起打包或再分发，请确保在分发包中包含其 MIT 许可证与版权声明。

---

## 2) DOMPurify
- 名称：DOMPurify（HTML 清理器，可选）
- 使用方式：CDN 引入（`https://cdn.jsdelivr.net/npm/dompurify@3.3.0/dist/purify.min.js`）
- 版本：3.3.0（以 `index.html` 中的 CDN 版本为准）
- 仓库：https://github.com/cure53/DOMPurify
- 许可证：双许可 Apache License 2.0 或 Mozilla Public License 2.0（二选一）
- 许可证原文（链接）：
  - Apache-2.0: https://www.apache.org/licenses/LICENSE-2.0
  - MPL-2.0: https://www.mozilla.org/MPL/2.0/

说明与合规建议：
- 本项目通过 CDN 以“未修改”的形式调用 DOMPurify。一般情况下，选择 Apache-2.0 会更便于在闭源/商用场景分发。
- 若将 DOMPurify 与本项目一起“打包分发”（而非运行时从 CDN 加载）：
  - 建议将 DOMPurify 许可证（至少其中一种）包含在你的分发包中；
  - 若选择 MPL-2.0，请关注其对“修改过的源码文件”的开源要求（文件级别 copyleft）；
  - 若选择 Apache-2.0，请在需要时包含 NOTICE/版权信息，且保留许可证文本。

---

## 适用范围与声明
- 本仓库自身采用 MIT 许可证（见 `LICENSE`）。本仓库代码的许可证不改变第三方库的许可证；第三方库依其各自的许可证条款授权与约束。
- 当前本仓库未内置上述库的源代码或压缩文件，而是通过 CDN 在浏览器中按需加载。若你将本项目“打包/离线分发”，请同时遵守相应第三方库的许可证要求。

最后更新：与 `index.html` 中的 CDN 版本号保持一致（Marked 16.4.1，DOMPurify 3.3.0）。如你升级这些依赖的版本，请同步更新本文件。
