# Саммаризация новостей - портал "Торговые новости"

1. Выполнено исследование данных - были проанализированы тексты и саммари с целью определить влияние количества продуктов и стран на длину саммари, а также выяснить, сколько из саммари содержат все определенные продукты и локации.

**Вывод:** Локации оказывают более значительное влияние на текст саммари, чем количество продуктов. В случае, если в тексте упоминается множество стран, их список сокращается до союза, включающего все эти страны. Аналогично, большое количество продуктов может быть упрощено до общего кода МСТК (Международная стандартная торговая классификация).

Количество продуктов и стран не оказывает прямого влияния на длину саммари. Существуют случаи, когда длина саммари зависит не только от упоминания локаций или продуктов.

В английских статьях, если товар относится к коду 93 (специальные операции и товары, не классифицированные по типу), не всегда ясно, о каком товаре идет речь. Поэтому в саммари необходимо дать объяснение для читателей или описать данный товар, учитывая, что российский читатель может быть не знаком с ним.

Часто длина новостей увеличивается из-за необходимости предоставить контекст (например, в статье о снятии санкций следует напомнить, когда и какие санкции были введены). Эта информация может быть присутствовать в тексте, но не всегда является очевидной при построении саммари.

**Проблема:** Классификация продуктов по коду МСТК сталкивается с низким качеством классификатора (72 класса, метрика 0.71 / 0.69 - f1_macro_weighted / f1_macro), что делает невозможным полагаться на эти классы на этапе обработки текста.

**Гипотеза:** Следует также исследовать упоминания в саммари таких сущностей, как "Money", "currency", "price", "percentage", поскольку данные сущности также должны быть отражены в саммари в соответствии с техническим заданием.



2. Для всех размеченных саммари проверена метрика bertscore.

Определен порог метрики для случайных пар новость-саммари. Результат мерики для случайных предложений около 0,63, 0.57, 0.6 и 0.67, 0.6, 0.63 для русского и английского языков соответственно.

Проверены статистики для метрики recall ниже случайной метрики, выше 75 и выще 95 перцентилей.

Для данных выше с полнотой выше 95 перцентиля (

В саммари, получившими максимально высокий recall выжными оказываются все параметры - количество локаций, продуктов, длина саммари в разбивке по языкам (относительно полной выборки).

Во всей выборке видна заметная корреляция полноты и данных, связанных с длиной саммари. Т.е. с ростом длины саммари и полнота быдет увеличиваться.
При этом нет никаких линейных зависимостей с такими показателями как количество продуктов, локаций или их матчингом.
