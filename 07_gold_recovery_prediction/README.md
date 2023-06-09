# Прогноз коэффициента восстановления золота из руды

## Задача

Задача состоит в создании прототипа модели машинного обучения для прогноза коэффициента восстановления золота из руды в зависимости от качества сырья и технических характеристик процесса. Модель позволить оптимизировать производственный процесс за счет уменьшения рисков убыточности. Качество модели оценивается исходя из показателя **sMAPE**. 

$$ sMAPE = \frac{1}{N}\sum_{i=1}^{N} \frac{|y_i - \hat{y}_i|}{(|y_i| + \hat{y}_i) / 2} \times 100 \% $$

$$ Итоговое\ sMAPE = 25\%\times sMAPE(rougher) + 75\%\times sMAPE(recovery),\ где $$

$y_i$ - фактическое значение коэфффициента восстановления,

$\hat{y}_i$ - прогнозное значение коэффициента восстановления,

$N$ - число объектов в выборке, по которой ведется расчет,

$rougher$ - стадия флотации,

$recovery$ - финальная стадия технологического процесса.

Данные для обучения и валидации результатов также приложены к техническому заданию. 

Для выполнения поставленной задачи необходимо:

1. Проанализировать состав и структуру имеющихся данных;
2. При необходимости доработать данные для дальнейшего использовапния;
2. Обучить и провалидировать результаты нескольких типов моделей, выбрать оптимальную;
3. Проверить результаты выбранной модели на тестовых данных.

## Данные

Данные находятся в трёх файлах:
- gold_recovery_train_new.csv — обучающая выборка;
- gold_recovery_test_new.csv — тестовая выборка;
- gold_recovery_full_new.csv — исходные данные.

Данные индексируются датой и временем получения информации (признак date). Соседние по времени параметры часто похожи. Некоторые параметры недоступны, потому что замеряются и/или рассчитываются значительно позже. Из-за этого в тестовой выборке отсутствуют некоторые признаки, которые могут быть в обучающей. Также в тестовом наборе нет целевых признаков.
Исходный датасет содержит обучающую и тестовую выборки со всеми признаками.

Признаки названы с указанием этапов технологического процесса.

## Основные выводы

Была проведена реконсилиация предоставленных данных, как на предмет соответствия значений и полноты, так и на различия в распределениях параметров на обучающей и тестовой выборках. Несоответствия не обнаружены.

После проведения предобработки (главным образом удаление аномалий) были исследованы три типа моделей регрессии: дерево решений, случайный лес и линейная регрессия. Для первых двух типов проводился подбор гиперпараметров. В результате кросс-валидации наилучший результат показала модель дерева решений с глубиной 4 и минимальным числом объектов в листе 30 (значение sMAPEна тестовой выборке 8,2%).

## Используемые библиотеки
*sklearn*, *pandas*, *matplotlib.pyplot*
