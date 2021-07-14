<h2 data-id="webpack-5-title">Webpack 5</h2>
<ul>
<li>Webpack 5 вышел 10/10/2020</li>
<li class="fragment"><a href="https://webpack.js.org/blog/2020-10-10-webpack-5-release/">Release Notes</a></li>
</ul>
<p class="reveal fragment">🤓&nbsp;Подробнее о нововведениях</p>
-----
<!-- .slide: data-auto-animate data-menu-title="Важные нововведения 1/2" -->
<h2 data-id="webpack-5-title">Важные нововведения</h2>
<ul>
<li>Node.js Polyfills убраны (добавляйте самостоятельно)</li>
<li class="fragment">Нативная поддержка Worker'ов</li>
<li class="fragment">Async Modules</li>
<li class="fragment">Asset Modules</li>
<li class="fragment">Progress Plugin&nbsp;😃</li>
<li class="fragment">Module Federation&nbsp;🪄</li>
</ul>
-----
<!-- .slide: data-auto-animate data-menu-title="Важные нововведения 2/2" -->
<h2 data-id="webpack-5-title">Важные нововведения</h2>
<ul>
<li>Улучшена работа с target</li>
<li class="fragment">Улучшенный Tree-Shaking</li>
<li class="fragment">Изменилась работа с хуками (касается плагинов)</li>
<li class="fragment">Filesystem Cache</li>
</ul>
-----
<h2 data-id="webpack-5-title">Workers</h2>
<pre data-id="webpack-5-animation"><code class="javascript" data-trim>new Worker(new URL("./worker.js", import.meta.url))
</code></pre>
-----
<h2 data-id="webpack-5-title">Async Modules</h2>
<p data-id="webpack-5-filename" class="reveal r-hstack justify-start">webpack.config.js: </p>
<pre data-id="webpack-5-animation"><code class="javascript" data-trim data-line-numbers="|4">module.exports = {
    // ...
    experiments: {
        topLevelAwait: true,
    },
}
</code></pre>
<p class="reveal fragment r-hstack justify-start">🧐&nbsp;<a href="https://github.com/tc39/proposal-top-level-await">Proposal Top Level Await</a></p>
-----
<h2 data-id="webpack-5-title">Progress Plugin</h2>
<p data-id="webpack-5-filename" class="reveal r-hstack justify-start">webpack.config.js: </p>
<pre data-id="webpack-5-animation"><code class="javascript" data-trim data-line-numbers="|5">const webpack = require('webpack');
module.exports = {
    // ...
    plugins: [
        new webpack.ProgressPlugin() // you can specify percentBy option
    ],
}
</code></pre>
-----
<h2 data-id="webpack-5-title">Output.clean</h2>
<p data-id="webpack-5-filename" class="reveal r-hstack justify-start">webpack.config.js: </p>
<pre data-id="webpack-5-animation"><code class="javascript" data-trim data-line-numbers="|6">const webpack = require('webpack');
module.exports = {
    // ...
    output: {
        // ...
        clean: true,
    },
}
</code></pre>
<p class="reveal fragment r-hstack justify-start">🤓&nbsp;Появился с 5.20+</p>
<p class="reveal fragment r-hstack justify-start">🧐&nbsp;Заменяет&nbsp;<a href="https://github.com/johnagan/clean-webpack-plugin">сlean-webpack-plugin</a></p>
-----
<h2 data-id="webpack-5-title">Filesystem Cache</h2>
<p data-id="webpack-5-filename" class="reveal r-hstack justify-start">webpack.config.js: </p>
<pre data-id="webpack-5-animation"><code class="javascript" data-trim data-line-numbers="|7">const webpack = require('webpack');
module.exports = {
    // ...
    cache: {
        // compression: 'gzip',
        // maxAge: 5184000000,
        type: 'filesystem',
    },
}
</code></pre>
<p class="reveal fragment r-hstack justify-start">🧐&nbsp;<a href="https://webpack.js.org/configuration/cache/">Cache</a></p>
-----
<h2 data-id="webpack-5-title">Asset Modules</h2>
<p data-id="code-filename" class="reveal r-hstack justify-start">webpack.config.js: </p>
<pre data-id="code-animation"><code class="javascript" data-trim data-line-numbers="|5|11,13|18,20|25,27">module.exports = {
    // ...
    output: {
        // ...
        assetModuleFilename: 'assets/[hash][ext]',
    },
    module: {
        rules: [
            {
                test: /\.(png|svg|jpg|jpeg|gif)$/i,
                type: 'asset/resource',
                generator: {
                  filename: 'assets/images/[name][ext]',
                },
            },
            {
                test: /\.(woff|woff2|eot|ttf|otf)$/i,
                type: 'asset/resource',
                generator: {
                    filename: 'assets/fonts/[hash][ext]',
                },
            },
            {
                test: /\.(webm|mp4)$/i,
                type: 'asset/resource',
                generator: {
                     filename: 'assets/video/[name][ext]',
                },
            },
        ],
    },
}
</code></pre>
<p class="reveal fragment r-hstack justify-start">🧐&nbsp;<a href="https://webpack.js.org/guides/asset-modules/">Asset Modules</a></p>
-----
<h2 data-id="webpack-5-title">Plugin Hooks</h2>
<p data-id="webpack-5-filename" class="reveal r-hstack justify-start">plugin.js: </p>
<pre data-id="webpack-5-animation"><code class="javascript" data-trim data-line-numbers="|4-8|9-19">class CustomPlugin {
    //...
    apply(compiler) {
        // webpack v4
        // compiler.hooks.emit.tap('CustomPlugin', (compilation) => {
        //    // ...
        //    compilation.assets[filename] = assetToEmit;
        // });
        compiler.hooks.thisCompilation.tap('CustomPlugin', (compilation) => {
            compilation.hooks.processAssets.tap(
                {
                    name: 'CustomPlugin',
                    stage: Compilation.PROCESS_ASSETS_STAGE_ADDITIONS,
                },
                (assets) => {
                    compilation.assets[filename] = assetToEmit;
                }
            );
        });
    }
}
</code></pre>
