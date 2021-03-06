
# Циклы

Благодаря предоставленным в Sass комплексным структурам данных, таких, как [списки](#section-24) и [карты](#section-25), не удивляет и возможность перебора по этим объектам.

Тем не менее, наличие циклов, как правило, подразумевает умеренно сложную логику, что, вероятно, не относится к Sass. Перед использованием цикла убедитесь, что он имеет смысл, и что он на самом деле решает задачу.

## Each

Цикл `@each`, безусловно, наиболее часто используемый из трёх циклов, предусмотренных Sass. Он предоставляет чистый API для перебора списка или карты.

{% include snippets/loops/01/index.html %}

При переборе карты всегда используйте имена переменных `$key` и `$value` ради последовательности.

{% include snippets/loops/02/index.html %}

Также соблюдайте следующие принципы, чтобы сохранить читаемость:

* Всегда пустая строка перед `@each`;
* Всегда пустая строка после закрывающей скобки (`}`), если на следующей строке нет закрывающей скобки (`}`).

## For

Цикл `@for` может быть полезным, когда скомбинирован с псевдоклассом CSS `:nth-*`. Исключая сценарии, когда предпочтительнее использовать цикл `@each`, если вам надо пройтись по какому-нибудь объекту.

{% include snippets/loops/03/index.html %}

Всегда используйте `$i` как переменную для соблюдения соглашения, пока у вас нет веских причин изменить её, никогда не используйте ключевое слово `to`, используйте `through`. Многие разработчики даже и не знают, что Sass предоставляет такие варианты; использование разных может привести к путанице.

Также следуйте следующим принципам, чтобы сохранить читаемость:

* Всегда пустая строка перед `@each`;
* Всегда пустая строка после закрывающей скобки (`}`), если на следующей строке не закрывающая скобка (`}`).

## While

Цикл `@while` не имеет абсолютно никакого применения в реальном проекте Sass, особенно из-за того, что нет способа остановить цикл изнутри. **Не используйте его**.
