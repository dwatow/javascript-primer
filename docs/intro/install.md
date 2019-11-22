
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