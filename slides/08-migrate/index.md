## Миграция с 4 на 5
[Webpack.js.org](https://webpack.js.org/migrate/5/) - официальный гайд
- Убрать node.js polyfills (или подключать самому) <!-- .element: class="fragment" -->
- Проверить нэйминг chunks и бандлов (для оптимизации кэширования) <!-- .element: class="fragment" -->
- Перейти на использование Assets Modules <!-- .element: class="fragment" -->
- Обновить плагины (пока могут работать как Deprecated) <!-- .element: class="fragment" -->
-----
<!-- .slide: data-menu-title="Node.js polyfills" -->
<h2 data-id="code-title">Node.js polyfills</h2>
<p data-id="code-description" class="reveal r-hstack justify-start">Проверить работу на 4 версии без nodejs polyfills</p>
<p data-id="code-filename" class="reveal r-hstack justify-start">webpack.config.js:</p>
<pre data-id="code-animation"><code class="javascript" data-trim>module.exports = {
  // ...
  node: {
    Buffer: false,
    process: false,
  },
};
</code></pre>
<p class="reveal fragment r-hstack justify-start">🧐&nbsp;Если нужны, то&nbsp;<a href="https://github.com/webpack/node-libs-browser">node-libs-browser</a></p>
-----
<!-- .slide: data-menu-title="Assets Modules" -->
<h2 data-id="code-title">Assets Modules</h2>
<p class="reveal r-hstack justify-start">Вместо raw-loader, url-loader, file-loader использовать Assets Modules</p>
<p data-id="code-filename" class="reveal r-hstack justify-start">webpack.config.js:</p>
<pre data-id="code-animation"><code class="javascript" data-trim data-line-numbers="|5-15|16-24">module.exports = {
   // ...
   module: {
        rules: [
            // {
            //    test: /\.(png|jpg|gif)$/i,
            //    use: [
            //      {
            //        loader: 'url-loader',
            //        options: {
            //          limit: 4 * 1024,
            //        },
            //      },
            //    ],
            // },
            {
                test: /\.(png|jpg|gif)$/i,
                type: 'asset',
                parser: {
                    dataUrlCondition: {
                        maxSize: 4 * 1024 // 4kb
                    },
                }.
            },
        ],
   },
};
</code></pre>
