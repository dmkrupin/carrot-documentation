﻿# Примеры ({{versionLabel}})

## Работа с Carrot Keyer

> Carrot Keyer - программный модуль позволяющий размещать нужный объект с зелёного фона на виртуальный (или любой другой) фон при помощи технологии рир-проекции.

> Для наилучшего результата рекомендуется использовать \***\* , при работе в режиме Interlace могут возникнуть проблемы при работе с **DeNoise\*\*.

_Входной сигнал_:
![](images\example_keyer\original.png)
_Изначальный вид_
![](images\example_keyer\default.png)
_Итоговый вид_
![](images\example_keyer\stage_11.png)

1. Откройте Carrot Engine.
2. Выберите **Tools > Contents Settings > Keyer Settings** или нажмите клавишу **F7**, чтобы открыть все доступные окна настроек.
   <br>![](images\example_keyer\screen_01.png)

> Для удобства настройки рекомендуется перейти в режим отображения **Mode > MultiView**, чтобы наблюдать за изменениями на всех этапах кеинга.

![](images\example_keyer\stage_01.png)

- Foreground - отображение переднего плана.
- DeNoise - отображение Foreground с шумоподавлением.
- DeSpill - отображение Foreground с избавлением от цветовых рефлексов.
- Screen Restoration - отображение Foreground с восстановлением зеленого цвета.
- Alpha Mask - отображение маски объекта, который нужно прокеить.
- Screen Mask -
- Shadows -
- Highlights -
- Background -
- Environment Overlay -
- Environment Light -

В правом нижнем углу для удобства расположены вектороскоп и гистограмма.
![](images\example_keyer\stage_02.png)

> Для наилучшего результата значения вектороскопа должны доходить до середины линии **_G_** или **_B_** в зависимости от цвета хромакея.<br> > <br>Для наилучшего качества гистограмма должна быть максимально ровной, растянутой по всей границе и без пиков по краям.<br> > <br>Нажатием **ЛКМ** или **ПКМ** по гистограмме можно посмотреть отдельно информацию по каждому цветовому каналу.

В начале нужно задать цвет хромакея, для этого:

1. Во вкладке **Alpha Mask** нажмите на кнопку `Pick` и с помощью **ЛКМ** щёлкните по любому участку хромакея на экране.
2. Оцените результат в окне режима _Alpha Mask._

### **DeNoise**

Наблюдаем, что изображение в _Alpha Mask_ имеет много шума, избавиться от него можно при помощи инструмента **DeNoise**:<br>
Во вкладке **DeNoise** имеются два параметра:

1. `Threshold` - порог срабатывания, позволяющий сохранить четкие границы на объектах;
2. `Radius` - радиус размытия в пикселях (в обычных случаях хватает значений до `50`).

Выставите значение `Threshold` в `0` и понемногу увеличивайте до требуемого результата. По необходимости скорректируйте параметр `Radius`.

Результат:
![](images\example_keyer\stage_03.png)

> Чтобы вернуть настройки по умолчанию, нажмите **ПКМ** по области стрелок нужного счетчика.

Режим _Final Result_:
![](images\example_keyer\stage_04.png)

### **DeSpill**

Картинка избавилась от лишнего шума, теперь необходимо убрать голубые границы с человека. Они возникли в результате того, что _DeSpill_ не соответствует заднему фону по тону и яркости.

> Если задний фон тёмный, а _DeSpill_ светлый, то на объекте будут видны белые границы и наоборот.

Чтобы исправить границы на объекте:

1. Переключите окно в режим отображения _DeSpill_.
   <br>Параметры вкладки **DeSpill**:
   - `Preset` - настройка соотношения красного и синего. В нашем случае лучше всего подошёл пресет **Average**.
     <br>Лучше всего добиться максимально серого цвета у **DeSpill** до наложения параметра `Saturation`.

- `Saturation` - смешивание с задним фоном по цвету.
- `Darken` и `Brighten` - изменение яркости тёмных и светлых областей.
  > Для наилучшего результата _DeSpill_ должен соответствовать по оттенкам и яркости изображению на _Background_.

Результат:
![](images\example_keyer\stage_05.png)

### **Screen Restoration**

Сравните окно _Screen Restoration_ с _Foreground_, в итоге должен получиться зеленый цвет без лишних объектов. Для настройки этого окна используется вкладка **Inner Mask**:

> **Inner Mask** помогает справиться с проблемными и дефектными элементами на объекте (например, зелеными пуговицами на человеке и т.п.)

1. С помощью инструментов `Red Weight`, `Blue Weight` и `Mask Levels` сделайте максимально возможную непрозрачную маску для необходимых объектов.
2. Наблюдайте за результатом в окнах _Inner Mask_, _Alpha Mask_ и _Screen Restoration_.

Результат:<br>
_Inner Mask_
![](images\example_keyer\stage_06.png)
_Alpha Mask_
![](images\example_keyer\stage_07.png)
_Screen Restoration_
![](images\example_keyer\stage_08.png)

### **Alpha Mask**

Теперь необходимо скорректировать саму маску. Для этого:

1. Во вкладке **Alpha Mask** выставите значение параметров `J Weight`, `Red Weight`, `Blue Weight`, `Inner Mask` на `0`.
2. Во вкладке **Alpha Mask (Advanced)** выберите `Key Type` - `UCS`.
   > У `RGB` параметры `Red Weight` и `Blue Weight` работают как процент вытеснения зелёного, т.е. в сумме эти два параметры должны, в идеале, составлять **единицу**.
3. За счёт параметров `Border Light` и `Border Dark` максимально проявите объект.

> `B. Feather` отвечает за смещение маски от границы **Inner Mask** до такого же расстояния снаружи объекта.

> `Floor Levels` отвечает за улучшения маски у объектов, помеченных как `Chromakey Floor` во вкладке **Mask.** 4. Во вкладке **`Alpha Mask`** начинаем подбирать параметр **`Inner Mask`** в районе значения `0,5`. 5. Далее мы изменяем значение параметров `Red Weight` и `Blue Weight` до `1`. Если маски не хватает, то мы начинаем добавлять значение `J Weight` (разность яркости с _Screen Restoration_ и _Foreground,_ работает только с `Key Type` _-_ `UCS`). Если визуально этот параметр не оказывает заметного эффекта на _Alpha Mask_, то лучше его отключить. С помощью `Mask Levels` можно “подчистить” маску, чтобы остались только необходимые объекты.

> Если видно мерцание кея, то его можно уменьшить через правки `Threshold` и `Radius` вкладки **Denoise.**

_Final Result_
![](images\example_keyer\stage_09.png)

### **Shadows** & **Highlights**

Для усиления отображения теней и отражений можно использовать вкладки **Shadows** и **Highlights**, однако в данном примере эти настройки не требуются и остаются выключенными.

### **Environment**

Для улучшения эффекта "вживления" объекта с окружением можно воспользоваться вкладкой **Environment** и режимами отображения _Environment Overlay_ и _Environment Light_:

1. `Overlay` - уровень наложения фона на объекты.
2. `Overlay Blur` - размытие фона, лучше оставлять детали до тех пор, пока это не будет заметно на объектах первого плана.
3. `Light Strength` - степень засветки по краям объектов.
4. `Light Blur` - размытие фона для засветки
5. `Light Levels` - корректировка уровней яркости фона для засветки

> Для наилучшего результатас помощью Light Levels нужно оставлять только те элементы, которые действительно в реальности могут давать засвет на края объекта.

_Environment Light_
![](images\example_keyer\stage_10.png)

_Environment Overlay_
![](images\example_keyer\stage_12.png)

Итоговый результат:
![](images\example_keyer\stage_11.png)