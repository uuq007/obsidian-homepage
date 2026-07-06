# 个人主页 v13.7 - 查看器入口

```datacorejsx
const { useState, useEffect, useRef } = dc;

function HomepageLoader() {
  const [Component, setComponent] = useState(null);
  const [status, setStatus] = useState('waiting');
  const loadedRef = useRef(false);
  const retriedRef = useRef(false);

  useEffect(() => {
    if (loadedRef.current) return;
    const dcGlobal = window.datacore;

    const tryLoad = async () => {
      if (loadedRef.current) return;
      loadedRef.current = true;
      setStatus('loading');

      try {
        const mod = await dc.require(dc.headerLink(dc.resolvePath("PersonalHomepageCode.md"), "ViewComponent"));
        setComponent(function() { return mod.EditableHomepage; });
      } catch (e) {
        loadedRef.current = false;
        if (!retriedRef.current) {
          retriedRef.current = true;
          setStatus('reindexing');
          // 查找并执行 DataCore 重建索引命令
          try {
            var cmds = app.commands.commands;
            for (var id in cmds) {
              if (id.indexOf('datacore') !== -1 && cmds[id].name.toLowerCase().indexOf('reindex') !== -1) {
                app.commands.executeCommandById(id);
                break;
              }
            }
          } catch(cmdErr) {}
          // 等待索引完成后重试
          setTimeout(function() { tryLoad(); }, 5000);
        } else {
          setStatus('error');
        }
      }
    };

    if (dcGlobal && dcGlobal.core && dcGlobal.core.initialized) {
      tryLoad();
    } else {
      setStatus('waiting');
      var ref = dcGlobal ? dcGlobal.on("initialized", function() { tryLoad(); }) : null;
      return function() { if (ref && dcGlobal) dcGlobal.offref(ref); };
    }
  }, []);

  if (Component) return <Component />;

  var statusText = status === 'waiting' ? '主页等待索引完成...' :
                   status === 'loading' ? '主页加载中...' :
                   status === 'reindexing' ? '主页加载失败，正在自动重建索引...' :
                   '主页加载失败，请手动执行 DataCore: Reindex entire vault 命令后刷新';

  return <div style={{ padding: 16, color: '#999', fontSize: 13 }}>{statusText}</div>;
}

return <HomepageLoader />;
```
