
# Адаптивный веб-дизайн и точки останова

Я не думаю, что надо рассказывать, что такое адаптивный веб-дизайн, так как он сейчас везде. Тем не менее, вы можете задаться вопросом: *почему раздел об адаптивном веб-дизайне находится в руководсте по Sass?* Просто есть кое-какие приёмы для облегчения работы с точками останова, так что я подумал, что будет неплохо перечислить их здесь.

## Именование точек останова

Я думаю, что медиа-запросы не должны быть привязаны к специальным устройствам. Например, определённо плохая идея – специально нацеливаться на iPad или устройства на Blackberry. Медиа-запросы должны обслуживать диапазон размеров экрана, пока нет перехода к следующему медиа-запросу.

По этим же причинам наименование точек останова не должно соотвествовать устройствам, а иметь более общие названия. Тем более, что некоторые телефоны теперь больше, чем планшеты, а некоторые планшеты больше экранов маленьких компьютеров, и тому подобное…

{% include snippets/rwd/01/index.html %}

Таким образом, [любое соглашение по именованию](https://css-tricks.com/naming-media-queries/), которое даёт кристально чистое понимание, что дизайн не привязан к конкретным устройствам, будет работать до тех пор, пока даёт ощущение масштаба.

{% include snippets/rwd/02/index.html %}

<div class="note">
  <p>В предыдущем примере используются вложенные карты для определения точек останова, но по большому счёту, всё зависит от способа управления точками останова, на который вы опираетесь. Вы можете выбрать строки, а не внутренние карты для большей гибкости (например <code>'(min-width: 800px)'</code>).</p>
</div>

## Управление точками останова

После того, как вы объявили ваши точки останова, вам нужен способ, чтобы использовать их в медиа-запросах. Есть много способов сделать это, но, должен сказать, я большой поклонник получения точек останова из карт через функцию геттер. Эта система является одновременно простой и эффективной.

{% include snippets/rwd/03/index.html %}

<div class="note">
  <p>Очевидно, что это довольно упрощенный менеджер точек останова, который не будет работать, когда надо обрабатывать произвольные или множественные точки остановки. Если вам нужно управление отзывчивостью с расширенными настройками, могу порекоммендовать вам не изобретать колесо, а воспользоваться отличными решениями: <a href="https://github.com/sass-mq/sass-mq">Sass-MQ</a>, <a href="http://breakpoint-sass.com/">Breakpoint</a> или <a href="https://github.com/eduardoboucas/include-media">include-media</a>.</p>
  <p>Если вы хотите больше узнать о том, как разобраться с медиа-запросами в Sass, то и <a href="https://www.sitepoint.com/managing-responsive-breakpoints-sass/">SitePoint</a>, и <a href="https://css-tricks.com/approaches-media-queries-sass/">CSS-Tricks</a> имеют отличные статьи на эту тему.</p>
</div>

## Использование медиа-запросов

Не так давно ещё были довольно жаркие дебаты о том, где именно должны быть описаны медиа-запросы: должны ли они быть в селекторах (как это позволяет Sass) или строго отделены от них? Я должен сказать, что я искренний защитник системы *медиа-запросов-внутри-системы*, я думаю, что это хорошо сочетается с идеей *компонентов*.

{% include snippets/rwd/04/index.html %}

Это создаст следующий CSS:

{% include snippets/rwd/05/index.html %}

Вы могли слышать, что это правило приводит к дублированию медиа-запросов в получаемом CSS. Это, безусловно, верно. Хотя, были сделаны тесты, которые говорят о том, что это не имеет особого значения, если за дело берётся Gzip (или аналог):

> … мы выяснили, были ли влияния на производительность комбинированных и рассеяных медиа-запросов, и пришли к выводу, что различие является минимальным в худшем случае, а по существу и не существует.<br>
> &mdash; Сэм Ричардс относительно Breakpoint

Теперь, если вы действительно обеспокоены дублированием медиа-запросов, вы всё ещё можете использовать инструмент, чтобы объединить их, например, [этот gem](https://github.com/aaronjensen/sass-media_query_combiner), однако я должен вас предупредить о возможных побочных эффектах перемещения CSS-кода. Вы остаетёсь без представления о порядке кода, что является важным.
