# Case-study оптимизации

### Актуальные проблемы
- Нужно оптимизировать механизм перезагрузки расписания из файла.
- Нужно найти и устранить проблемы, замедляющие формирование этих страниц.

#### Формирование метрики
Для того, чтобы понимать, дают ли мои изменения положительный эффект на быстродействие программы я использовал разницу между окончанием работы скрипта и началом работы на объемах small.json

#### Feedback-Loop
Для того, чтобы иметь возможность быстро проверять гипотезы я выстроил эффективный `feedback-loop`, который позволил мне получать обратную связь по эффективности сделанных изменений за 10 секунд

#### Находки
- `pghero` - вообще ничего не предлагал, возможно он не работал на dev окружении, но логами сыпал
- добавил индексы для `buses`, `services` и `trips` "по наитию" и это не дало никаких изменений
- для ускорения импорта данных использовал `activerecord-import`
- для профилирования отображения данных на странице использовал `rack-mini-profiler` и `bullet`

#### Результаты
В результате проделанной оптимизации удалось обработать файл `large.json` за ~30 секунд. `medium.json` ~10 секунд. `small.json` ~5 секунд.

Рендеринг страницы расписания удалось уменьшить до 400 мс для `medium.json` и до 8.5 секунд для `large.json`.
