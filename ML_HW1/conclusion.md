# Резюме по проделанной работе
1. Был проведен базоый EDA и построены различные визуализации, которые помогли лучше понять данные и их взаимосвязь с целевой переменной.
2. Была проведена первичная обработка признаков и объектов, включающая в себя: удаление дубликатов, заполнение пропусков, извлечение новых признаков.
3. Далее стояла задача построить несколько моделей линейной регресси с разной конфигурацией, а именно:
* Мы строили модель линейной регресси на сырах признаках (lm) и на стандартизированных признаках (lm_std). Разница в метриках качества между этими двумя моделями была близка к нулю. Однако, благодаря стандартизации, у нас появилась возможность интерпретировать важность признаков в модели. Самым важным признаком оказалась переменная max_power.
* Далее мы попробовали улучшить модель с помощью LASSO-регрессии за счет применения регуляризации, а также попробовали воспользоваться свойством LASSO-регрессии, которое позволяет занулять незначимые признаки. Коэффициенты регуляризации в этом случае подбирались вручную. Улучшения метрик качества по сравнению с предыдущим пунктом получить не удалось.
* Затем мы реализовали подбор гиперпараметров с помощью GridSearchCV по 10-ти фолдам. На основании подбора был определен лучший набор коэффициентов в модели. Однако на рост метрик качества это по-прежнему не повлияло.
4. Следующей задачей было дообогатить наши выборки категориальными признаками. Для этого мы их дополнительно предобработали и закодировали через OneHotEncoding. После этого мы обучили на новом признаковом пространстве модель с Ridge-регрессией. Благодаря новому признаковому пространству метрика качества $R^2$ улучшилась с 0.54 до 0.78. Таким образом прирост качества благодаря добавлению новых прзинаков составил ~55%.
5. Далее мы сформулировали и реализовали бизнес метрику для данной задачи, которая показывает для данной модели МО долю прогнозов, отличающихся от реальных цен на эти авто не более чем на 10%.
6. Опираясь на данную бизнес-метрику мы определили, что лучше всего задачу бизнеса решает модель Ridge-регрессии с вещественными и категориальными признаками.
7. Заключительным этапом выполнения ДЗ стала реализация сервиса на FastApi, который выполнял две функции, а именно: 
* на вход подаются признаки одного объекта, а возвращается предсказанная стоимость автомобиля;
* на вход подается список признаков для нескольких объектов, а возвращается список предсказанных стоимостей для этих автомобилей. 

Сервис был успешно реализован (но это не точно).


P.S.: также мне кажется, что мне не нужно прикладывать скрины работы сервиса, поскольку я не пользовался интерфейсной частью через fastapi/docs, а отправлял post-запросы прям из ячейки ноутбука и там сразу видно все результаты. Результаты работы сервиса проверил. Они идентичны тому, что выдавала модель во 2 части.

# Что не удалось сделать
В целом все, что требовалось в ДЗ получилось сделать. Единственная сложность была с реализацией сервиса на FastApi, т.к. никогда ранее этим не занимался. Хотелось бы увидеть какое-нибудь эталонное решение этой задачи, потому что мое решение вряд ли SOTA. Очень интересно как это в идеале должно было бы выглядеть.