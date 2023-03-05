<p align="center">
  <a href="https://transitivebullsh.it/nextjs-notion-starter-kit">
    <img alt="示例文章页面" src="https://user-images.githubusercontent.com/552829/160132094-12875e09-41ec-450a-80fc-ae8cd488129d.jpg" width="689">
  </a>
</p>

# Next.js Notion 启动套件

> 使用 Next.js 和 Notion 构建网站的完美启动套件。

[![构建状态](https://github.com/transitive-bullshit/nextjs-notion-starter-kit/actions/workflows/build.yml/badge.svg)](https://github.com/transitive-bullshit/nextjs-notion-starter-kit/actions/workflows/build.yml) [![Prettier 代码格式化](https://img.shields.io/badge/code_style-prettier-brightgreen.svg)](https://prettier.io)

## 简介

这个仓库是我用来构建我的个人博客和作品集网站 [transitivebullsh.it](https://transitivebullsh.it) 的。

它使用 Notion 作为 CMS，[react-notion-x](https://github.com/NotionX/react-notion-x)，[Next.js](https://nextjs.org/)，和 [Vercel](https://vercel.com)。

## 特点

- 只需几分钟就可以设置好（[单一配置文件](./site.config.ts)）💪
- 通过 [react-notion-x](https://github.com/NotionX/react-notion-x) 对 Notion 内容的强大支持
- 使用 Next.js，TS 和 React 构建
- 出色的页面速度
- 平滑的图片预览
- 自动社交图片
- 自动漂亮的 URL
- 自动目录
- 全面支持暗黑模式
- 通过 CMD+K / CMD+P 快速搜索
- 响应不同设备
- 针对 Next.js 和 Vercel 优化

## 演示

- [默认演示](https://nextjs-notion-starter-kit.transitivebullsh.it) - 部署自 `main` 分支
- [我的网站](https://transitivebullsh.it) - 部署自 `transitive-bullshit` 分支



## 设置

**所有配置都在 [site.config.ts](./site.config.ts) 中定义。**

这个项目需要一个较新版本的 Node.js（我们建议 >= 16）。

1. Fork / 克隆这个仓库
2. 在 [site.config.ts](./site.config.ts) 中修改一些值
3. `npm install`
4. `npm run dev` 来本地测试
5. `npm run deploy` 来部署到 vercel 💪

我尽可能地让配置变得简单 —— 你真正需要做的就是编辑 `rootNotionPageId`。

我们建议复制[默认页面](https://notion.so/7875426197cf461698809def95960ebf)作为起点，但你可以使用任何你想要的公开 notion 页面。

确保你的根 Notion 页面是**公开**的，然后复制链接到剪贴板。提取 URL 的最后一部分，看起来像 `7875426197cf461698809def95960ebf`，这是你页面的 Notion ID。

为了找到你的 Notion 工作区 ID（可选），只需将任何一个网站页面加载到浏览器中，并打开开发者控制台。有一个全局变量可以访问，叫做 `block`，它是当前页面的 Notion 数据。如果你输入 `block.space_id`，它会打印出你页面的工作区 ID。

我建议在主页上设置一个集合，包含所有的文章 / 项目 / 内容。然而，对于 Notion 工作区没有结构上的限制，所以请随意添加内容，就像在 Notion 中一样。

根据网上的搜索结果²³⁴，我为你翻译了以下内容：

## URL 路径

应用程序在开发和生产环境中使用的 URL 路径有些不同（不过把任何开发路径名粘贴到生产环境中都可以，反之亦然）。

在开发环境中，它会使用 `/nextjs-notion-blog-d1b5dcf8b9ff425b8aef5ce6f0730202`，这是一个根据页面标题生成的 slug，后面加上它的 Notion ID。我发现在本地开发过程中，始终将 Notion 页面 ID 放在最前面是非常有用的。

在生产环境中，它会使用 `/nextjs-notion-blog`，这样就更好了，因为它去掉了多余的 ID 杂乱。

Notion ID 到 slug 化页面标题的映射是在构建过程中自动完成的。只要记住，如果你计划随着时间改变页面标题，你可能想要确保旧链接仍然有效，并且我们目前没有提供检测旧链接的解决方案，除了 Next.js 的内置[重定向支持](https://nextjs.org/docs/api-reference/next.config.js/redirects)。

查看 [mapPageUrl](./lib/map-page-url.ts) 和 [getCanonicalPageId](https://github.com/NotionX/react-notion-x/blob/master/packages/notion-utils/src/get-canonical-page-id.ts) 了解更多细节。

你可以通过在数据库中添加一个 `Slug` 文本属性来覆盖每个页面的默认 slug 生成。任何有 `Slug` 属性的页面都会使用它作为 slug。

注意：如果你的工作区中有多个具有相同 slug 化名称的页面，应用程序会抛出一个错误，让你知道有重复的 URL 路径名。

根据网上的搜索结果²³⁴，我为你翻译了以下内容：

## 预览图像

<p align="center">
  <img alt="示例预览图像" src="https://user-images.githubusercontent.com/552829/160142320-35343317-aa9e-4710-bcf7-67e5cdec586d.gif" width="458">
</p>

我们使用 [next/image](https://nextjs.org/docs/api-reference/next/image) 来高效地提供图像，预览图像可以通过 [lqip-modern](https://github.com/transitive-bullshit/lqip-modern) 生成。这样我们就可以得到非常优化的图像支持，让图像看起来更光滑。

预览图像是**默认启用**的，但它们可能会生成缓慢，所以如果你想要禁用它们，可以在 `site.config.ts` 中将 `isPreviewImageSupportEnabled` 设置为 `false`。

### Redis

如果你想要缓存生成的预览图像，以加快后续的构建速度，你需要首先设置一个外部的 [Redis](https://redis.io) 数据存储。要启用 redis 缓存，可以在 `site.config.ts` 中将 `isRedisEnabled` 设置为 `true`，然后设置 `REDIS_HOST` 和 `REDIS_PASSWORD` 环境变量指向你的 redis 实例。

你可以在本地添加一个 `.env` 文件来做这件事：

```bash
REDIS_HOST='TODO'
REDIS_PASSWORD='TODO'
```

如果你不确定使用哪个 Redis 提供商，我们推荐 [Redis Labs](https://redis.com)，它提供了一个免费计划。

注意预览图像和 redis 缓存都是可选功能。如果你不想处理它们，只需在你的站点配置中禁用它们。

## 样式

所有定制 Notion 内容的 CSS 样式都位于 [styles/notion.css](./styles/notion.css) 中。它们主要针对 react-notion-x 导出的全局 CSS 类名 [styles.css](https://github.com/NotionX/react-notion-x/blob/master/packages/react-notion-x/src/styles.css)。

每个 notion 块都有自己独特的类名，所以你可以这样针对单个块：

```css
.notion-block-260baa77f1e1428b97fb14ac99c7c385 {
  display: none;
}
```


## 暗黑模式

<p align="center">
  <img alt="Light Mode" src="https://transitive-bs.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F83ea9f0f-4761-4c0b-b53e-1913627975fc%2Ftransitivebullsh.it_-opt.jpg?table=block&id=ed7e8f60-c6d1-449e-840b-5c7762505c44&spaceId=fde5ac74-eea3-4527-8f00-4482710e1af3&width=2000&userId=&cache=v2" width="45%">
&nbsp; &nbsp; &nbsp; &nbsp;
  <img alt="Dark Mode" src="https://transitive-bs.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fc0839d6c-7141-48df-8afd-69b27fed84aa%2Ftransitivebullsh.it__(1)-opt.jpg?table=block&id=23b11fe5-d6df-422d-9674-39cf7f547523&spaceId=fde5ac74-eea3-4527-8f00-4482710e1af3&width=2000&userId=&cache=v2" width="45%">
</p>

暗黑模式完全支持，并可以通过页脚中的太阳/月亮图标切换。

## 自动社交图片

<p align="center">
  <img alt="Example social image" src="https://user-images.githubusercontent.com/552829/162001133-34d4cf24-123a-4569-a540-f683b22830d1.jpeg" width="600">
</p>

所有的开放图形和社交元标签都是从您的 Notion 内容生成的，这使得社交分享默认看起来很专业。

社交图片是使用 [Vercel OG Image Generation](https://vercel.com/docs/concepts/functions/edge-functions/og-image-generation) 自动生成的。您可以通过编辑 [api/social-images.tsx](./pages/api/social-image.tsx) 来调整社交图片的默认 React 模板。

您可以在生产环境中查看一个示例社交图片 [here](https://transitivebullsh.it/api/social-image?id=dfc7f709 ae3e 42c6 9292 f6543d5586f0)。


## 自动目录

  <p align="center">
    <img alt="平滑的目录滚动监听" src="https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fcb2df62d-9028-440b-964b-117711450921%2Ftoc2.gif?table=block&id=d7e9951b-289c-4ff2-8b82-b0a61fe260b1&cache=v2" width="240">
  </p>

  默认情况下，每篇文章页面都会在桌面上显示一个`aside`作为目录。它使用**滚动监听**逻辑，在用户滚动文档时自动更新当前章节，并且使得在不同章节之间跳转非常容易。

  如果一个页面的目录项少于`minTableOfContentsItems`（默认为3），则目录将被隐藏。它也会在首页和浏览器窗口太小的情况下隐藏。

  这个目录使用了和Notion内置的目录块相同的逻辑（参见[getPageTableOfContents](https://github.com/NotionX/react-notion-x/blob/master/packages/notion-utils/src/get-page-table-of-contents.ts)了解底层逻辑）。

## 响应式

  <p align="center">
    <img alt="移动端文章页面" src="https://user-images.githubusercontent.com/552829/160132983-c2dd5830-80b3-4a0e-a8f1-abab5dbeed11.jpg" width="300">
  </p>


## 分析

  分析是一个可选的功能，如果你想要的话，很容易开启。

### Fathom Analytics

[Fathom](https://usefathom.com/ref/42TFOZ) 提供了一个轻量级的 Google Analytics 替代方案。

要启用，只需添加一个 `NEXT_PUBLIC_FATHOM_ID` 环境变量，它只会在生产环境中使用。

### PostHog Analytics

[PostHog](https://posthog.com/) 提供了一个轻量级的，**开源**的 Google Analytics 替代方案。

要启用，只需添加一个 `NEXT_PUBLIC_POSTHOG_ID` 环境变量，它也只会在生产环境中使用。

## 环境变量

如果您使用 Redis、分析或任何其他需要环境变量的功能，那么您需要[将它们添加到您的 Vercel 项目](https://vercel.com/docs/concepts/projects/environment-variables) 中。

如果您想用 GitHub Actions 测试您的 redis 构建，那么您需要编辑[默认构建操作](./.github/workflows/build.yml) 来添加 `REDIS_HOST` 和 `REDIS_PASSWORD`。这里有一个[来自我的个人分支的例子](https://github.com/transitive-bullshit/nextjs-notion-starter-kit/blob/transitive-bullshit/.github/workflows/build.yml#L17-L21)。您还需要将这些环境变量添加到您的 GitHub 仓库作为[仓库密钥](https://docs.github.com/en/actions/security-guides/encrypted-secrets)。




## 贡献

  请参阅[贡献指南](contributing.md)并加入我们令人惊叹的[贡献者](https://github.com/transitive-bullshit/nextjs-notion-starter-kit/graphs/contributors)名单！

## 许可证

  MIT © [Travis Fischer](https://transitivebullsh.it)

  通过<a href="https://twitter.com/transitive_bs">关注我在推特上的<img src="https://storage.googleapis.com/saasify-assets/twitter-logo.svg" alt="twitter" height="24px" align="center"></a>来支持我的开源工作

