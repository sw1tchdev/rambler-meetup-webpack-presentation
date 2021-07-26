<!-- .slide: data-auto-animate -->
<h2 data-id="webpack-mf-title">Module Federation</h2>
<ul>
<li>Нововведение в Webpack 5</li>
<li class="fragment">Придумал <a href="https://twitter.com/ScriptedAlchemy">Zack Jackson</a></li>
<li class="fragment">Дает возможность подключать динамически модули из другой webpack-сборки, которые могут быть на другом хосте</li>
<li class="fragment">Иными словами MF позволяет использовать микрофронтенды прямо в браузере 🎉</li>
</ul>
-----
<!-- .slide: data-auto-animate -->
<h2 data-id="webpack-mf-title">Для чего был придуман</h2>
<ul>
    <li>Безболезненно разрабатывать большое приложение несколькими командами</li>
    <li class="fragment">Убрать перезагрузку страниц при переходе между Microfrontend'ами</li>
    <li class="fragment">Не грузить лишний раз vendor code, который уже был загружен ранее</li>
    <li class="fragment">Не надо пересобирать приложение, если поменялся один из Microfrontend</li>
    <li class="fragment">Приложение собирается налету в браузере, а удаленные модули можно просто разместить на CDN</li>
</ul>
-----
<h2 data-id="webpack-mf-title">Демо</h2>

[sw1tchdev/meetup-webpack-mf](https://github.com/sw1tchdev/meetup-webpack-mf)

-----
<h2 data-id="webpack-mf-title">Недостатки</h2>
<ul>
    <li>Документация MF на <a href="https://webpack.js.org/concepts/module-federation/">webpack.js.org</a></li>
    <li class="fragment">Возможные проблемы с сетью во время загрузки модулей</li>
    <li class="fragment">Сложности с тестированием</li>
    <li class="fragment">SSR можно, но пока это больно</li>
    <li class="fragment">Технология еще не отработана</li>
    <li class="fragment">HMR</li>
</ul>
-----
<h2 data-id="webpack-mf-title">Примеры Module Federation</h2>

[module-federation/module-federation-examples](https://github.com/module-federation/module-federation-examples)

