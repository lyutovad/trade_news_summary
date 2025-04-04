# Саммаризация новостей - портал "Торговые новости"

1. Выполнено исследование данных - были проанализированы тексты и саммари с целью определить влияние количества продуктов и стран на длину саммари, а также выяснить, сколько из саммари содержат все определенные продукты и локации.

**Вывод:** Локации оказывают более значительное влияние на текст саммари, чем количество продуктов. В случае, если в тексте упоминается множество стран, их список сокращается до союза, включающего все эти страны. Аналогично, большое количество продуктов может быть упрощено до общего кода МСТК (Международная стандартная торговая классификация).

Количество продуктов и стран не оказывает прямого влияния на длину саммари. Существуют случаи, когда длина саммари зависит не только от упоминания локаций или продуктов.

В английских статьях, если товар относится к коду 93 (специальные операции и товары, не классифицированные по типу), не всегда ясно, о каком товаре идет речь. Поэтому в саммари необходимо дать объяснение для читателей или описать данный товар, учитывая, что российский читатель может быть не знаком с ним.

Часто длина новостей увеличивается из-за необходимости предоставить контекст (например, в статье о снятии санкций следует напомнить, когда и какие санкции были введены). Эта информация может быть присутствовать в тексте, но не всегда является очевидной при построении саммари.

**Проблема:** Классификация продуктов по коду МСТК сталкивается с низким качеством классификатора (72 класса, метрика 0.71 / 0.69 - f1_macro_weighted / f1_macro), что делает невозможным полагаться на эти классы на этапе обработки текста.

**Гипотеза:** Следует также исследовать упоминания в саммари таких сущностей, как "Money", "currency", "price", "percentage", поскольку данные сущности также должны быть отражены в саммари в соответствии с техническим заданием.



2. Для всех размеченных саммари проверена метрика bertscore.

Метрика bertscore используется в задачах генерации текста благодаря ее лучшей корреляции с человеческими оценками по сравнению с традиционными методами, основанными на перекрытии.
Для модели саммаризации преимущества этой метрики:
- использование контекстных векторов (например, от BERT и подобных моделей) позволяет лучше понимать смысл текста, что особенно важно для выявления семантической близости между оригинальным текстом и его кратким содержанием. Это обеспечивает более точную оценку качества саммаризации.
- Косинусное сходство между контекстуальными вложениями позволяет оценить, насколько близко содержание саммари соответствует оригинальному тексту, что дает больше понимания, насколько тексты получились содержательно близкими. Такое понимание традиционные метрики, основанные на перекрытии слов, дать не могут.
- Линейное масштабирование значений метрики может облегчить интерпретацию результатов оценки. Это может способствовать более быстрой и точной корректировке моделей саммаризации.

Для нашей задачи также важным бонусом метрики может быть учет редких слов, которые встречаются в новостных текстах.

BertSCORE позволяет посмотреть 3 оценки: precision, recall, f1

<img src=./R_P_F_Bert.jpg>

Precision BERTScore показывает, насколько точно модель саммаризации передает информацию из исходного текста. Он измеряет, сколько токенов в предложении-кандидате соответствуют токенам в эталонном предложении. Чем выше значение precision BERTScore, тем более точно модель передает информацию.

Recall BERTScore показывает, насколько полно модель саммаризации передает информацию из исходного текста. Он измеряет, сколько токенов в эталонном предложении соответствуют токенам в предложении-кандидате. Чем выше значение recall BERTScore, тем более полно модель передает информацию.

F1 BERTScore является объединением precision и recall BERTScore и показывает общую производительность модели саммаризации. Он учитывает как точность, так и полноту передачи информации из исходного текста. Чем выше значение f1 BERTScore, тем более точно и полно модель передает информацию.


Нам важно больше внимания обратить на метрику recall или на F1. Можно подумать про Fβ-меру, где β будет приближаться к 2.

Определен порог метрики для случайных пар новость-саммари (самари перемешаны для всего датасета). Результат мерики для случайных предложений (0.628898632607875, 0.5693117015176956, 0.597188990363474):
- (0.6330698035954392, 0.5704953966405236, 0.5997249384421212) для русского языка
- (0.617849948057866, 0.5661763052334143, 0.5904717182977376) для английского языка.

Проверены статистики для метрики recall ниже случайной метрики (621 новость), выше 75 (6730 новостей) и выше 95 перцентилей (1347 новостей).

В саммари, получившими максимально высокий recall выжными оказываются все параметры - количество локаций, продуктов, длина саммари в разбивке по языкам (относительно полной выборки).

Во всей выборке видна заметная корреляция полноты и данных, связанных с длиной саммари. Т.е. с ростом длины саммари и полнота быдет увеличиваться.
При этом нет никаких линейных зависимостей с такими показателями как количество продуктов, локаций или их матчингом.


3. Исследованы саммари, содержащие количественные данные.
- QUANTITY – количества
- PERCENT – проценты
- MONEY – деньги
- PRICE – цена
- CURRENCY – валюта

Количество новостей с сущностями:
- money - 12753, 
- percent - 12072, 
- quantity - 13935,
- price - 1187,
- currency - 4369

Всего 254 новости содержать все эти сущности. 
currency не содержит важной информации, солбец уделен.

После объединения всех данных в один датасет, осталось 18907 строк (ru - 13531, en - 5376).

Линейная зависимость между длиной саммари и численными показателями не выявлена.

В датасете, содержащем все сущности, выявлена славая зависимость для quantity с длиной саммари.

Проверка на вхождение числовых показателей в саммари показала, что в саммари попадает бОльшая часть числовых данных. При этом точно выявить зависимость не удалось, насколько зависит количество матчей от длины текста, или насколько зависит длина саммари от матчей.


**Гипотеза:** если опираться на списки, полученные NER, то нужно ранжировать сущности по важности:
1. Локации + числовые
2. Продукты

Если выделяются числовые показатели, больше одной сущности, то порядок отбора:
1. quantity
2. percent
3. price
4. money