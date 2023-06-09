# Выявление токсичных комментариев

## Задача

Цель проекта состоит в построении модели, классифицирующей комментарии пользователей на позитивные и негативные (для отправки токсичных комментариев на модерацию). Обучение модели будет происходить на заранее размеченных данных. По требованию заказчика, качество модели будет определяться метрикой *F1*; показатель должен быть не менее 0.75. 

Для достижения поставленной цели необходимо:

1. Подготовить данные, переведя естественный текст в векторную форму;
2. Обучить несколько типов моделей, подобрать оптимальные гиперпараметры;
3. Сравнить качество моделей на кросс-валидации, выбрать модель с наивысшей метрикой;
4. Проверить выбранную модель на тестовой выборке.

Перевод естественного текста в векторный вид будет производиться методов *TF-IDF*. В качестве прогностических моделей будут исследоваться логистическая регрессия, градиентный бустинг и байесовский классификатор.

## Данные

Данные находятся в файле toxic_comments.csv. Столбец `text` в нём содержит текст комментария, а `toxic` — целевой признак.

## Основные выводы

Предоставленная выборка не сбалансирована по классам - на долю позитивного класса (т.е. токсичных комментариев) приходится ок. 10% объектов, что было учтено при разбиении выборкок. Перед векторизацией была проведена лемматизация текстов; для ускорения и устранения возможных "мусорных" признаков из выборки были удалены аномально длинные комментарии (примерная блина более 400 слов).

Были обучены три типа моделей: логистическая регрессия, градиентный бустинг и байесовский классификатор с подбором гиперпараметров. Наилучший результат (0.78 на тестовой выборке) показала модель градиентного бустинга, сбалансированная по классам, с максимальной глубиной 8, шагом обучения 0.444 и числом итераций 1000.

## Используемые библиотеки

*nltk*, *sklearn*,*lightgbm*, *optuna*, *pandas*, *seaborn*
