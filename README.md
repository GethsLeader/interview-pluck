# Pluck


Реализация простого "интернет магазина". Без `backend` части.


## Требования


### 1. Runtime configuration


Заменить "стандартное" вбилживаемое в приложение окружение с конфигурацией на динамически подгружаемую при инициализации
приложения конфигурацию, которая должна быть доступна в любой части приложения. Эта конфигурация содержит флаг для
индикации включен ли production режим или нет (свойство `production`, если оно `true`, то вызвать `enableProdMode`) и
настройки для банеров (массив `banners`), которые нужно отобразить в приложении.


### 2. Routes, lazy modules


В приложении должно быть 3 "lazy" модуля подгружаемых через routing:


#### Витрина


Подгружает и отображает список товаров. Товары должны подгружаться динамически из `mock` конфига
[/assets/configs/goods-mock/index.json](assets/configs/goods-mock/index.json). При отображении карточки товара следует
отобразить его изображение, название, цену (оригинальную и после скидки) и кнопку добавления в корзину (если товар еще
не был добавлен). При нажатии на карточку товара должен происходить переход в модуль "Детали товара".


#### Детали о товаре


Подгружает и отображает полную информацию о товаре и кнопку добавления в корзину. Если товар уже был добавлен в корзину,
то отобразить количество товара в корзине с кнопками "+" и "-" для добавления или удаления единиц товара из корзины.
Информация о товаре должна подгружаться динамически из [/assets/configs/goods-mock](assets/configs/goods-mock) по id.


#### Корзина


Отображает список добавленных в корзину товаров с их изображениями, названием, ценой и позволяет менять их добавленное
количество кнопками "+" и "-". В нижней части отображаются общая сумма и кнопка "Process to checkout" (которая при
нажатии просто выводит логотип ([/assets/images/logos/logo-1.png](assets/images/logos/logo-1.png)) и текст "WIP" в
диалоговом окне).


### 3. Main component


Основной компонент должен содержать:
* Заголовок с логотипом ([/assets/images/logos/logo-1.png](assets/images/logos/logo-1.png)) и кнопкой корзины
(если в корзине есть добавленные товары, то отобразить количество позиций на кнопке в badge);
* Компонент отображающий банера. Банера не должны подгружаться и отображаться до тех пор, пока не инициализируется 
основной контент на странице (это может быть либо витрина, или детали о товаре, или корзина). После инициализации
основного контента - подгрузить изображения банеров (свойство `path`) и отобразить их компонент с какой-либо подходящей
быстрой анимацией. Кроме изображения каждый баннер содержит текст (свойство `text`), который выводится в определенной
зоне баннера (свойство `zone`). По факту получается так, что компонент банеров является простой каруселью со слайдами.
Карусель переключает слайды каждые 10 секунд или при нажатии на какие-либо элементы навигации (на усмотрение 
разработчика);
* Компонент router-outlet.


### 4. Реализация

* Для реализации нужно использовать версию Angular 10+;
* Верстка и основные модули приложения должны быть реализованы разработчиком (желательно использовать минималистичный
дизайн);
* Компонент карусели банеров должен быть реализован разработчиком и не может быть из сторонней библиотеки;
* Товар добавленный в корзину должен сохранятся в `localStorage`;
* Использование `NgRx` приветствуется;
* Наличие `e2e` тестов необязательно, работающие `unit` тесты приветствуются;
* Дополнительно можно добавить систему отзывов к товарам (сами отзывы и рейтинг сохранять в `localStorage`/`IndexedDB`);
* Код выполненного тестового задания должен размещаться в открытом репозитории на github/gitlab/bitbucket.
