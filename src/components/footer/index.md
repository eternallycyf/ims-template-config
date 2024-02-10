---
title: footer
---

## footer

```ts
export const footer = (repo: string) => [
  {
    title: '相关依赖',
    items: [
      {
        title: 'ims-view-pc',
        url: 'https://ims-view.site/components',
        openExternal: true,
      },
      {
        title: '@ims-view/hooks',
        url: 'https://ims-view.site/hooks',
        openExternal: true,
      },
      {
        title: '@ims-view/utils',
        url: 'https://ims-view.site/utils',
        openExternal: true,
      },
      {
        title: '@ims-view/chart',
        url: 'https://ims-view.site/charts',
        openExternal: true,
      },
      {
        title: 'ims-graph',
        url: 'https://ims-graph.vercel.app/components/graph-chart',
        openExternal: true,
      },
      {
        title: 'ims-indexed-db',
        url: 'https://ims-indexed-db.vercel.app/',
        openExternal: true,
      },
      {
        title: '@ims-view/components',
        url: 'https://github.com/eternallycyf/components',
        openExternal: true,
      },
      {
        title: '@ims-view/editor',
        url: 'https://ims-editor.vercel.app/',
        openExternal: true,
      },
      {
        title: 'ims-react-directive',
        url: 'https://github.com/eternallycyf/ims-react-directive',
        openExternal: true,
      },
    ],
  },
  {
    title: '帮助',
    items: [
      {
        title: 'GitHub',
        url: `https://github.com/eternallycyf/${repo}`,
        openExternal: true,
      },
      {
        title: '更新日志',
        url: `/changelog/${repo}`,
      },
      {
        title: '讨论',
        url: `https://github.com/eternallycyf/${repo}/issues`,
        openExternal: true,
      },
    ],
  },
  {
    title: '模板及配置',
    items: [
      {
        title: 'ims-monorepo-template',
        description: 'monorepo模板',
        url: 'https://github.com/eternallycyf/ims-monorepo-template',
        openExternal: true,
      },
      {
        title: 'ims-template',
        description: 'npm模板',
        url: 'https://github.com/eternallycyf/ims-template',
        openExternal: true,
      },
      {
        title: 'ims-template-config',
        description: '配置',
        url: 'https://github.com/eternallycyf/ims-template-config',
        openExternal: true,
      },
    ],
  },
  {
    title: '更多',
    items: [
      {
        title: 'lrxc-cli',
        url: 'https://github.com/eternallycyf/lrxc-cli',
        openExternal: true,
      },
    ],
  },
];
```
