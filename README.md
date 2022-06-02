# Кастомный компонент для ESPHome для управления кондиционером по wifi <!--[![GitHub release](https://img.shields.io/github/v/release/GrKoR/esphome_aux_ac_component)](https://github.com/GrKoR/esphome_aux_ac_component/releases/) [![Телеграм](https://img.shields.io/badge/Telegram-2CA5E0?style=flat&logo=telegram&logoColor=white)](https://t.me/aux_ac) -->

English readme [is here](README-EN.md#esphome-aux-air-conditioner-custom-component-aux_ac). 

Управляет кондиционерами на базе AUX по wifi.<br />
По тексту ниже для компонента используется сокращение `aux_ac`.

Обсудить проект можно [в чате Телеграм](https://t.me/aux_ac).<br /> 
Отзывы о багах и ошибках, а так же запросы на дополнительный функционал оставляйте [в соответствующем разделе](https://github.com/GrKoR/esphome_aux_ac_component/issues).
Будет просто отлично, если к своему сообщению вы добавите лог и подробное описание. Для сбора логов есть [специальный скрипт на Python](https://github.com/GrKoR/ac_python_logger). С его помощью вы сможете сохранить в csv-файл все пакеты, которыми обменивается wifi-модуль и сплит-система. Если такой лог дополнить описанием, в какое время и что именно вы пытались включить, то это сильно ускорит исправление багов.


## ДИСКЛЭЙМЕР (ОТМАЗКИ) ##
1. Все материалы этого проекта (программы, прошивки, схемы, 3D модели и т.п.) предоставляются "КАК ЕСТЬ". Всё, что вы делаете с вашим оборудованием, вы делаете на свой страх и риск. Автор не несет ответственности за результат и ничего не гарантирует. Если вы с абсолютной четкостью не понимаете, что именно вы делаете и для чего, лучше просто купите wifi-модуль у производителя вашего кондиционера. 
2. Я ~~не настоящий сварщик~~ не программер. Поэтому код наверняка не оптимален и плохо оформлен (зато комментариев по коду я разместил от души), местами может быть написан небезопасно. И хоть я и старался протестировать всё, но уверен, что какие-то моменты упустил. Так что отнеситесь к коду с подозрением, ожидайте от него подвоха и если что-то увидели - [пишите в багрепорт](https://github.com/GrKoR/esphome_aux_ac_component/issues).


## Поддерживаемые кондиционеры ## 
AUX - это один из нескольких OEM-производителей кондиционеров. AUX производят кондиционеры как под собственным брендом, так и для внешних заказчиков. Поэтому есть шанс, что произведенный на их фабрике кондиционер неизвестного бренда с `aux_ac` так же заработает.
В интернете есть такой перечень производившихся на фабриках AUX брендов: AUX, Abion, AC ELECTRIC, Almacom, Ballu , Centek, Climer, DAX, Energolux, ERISSON, Green Energy, Hyundai, IGC, Kentatsu (некоторые серии), Klimaire, KOMANCHI, LANZKRAFT, LEBERG, LGen, Monroe, Neoclima, NEOLINE, One Air, Pioneer (до 2016 года), Roda, Rovex, Royal Clima, SAKATA, Samurai, SATURN, Scarlett, SmartWay, Soling, Subtropic, SUBTROPIC, Supra, Timberk, Vertex, Zanussi. В его полноте и достоверности есть сомнения, но ничего лучше найти не удалось.


### Список совместимых (протестированных) кондиционеров ###
[Список протестированных кондиционеров](docs/AC_TESTED.md) размещен в отдельном файле и включает те модели, на которых `aux_ac` был запущен автором компонента или пользователями. Этот список постоянно пополняется, преимущественно по обратной связи от пользователей [в чате Телеграм](https://t.me/aux_ac).<br />
 
### Если кондиционер в списке отсутствует ###
Если производитель вашего кондиционера есть в списке выше, то стоит изучить вопрос. Возможно, вам тоже подойдет `aux_ac` для управления по wifi.<br />
Если в инструкции пользователя вашего кондиционера что-то написано про возможность управления по wifi (особенно с помощью мобильного приложения ACFreedom), то есть весьма существенные шансы, что `aux_ac` сможет управлять и вашим кондиционером. Но будьте осмотрительны: ваш кондиционер никем не тестировался и важно четко понимать, что вы делаете. Иначе можете наломать дров.<br />
Если вы не уверены в своих силах, лучше дождитесь, пока другие более опытные пользователи протестируют вашу модель кондиционера (правда, это может не случиться никогда). Или приходите с вопросами [в телеграм-чат](https://t.me/aux_ac). Возможно, там вам помогут.

Если вы протестировали ваш кондиционер и он работает, напишите мне, пожалуйста. Я внесу вашу модель в список протестированных. Возможно, это упростит кому-то жизнь =)<br />
Лучший способ сообщить о протестированном кондиционере - написать [в телеграм](https://t.me/aux_ac) или [в разделе багрепортов и заказа фич](https://github.com/GrKoR/esphome_aux_ac_component/issues).

## Как использовать компонент ##
Для работы с кондиционером понадобится "железо" и прошивка. Описание электроники вынесено [в отдельный файл](docs/HARDWARE.md).

### Прошивка: интеграция aux_ac в вашу конфигурацию ESPHome ###
Для использования требуется [ESPHome](https://esphome.io) версией не ниже 1.18.0. Именно в этой версии появились `external_components`. Но лучше использовать версию 1.20.4 или старше, так как до этой версии массированно исправлялись ошибки в механизме подключения внешних компонентов.<br />

## Установка ##
1. Подключите компонент.
За подробностями можно заглянуть в [официальную документацию ESPHome](https://esphome.io/components/external_components.html?highlight=external).
```yaml
external_components:
  - source:
      type: git
      url: https://github.com/GrKoR/esphome_aux_ac_component
```
2. Настройте UART для коммуникации с вашим кондиционером:
```yaml
uart:
  id: ac_uart_bus
  tx_pin: GPIO1
  rx_pin: GPIO3
  baud_rate: 4800
  data_bits: 8
  parity: EVEN
  stop_bits: 1
```
3. **ВАЖНО!** Нужно отключить логгер ESPHome, чтобы он не отправлял в кондиционер свои данные.
Отключение логгера от UART никак не затронет вывод в лог консоли или web-сервера.
```yaml
logger:
    baud_rate: 0
```
Если по каким-то причинам вам нужен вывод логгера в UART, можно переключить его на другой UART чипа. Например, у ESP8266 два аппаратных UART: UART0 и UART1. `Aux_ac` подходит только UART0, поскольку только он у esp8266 имеет и TX и RX. Логгеру достаточно только TX. Такой функционал в чипе esp8266 у UART1:
```yaml
logger:
    level: DEBUG
    hardware_uart: UART1
```

## Настройка компонента ##
Минимальная конфигурация:
```yaml
climate:
  - platform: aux_ac
    name: "AC Name"
```

Полная конфигурация:
```yaml
climate:
  - platform: aux_ac
    name: "AC Name"
    id: aux_id
    uart_id: ac_uart_bus
    period: 7s
    show_action: true
    display_inverted: true
    indoor_temperature:
      name: AC Indoor Temperature
      id: ac_indoor_temp
      accuracy_decimals: 1
      internal: false
    outdoor_temperature:
      name: AC Outdoor Temperature
      id: ac_outdoor_temp
      internal: false
    outbound_temperature:
      name: AC Colant Outbound Temperature
      id: ac_outbound_temp
      internal: false
    inbound_temperature:
      name: AC Colant Inbound Temperature
      id: ac_inbound_temp
      internal: false
    compressor_temperature:
      name: AC Compressor Temperature
      id: ac_strange_temp
      internal: false
    display_state:
      name: AC Display State
      id: ac_display_state
      internal: false
    defrost_state:
      name: AC Defrost State
      id: ac_defrost_state
      internal: false
    invertor_power:
      name: AC Invertor Power
      id: ac_invertor_power
      internal: false
    preset_reporter:
      name: AC Preset Reporter
      id: ac_preset_reporter
      internal: false
    visual:
      min_temperature: 16
      max_temperature: 32
      temperature_step: 1
    supported_modes:
      - HEAT_COOL
      - COOL
      - HEAT
      - DRY
      - FAN_ONLY
    custom_fan_modes:
      - MUTE
      - TURBO
    supported_presets:
      - SLEEP
    custom_presets:
      - CLEAN
      - HEALTH
      - ANTIFUNGUS
    supported_swing_modes:
      - VERTICAL
      - HORIZONTAL
      - BOTH
```

## Параметры компонента: ##
- **name** (**Обязательный**, строка): Имя кондиционера. Как минимум один из параметров `id` или `name` должен быть указан!
- **id** (*Опциональный*, [ID](https://esphome.io/guides/configuration-types.html#config-id)): Укажите идентификатор кондиционера чтобы обращаться к нему из кода. Как минимум один из параметров `id` или `name` должен быть указан!
- **uart_id** (*Опциональный*, [ID](https://esphome.io/guides/configuration-types.html#config-id)): Укажите ID [шины UART](https://esphome.io/components/uart.html), к которой подключен кондиционер. Если сконфигурирована одна шина, то компонент подключит её автоматически. Если шин несколько, то лучше указать вручную.
- **period** (*Опциональный*, [время](https://esphome.io/guides/configuration-types.html#config-time), по умолчанию ``7s``): Период между запросами статуса кондиционера. `Aux_ac` получает новое состояние кондиционера только после регулярного запроса, потому что сам кондиционер об изменении параметров своеё работы не уведомляет. Поэтому нужно запрашивать его, вдруг пользователь установил иной режим работы с помощью ИК-пульта.
- **show_action** (*Опциональный*, логическое, по умолчанию ``true``): Показывать ли текущую задачу кондиционера (экспериментальная функция). Например, в режиме HEAT-COOL кондиционер может выполнять одну из следующих задач:
  - НАГРЕВ: нагревает воздух в комнате;
  - ПРОСТОЙ: кондиционер работает в режиме вентилятора для перемешивания воздуха в комнате, поскольку целевая температура уже достигнута;
  - ОХЛАЖДЕНИЕ: кондиционер охлаждает воздух в комнате.
  Аналогично будут отображаться действия кондиционера и для режимов ОТОПЛЕНИЕ и ОХЛАЖДЕНИЕ. Единственная разница будет в количестве действий: ПРОСТОЙ+НАГРЕВ для режима отопления и ПРОСТОЙ+ОХЛАЖДЕНИЕ для режима охлаждения комнаты.
- **display_inverted** (*Опциональный*, логическое, по умолчанию ``false``): Настраивает способ управления дисплеем. Как выяснилось (issue [#31](https://github.com/GrKoR/esphome_aux_ac_component/issues/31)), включение-выключение дисплея обрабатывается кондиционерами по разному. Кондиционеры Rovex включают дисплей по `0` в соответствующем бите команды и выключают по биту `1`. Многие другие модели кондиционеров поступают наоборот.
- **indoor_temperature** (*Опциональный*): Параметры создаваемого датчика температуры воздуха, если такой датчик нужен
  - **name** (**Обязательный**, строка): Имя датчика температуры.
  - **id** (*Опциональный*, [ID](https://esphome.io/guides/configuration-types.html#config-id)): Можно указать свой ID для датчика для использования в лямбдах.
  - **internal** (*Опциональный*, логическое): Пометить данный датчик как внутренний. Внутренний датчик не будет передаваться во фронтэнд (такой как Home Assistant). В противоположность стандартному поведению [сенсоров](https://esphome.io/components/sensor/index.html#base-sensor-configuration) этот параметр для датчика в кондиционере **всегда выставлен в true** за исключением случаев, когда пользователь не установил его в `false`. То есть по умолчанию значение сенсора не будет передаваться во фронтенд даже если указано `name` для сенсора.
  - Все остальные параметры [сенсора](https://esphome.io/components/sensor/index.html#base-sensor-configuration) ESPHome.
- **outdoor_temperature** (*Опциональный*): Параметры создаваемого датчика уличной температуры воздуха, если такой датчик нужен. Параметры аналогичны датчику внутренней температуры **indoor_temperature** (см. выше).
- **inbound_temperature** (*Опциональный*): Параметры создаваемого датчика температуры на подаче теплоносителя, если такой датчик нужен. Параметры аналогичны датчику внутренней температуры **indoor_temperature** (см. выше).
- **outbound_temperature** (*Опциональный*): Параметры создаваемого датчика температуры на обратке теплоносителя, если такой датчик нужен. Параметры аналогичны датчику внутренней температуры **indoor_temperature** (см. выше).
- **compressor_temperature** (*Опциональный*): Параметры создаваемого датчика температуры компрессора, если такой датчик нужен. Параметры аналогичны датчику внутренней температуры **indoor_temperature** (см. выше).
- **display_state** (*Опциональный*): Параметры создаваемого датчика дисплея (включен или выключен), если такой датчик нужен.
  - **name** (**Обязательный**, строка): Имя датчика дисплея.
  - **id** (*Опциональный*, [ID](https://esphome.io/guides/configuration-types.html#config-id)): Можно указать свой ID для датчика для использования в лямбдах.
  - **internal** (*Опциональный*, логическое): Пометить данный датчик как внутренний. Внутренний датчик не будет передаваться во фронтэнд (такой как Home Assistant). В противоположность стандартному поведению [бинарных сенсоров](https://esphome.io/components/binary_sensor/index.html#base-binary-sensor-configuration) этот параметр для датчика в кондиционере **всегда выставлен в true** за исключением случаев, когда пользователь не установил его в `false`. То есть по умолчанию значение сенсора не будет передаваться во фронтенд даже если указано `name` для сенсора.
  - Все остальные параметры [бинарного сенсора](https://esphome.io/components/binary_sensor/index.html#base-binary-sensor-configuration) ESPHome.
- **defrost_state** (*Опциональный*): Параметры создаваемого датчика состояния разморозки (включена или выключена), если такой датчик нужен. Параметры аналогичны датчику дисплея **display_state**.
- **invertor_power** (*Опциональный*): Параметры создаваемого датчика мощности инвертора, если такой датчик нужен. Параметры аналогичны датчику дисплея **display_state**.
- **preset_reporter** (*Опциональный*): Параметры создаваемого текстового датчика текущего активного пресета. Параметры аналогичны датчику дисплея **display_state**.  
Климатические устройства ESPHome не отправляют по MQTT активный пресет (см. **supported_presets** и **custom_presets**), в котором работает устройство. Если вы используете MQTT и хотите получать информацию о пресетах, то пропишите этот датчик в конфигурации.
- **supported_modes** (*Опциональный*, список): Список поддерживаемых режимов работы. Возможные значения: ``HEAT_COOL``, ``COOL``, ``HEAT``, ``DRY``, ``FAN_ONLY``. Обратите внимание: некоторые производители кондиционеров указывают на пульте режим AUTO, хотя по факту этот режим не работает по расписанию и только лишь поддерживает целевую температуру. Такой режим в ESPHome называется HEAT_COOL. По умолчанию список содержит только значение ``FAN_ONLY``.
- **custom_fan_modes** (*Опциональный*, список): Список поддерживаемых дополнительных режимов вентилятора. Возможные значения: ``MUTE``, ``TURBO``. По умолчанию никакие дополнительные режимы не установлены.
- **supported_presets** (*Опциональный*, список): Список поддерживаемых базовых функций кондиционера. Возможные значения: ``SLEEP``. По умолчанию никакие базовые функции не установлены.
- **custom_presets** (*Опциональный*, список): Список поддерживаемых дополнительных функций кондиционера. Возможные значения: ``CLEAN``, ``HEALTH``, ``ANTIFUNGUS``. По умолчанию никакие дополнительные функции не установлены.
- **supported_swing_modes** (*Опциональный*, список): Список поддерживаемых режимов качания шторки. Возможные значения: ``VERTICAL``, ``HORIZONTAL``, ``BOTH``. По умолчанию устанавливается, что качание шторки кондиционером не поддерживается.
- Все остальные параметры [климатического устройства](https://esphome.io/components/climate/index.html#base-climate-configuration) ESPHome.

## Действия: ##
### ``aux_ac.display_on`` ###
Включение экрана температуры на лицевой панели кондиционера.

```yaml
on_...:
  then:
    - aux_ac.display_on: aux_id
```
- **aux_id** (**Обязательный**, строка): ID компонента `aux_ac`.

### ``aux_ac.display_off`` ###
Выключение экрана температуры на лицевой панели кондиционера.

```yaml
on_...:
  then:
    - aux_ac.display_off: aux_id
```
- **aux_id** (**Обязательный**, строка): ID компонента `aux_ac`.

### ``aux_ac.vlouver_stop`` ###
Остановка вертикального движения жалюзи кондиционера. Если жалюзи качались в вертикальном направлении, то можно их остановить в нужном положении. 

```yaml
on_...:
  then:
    - aux_ac.vlouver_stop: aux_id
```
- **aux_id** (**Обязательный**, строка): ID компонента `aux_ac`.

### ``aux_ac.vlouver_swing`` ###
Включение вертикального качания жалюзи кондиционера.

```yaml
on_...:
  then:
    - aux_ac.vlouver_swing: aux_id
```
- **aux_id** (**Обязательный**, строка): ID компонента `aux_ac`.

### ``aux_ac.vlouver_top`` ###
Установка жалюзи в самое верхнее положение.

```yaml
on_...:
  then:
    - aux_ac.vlouver_top: aux_id
```
- **aux_id** (**Обязательный**, строка): ID компонента `aux_ac`.

### ``aux_ac.vlouver_middle_above`` ###
Установка жалюзи во второе сверху положение. Это положение между верхним и средним.

```yaml
on_...:
  then:
    - aux_ac.vlouver_middle_above: aux_id
```
- **aux_id** (**Обязательный**, строка): ID компонента `aux_ac`.

### ``aux_ac.vlouver_middle`` ###
Установка жалюзи в среднее положение.

```yaml
on_...:
  then:
    - aux_ac.vlouver_middle: aux_id
```
- **aux_id** (**Обязательный**, строка): ID компонента `aux_ac`.

### ``aux_ac.vlouver_middle_below`` ###
Установка жалюзи в положение ниже среднего.

```yaml
on_...:
  then:
    - aux_ac.vlouver_middle_below: aux_id
```
- **aux_id** (**Обязательный**, строка): ID компонента `aux_ac`.

### ``aux_ac.vlouver_bottom`` ###
Установка жалюзи в самое нижнее положение.

```yaml
on_...:
  then:
    - aux_ac.vlouver_bottom: aux_id
```
- **aux_id** (**Обязательный**, строка): ID компонента `aux_ac`.



## Простейший пример ##
Исходный код простейшего примера можно найти в файле [aux_ac_simple.yaml](https://github.com/GrKoR/esphome_aux_ac_component/blob/master/examples/simple/aux_ac_simple.yaml).

Все настройки в нем тривиальны и подробно описаны [в официальной документации на ESPHome](https://esphome.io/index.html) и дополнены в разделе о настройке компонента выше.<br />
Просто скопируйте yaml-файл примера в локальную папку у себя на компьютере, пропишите настройки вашей сети WiFi и откомпилируйте YAML с использованием ESPHome. 


## Продвинутый пример ##
Все исходники продвинутого примера лежат [в соответствующей папке](https://github.com/GrKoR/esphome_aux_ac_component/tree/master/examples/advanced).

В этом примере мы конфигурируем два относительно одинаковых кондиционера на работу с `aux_ac`.<br />
Вводные: представим, что у нас есть два кондея, расположенных в кухне и в гостиной. Эти кондиционеры могут и не быть одного бренда. Главное, чтобы они были совместимы с `aux_ac`.<br />  
Поскольку мы ленивы, мы пропишем все общие настройки обоих кондиционеров в общем конфигурационном файле `ac_common.yaml`.<br />
А все параметры, специфичные для каждого конкретного устройства, вынесем в отдельные файлы. Это файлы `ac_kitchen.yaml` и `ac_livingroom.yaml`. В них мы установим значения для подстановок `devicename` и `upper_devicename`, чтобы у устройств в сети были корректные имена самого компонента и его сенсоров. И здесь же мы указываем уникальные для каждого устройства IP-адреса, спрятанные в `secrets.yaml`.<br />
Кстати да! **Не забудьте** присвоить корректные значения `wifi_ip_kitchen`, `wifi_ota_ip_kitchen`, `wifi_ip_livingroom` и `wifi_ota_ip_livingroom` в файле `secrets.yaml` наряду с остальной "секретной" информацией (например пароли, токены и т.п.). Файл `secrets.yaml` по понятным причинам на гитхаб не выложен.

Если попытаться компилировать файл `ac_common.yaml`, то ESPHome выдаст ошибку. Для корректной прошивки необходимо компилировать `ac_kitchen.yaml` или `ac_livingroom.yaml`.