
# 改裝 docpress

## 擴充 markdown-it 的渲染外掛安裝方式

**/Users/chris/case/javascript-primer/node_modules/docpress-core/lib/helpers/markdown.js**

```javascript
function loadPlugins (md, plugins, cwd) {
  md = plugins.reduce((md, plug) => {
    if (plug instanceof Object && plug.name) {
      return md.use(require(plugPath(plug.name)), plug.options);
    }
    return md.use(require(plugPath(plug)));
  }, md);
}

function plugPath (plugName) {
  const pluginPath = tryRequire(`markdown-it-${plugName}`) ||
    (cwd && tryRequire(`${cwd}/node_modules/markdown-it-${plugName}`))
  if (!pluginPath) throw new Error(`Can't find module 'markdown-it-${plugName}'`)
  return pluginPath;
}
```
安心的安裝這些。

```shell
npm install -D markdown-it-abbr
npm install -D markdown-it-checkbox
npm install -D markdown-it-container
npm install -D markdown-it-deflist
npm install -D markdown-it-emoji
npm install -D markdown-it-footnote
npm install -D markdown-it-imsize
npm install -D markdown-it-ins
npm install -D markdown-it-mark
npm install -D markdown-it-regexp
npm install -D markdown-it-sub
npm install -D markdown-it-sup
```

並且在 docpress.json 檔案加上參數設定

```json
{
  // ...,
  "markdown": {
    "plugins": [
      "abbr",
      "deflist",
      "footnote",
      "imsize",
      "ins",
      "mark",
      "regexp",
      "sub",
      "sup",
      "checkbox",
      {
        "name": "container",
        "options": "success"
      },
      {
        "name": "container",
        "options": "info"
      },
      {
        "name": "container",
        "options": "warning"
      },
      {
        "name": "container",
        "options": "danger"
      },
      {
        "name": "emoji",
        "options": {
          "shortcuts": {}
        }
      }
    ]
  }
}
```