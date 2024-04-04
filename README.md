# Кастомный компонент для ESPHome для управления кондиционером по Wi-Fi <!--[![GitHub release](https://img.shields.io/github/v/release/GrKoR/esphome_aux_ac_component)](https://github.com/GrKoR/esphome_aux_ac_component/releases/) [![Телеграм](https://img.shields.io/badge/Telegram-2CA5E0?style=flat&logo=telegram&logoColor=white)](https://t.me/aux_ac) -->

English readme [is here](README-EN.md#esphome-aux-air-conditioner-custom-component-aux_ac). 

Управляет кондиционерами на базе AUX по Wi-Fi.<br />
По тексту ниже для компонента используется сокращение `aux_ac`.

Обсудить проект можно [в чате Телеграм](https://t.me/aux_ac).<br /> 
Отзывы о багах и ошибках, а так же запросы на дополнительный функционал оставляйте [в соответствующем разделе](https://github.com/GrKoR/esphome_aux_ac_component/issues).
Будет просто отлично, если к своему сообщению вы добавите лог и подробное описание. Для сбора логов есть [специальный скрипт на Python](https://github.com/GrKoR/ac_python_logger). С его помощью вы сможете сохранить в csv-файл все пакеты, которыми обменивается Wi-Fi модуль и сплит-система. Если такой лог дополнить описанием, в какое время и что именно вы пытались включить, то это сильно ускорит исправление багов.
Также есть [подробная инструкция, описывающая как правильно запросить фичу](docs/HOW_TO_FEATURE_REQUEST.md).


## ДИСКЛЭЙМЕР (ОТМАЗКИ) ##
1. Все материалы этого проекта (программы, прошивки, схемы, 3D модели и т.п.) предоставляются "КАК ЕСТЬ". Всё, что вы делаете с вашим оборудованием, вы делаете на свой страх и риск. Автор не несет ответственности за результат и ничего не гарантирует. Если вы с абсолютной четкостью не понимаете, что именно вы делаете и для чего, лучше просто купите Wi-Fi модуль у производителя вашего кондиционера. 
2. Я ~~не настоящий сварщик~~ не программер. Поэтому код наверняка не оптимален и плохо оформлен (зато комментариев по коду я разместил от души), местами может быть написан небезопасно. И хоть я и старался протестировать всё, но уверен, что какие-то моменты упустил. Так что отнеситесь к коду с подозрением, ожидайте от него подвоха и если что-то увидели - [пишите в багрепорт](https://github.com/GrKoR/esphome_aux_ac_component/issues).


## Поддерживаемые кондиционеры ## 
AUX - это один из нескольких OEM-производителей кондиционеров. AUX производят кондиционеры как под собственным брендом, так и для внешних заказчиков. Поэтому есть шанс, что произведенный на их фабрике кондиционер неизвестного бренда с `aux_ac` так же заработает.
В интернете есть такой перечень производившихся на фабриках AUX брендов: AUX, Abion, AC ELECTRIC, Almacom, Ballu , Centek, Climer, DAX, Energolux, ERISSON, Green Energy, Hyundai, IGC, Kentatsu (некоторые серии), Klimaire, KOMANCHI, LANZKRAFT, LEBERG, LGen, Monroe, Neoclima, NEOLINE, One Air, Pioneer (до 2016 года), Roda, Rovex, Royal Clima, SAKATA, Samurai, SATURN, Scarlett, SmartWay, Soling, Subtropic, SUBTROPIC, Supra, Timberk, Vertex, Zanussi. В его полноте и достоверности есть сомнения, но ничего лучше найти не удалось.


### Список совместимых (протестированных) кондиционеров ###
[Список протестированных кондиционеров](docs/AC_TESTED.md) размещен в отдельном файле и включает те модели, на которых `aux_ac` был запущен автором компонента или пользователями. Этот список постоянно пополняется, преимущественно по обратной связи от пользователей [в чате Телеграм](https://t.me/aux_ac).<br />
 
### Если кондиционер в списке отсутствует ###
Если ваш кондиционер отсутствует в списке протестированных, то это еще не значит, что его не получится подключить к Wi-Fi. Вот основные "звоночки", которые могут говорить о высоких шансах на успех:
1. Если производитель вашего кондиционера есть в списке протестированных выше, но модели нет.
2. Если на шильдике кондиционера в строке производитель написано что-то про AUX или Аукс.
3. Если в инструкции пользователя вашего кондиционера что-то написано про возможность управления по Wi-Fi с помощью мобильного приложения ACFreedom.
4. Если производитель вашего кондиционера предлагает для управления Wi-Fi модуль CTTM-40X24-WIFI-AKS (слева) или такой, как на фото справа. Причем правый модуль может быть как с USB-разъемом, так и с 5-контактным разъемом.  
   <img src="https://user-images.githubusercontent.com/57137862/172053621-60fe39d8-066e-44fa-91c5-725fa1f5c3bc.png" height="300">  <img src="https://user-images.githubusercontent.com/57137862/172053744-8ce4a13d-28cb-4688-a998-11ca3a7129df.png" height="300">  
   

Но будьте осмотрительны: ваш кондиционер никем не тестировался и важно четко понимать, что вы делаете. Иначе можете наломать дров.  
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
Если требуется прошить определенную версию компонента, используйте синтаксис из примера ниже. Здесь прошивается версия 0.2.14. Список версий смотрите [в тегах на гитхаб](https://github.com/GrKoR/esphome_aux_ac_component/tags).
```yaml
external_components:
  - source:
      type: git
      url: https://github.com/GrKoR/esphome_aux_ac_component
      ref: v.0.2.14
```
2. Настройте UART для коммуникации с вашим кондиционером:
```yaml
uart:
  id: ac_uart_bus
  # ВНИМАНИЕ! Для TX и RX на платах типа NodeMCU используйте GPIO4 (D2) и GPIO5 (D1)!
  # подробнее см. в документации: https://github.com/GrKoR/esphome_aux_ac_component/blob/master/docs/HARDWARE.md
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
    display_inverted: false
    timeout: 300
    optimistic: true
    indoor_ambient_temperature:
      name: AC Indoor Ambient Temperature
      id: ac_indoor_ambient_temp
      accuracy_decimals: 1
      internal: false
    outdoor_ambient_temperature:
      name: AC Outdoor Ambient Temperature
      id: ac_outdoor_ambient_temp
      internal: false
    outdoor_condenser_temperature:
      name: AC Outdoor Condenser Temperature
      id: ac_outdoor_condenser_temp
      internal: false
    compressor_suction_temperature:
      name: AC Compressor Suction Temperature
      id: ac_compressor_suction_temp
      internal: false
    indoor_coil_temperature:
      name: AC Indoor Coil Temperature
      id: ac_indoor_coil_temp
      internal: false
    compressor_discharge_temperature:
      name: AC Compressor Discharge Temperature
      id: ac_compressor_discharge_temp
      internal: false
    defrost_temperature:
      name: AC Defrost Temperature
      id: ac_defrost_temp
      internal: false
    display_state:
      name: AC Display State
      id: ac_display_state
      internal: false
    defrost_state:
      name: AC Defrost State
      id: ac_defrost_state
      internal: false
    inverter_power:
      name: AC Inverter Power
      id: ac_inverter_power
      internal: false
    inverter_power_limit_value:
      name: AC Inverter Power Limit Value
      id: ac_inverter_power_limit_value
      internal: false
    inverter_power_limit_state:
      name: AC Inverter Power Limit State
      id: ac_inverter_power_limit_state
      internal: false
    preset_reporter:
      name: AC Preset Reporter
      id: ac_preset_reporter
      internal: false
    vlouver_state:
      name: AC Vertical Louvers State
      id: ac_vlouver_state
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

- **period** (*Опциональный*, [время](https://esphome.io/guides/configuration-types.html#config-time), по умолчанию ``7s``): Период между запросами статуса кондиционера. `Aux_ac` получает новое состояние кондиционера только после регулярного запроса, потому что сам кондиционер об изменении параметров своей работы не уведомляет. Поэтому нужно запрашивать его, вдруг пользователь установил иной режим работы с помощью ИК-пульта.

- **display_inverted** (*Опциональный*, логическое, по умолчанию ``false``): Настраивает способ управления дисплеем. Как выяснилось (issue [#31](https://github.com/GrKoR/esphome_aux_ac_component/issues/31)), включение-выключение дисплея обрабатывается кондиционерами по разному. Кондиционеры Rovex включают дисплей по `0` в соответствующем бите команды и выключают по биту `1`. Многие другие модели кондиционеров поступают наоборот.

- **timeout** (*Опциональный*, неотрицательное целое, по умолчанию ``300``): Таймаут получения пакета для ресивера данных `aux_ac`.  
  Чаще всего вам это значение никогда не понадобится. Поскольку этот параметр опционален, то его можно смело пропустить, если нет необходимости менять таймауты.  
  Единственная ситуация, когда вам может пригодиться этот параметр, - это сильно загруженная ESP. Если по какой-то неподдающейся логике причине вы кроме `aux_ac` нагрузили свою ESP кучей дополнительных ресурсоемких задач, то у компонента может просто не хватать времени для оперативного приёма ответов от кондиционера. В этом случае в логе будут сообщения о том, что последовательность команд была прервана по таймауту. Чтобы это исправить, лучше, конечно, немного разгрузить ESP. Если это вам не подходит, тогда можно увеличить таймаут.  
  Значение таймаута в прошивке ограничено диапазоном от `300` до `800` миллисекунд. Устанавливать значения выше можно только отредактировав исходные коды компонента. Но сильно задирать таймаут не стоит. Кондиционер периодически рассылает пакеты без запроса со стороны `aux_ac` и это приводит к сбою в отправке команды.  

- **optimistic** (*Опциональный*, логическое, по умолчанию ``true``) В «оптимистичном» режиме компонент не ждёт от кондиционера изменения параметров работы, а сразу после отправки команды в кондиционер сообщает в Home Assistant о новом состоянии. Если кондиционер команду не принял, то спустя несколько секунд eps получит текущее состояние всех систем и отправит в умный дом реальное состояние кондиционера. В итоге, если подавать в кондиционер неподдерживаемые команды, они будут записываться в историю Home Assistant и спустя время сбрасываться сбрасываться.  
В «пессимистичном» режиме esp отправляет команду в кондиционер, но об изменении состояний не сообщает до тех пор, пока не получит информацию о фактическом режиме работы кондиционера.  
В большинстве случаев разница между этими режимами будет практически незаметна.  

- **indoor_ambient_temperature** (*Опциональный*): Параметры создаваемого датчика температуры воздуха, если такой датчик нужен
  - **name** (**Обязательный**, строка): Имя датчика температуры.
  - **id** (*Опциональный*, [ID](https://esphome.io/guides/configuration-types.html#config-id)): Можно указать свой ID для датчика для использования в лямбдах.
  - **internal** (*Опциональный*, логическое): Пометить данный датчик как внутренний. Внутренний датчик не будет передаваться во фронтэнд (такой как Home Assistant). В противоположность стандартному поведению [сенсоров](https://esphome.io/components/sensor/index.html#base-sensor-configuration) этот параметр для датчика в кондиционере **всегда выставлен в true** за исключением случаев, когда пользователь не установил его в `false`. То есть по умолчанию значение сенсора не будет передаваться во фронтенд даже если указано `name` для сенсора.
  - Все остальные параметры [сенсора](https://esphome.io/components/sensor/index.html#base-sensor-configuration) ESPHome.
  > **ВНИМАНИЕ!** Название сенсора было изменено в версии v.1.0.0 для синхронизации с сервисными схемами производителя кондиционеров.

- **outdoor_ambient_temperature** (*Опциональный*): Параметры создаваемого датчика уличной температуры воздуха, если такой датчик нужен. Параметры аналогичны датчику внутренней температуры **indoor_ambient_temperature** (см. выше).  
  > **ВНИМАНИЕ!** Когда кондиционер выключен, температура наружного воздуха обновляется редко (раз в 6-7 часов). Это не баг компонента, а особенность работы железа кондиционера. Единственный способ получать изменения чаще - создать шаблонный сенсор, температуру которого изменять вручную. Когда кондиционер работает, значение такого сенсора можно копировать из **outdoor_ambient_temperature**. Когда кондиционер выключен, значение температуры пересчитывать по динамике сенсора **compressor_suction_temperature** (он изменяется часто и при выключенном кондее показывает значения близкие к температуре воздуха). Заморочки с пересчетом нужны потому, что показания сенсоров не идентичны и на графике значений шаблонного сенсора могут быть ступеньки при переходе с **outdoor_ambient_temperature** на **compressor_suction_temperature** и обратно.  
  > **ВНИМАНИЕ!** Название сенсора было изменено в версии v.1.0.0 для синхронизации с сервисными схемами производителя кондиционеров.

- **outdoor_condenser_temperature** (*Опциональный*): Параметры создаваемого датчика температуры конденсатора в наружном блоке кондиционера, если такой датчик нужен. Параметры аналогичны датчику внутренней температуры **indoor_ambient_temperature** (см. выше).  

- **indoor_coil_temperature** (*Опциональный*): Параметры создаваемого датчика температуры на теплообменнике во внутреннем блоке кондиционера, если такой датчик нужен. Параметры аналогичны датчику внутренней температуры **indoor_ambient_temperature** (см. выше).
  > **ВНИМАНИЕ!** Название сенсора было изменено в версии v.1.0.0 для синхронизации с сервисными схемами производителя кондиционеров.

- **compressor_suction_temperature** (*Опциональный*): Параметры создаваемого датчика температуры на входе в компрессор, если такой датчик нужен. Параметры аналогичны датчику внутренней температуры **indoor_ambient_temperature** (см. выше).
  > **ВНИМАНИЕ!** Название сенсора было изменено в версии v.1.0.0 для синхронизации с сервисными схемами производителя кондиционеров.

- **compressor_discharge_temperature** (*Опциональный*): Параметры создаваемого датчика температуры на выходе компрессора, если такой датчик нужен. Параметры аналогичны датчику внутренней температуры **indoor_ambient_temperature** (см. выше).
  > **ВНИМАНИЕ!** Название сенсора было изменено в версии v.1.0.0 для синхронизации с сервисными схемами производителя кондиционеров.

- **defrost_temperature** (*Опциональный*): Параметры создаваемого датчика температуры разморозки в наружном блоке кондиционера, если такой датчик нужен. Параметры аналогичны датчику внутренней температуры **indoor_ambient_temperature** (см. выше).  

- **display_state** (*Опциональный*): Параметры создаваемого датчика дисплея (включен или выключен), если такой датчик нужен.
  - **name** (**Обязательный**, строка): Имя датчика дисплея.
  - **id** (*Опциональный*, [ID](https://esphome.io/guides/configuration-types.html#config-id)): Можно указать свой ID для датчика для использования в лямбдах.
  - **internal** (*Опциональный*, логическое): Пометить данный датчик как внутренний. Внутренний датчик не будет передаваться во фронтэнд (такой как Home Assistant). В противоположность стандартному поведению [бинарных сенсоров](https://esphome.io/components/binary_sensor/index.html#base-binary-sensor-configuration) этот параметр для датчика в кондиционере **всегда выставлен в true** за исключением случаев, когда пользователь не установил его в `false`. То есть по умолчанию значение сенсора не будет передаваться во фронтенд даже если указано `name` для сенсора.
  - Все остальные параметры [бинарного сенсора](https://esphome.io/components/binary_sensor/index.html#base-binary-sensor-configuration) ESPHome.

- **defrost_state** (*Опциональный*): Параметры создаваемого датчика состояния разморозки (включена или выключена), если такой датчик нужен. Параметры аналогичны датчику дисплея **display_state**.

- **inverter_power** (*Опциональный*): Параметры создаваемого датчика мощности инвертора, если такой датчик нужен. Параметры аналогичны датчику дисплея **display_state**.
  > **ВНИМАНИЕ!** Название параметра было изменено в версии v.0.2.9 в рамках борьбы с безграмотностью.

- **inverter_power_limit_state** (*Опциональный*): Параметры создаваемого датчика состояния функции ограничения мощности. Показывает, включена данная функция в настоящий момент или нет. По очевидным причинам актуально только для инверторных кондиционеров, для "старт-стоп" кондиционеров всегда будет "выключен". Параметры аналогичны датчику дисплея **display_state**.

- **inverter_power_limit_value** (*Опциональный*): Параметры создаваемого датчика текущего ограничения мощности, если такой датчик нужен. Параметры аналогичны датчику внутренней температуры **indoor_ambient_temperature** (см. выше).  
Сенсор отображает текущее значение ограничения максимальной мощности для инверторного кондиционера. Значение в процентах. С кондиционерами "старт-стоп" по очевидным причинам не работает, всегда показывая значение `0%`.  Заданное пользователем значения лимита будет отображено только после того, как кондиционер подтвердит полученное значение и начнет с ним работать.  
В силу ограничений на уровне железа лимит мощности может быть задан только в пределах от `30%` до `100%`.

- **preset_reporter** (*Опциональный*): Параметры создаваемого текстового датчика текущего активного пресета. Параметры аналогичны датчику дисплея **display_state**.  
  Климатические устройства ESPHome не отправляют по MQTT активный пресет (см. **supported_presets** и **custom_presets**), в котором работает устройство. Если вы используете MQTT и хотите получать информацию о пресетах, то пропишите этот датчик в конфигурации.

- **vlouver_state** (*Опциональный*): Параметры создаваемого сенсора состояния вертикальных жалюзи. Параметры аналогичны датчику дисплея **display_state**.  Состояние жалюзи кодируется целочисленными значениями (подробнее смотри [aux_ac.vlouver_set action](#aux_ac_._vlouver_set) ниже).

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

### ``aux_ac.vlouver_set`` ###
Переводит жалюзи в указанное состояние.

Состояние кодируется следующими целочисленными значениями:  
- `0`: жалюзи находятся в состоянии `SWING` (качаются вверх-вниз);
- `1`: жалюзи остановлены в каком-то пользовательском положении;
- `2`: жалюзи установлены в верхнее положение;
- `3`: жалюзи установлены в положение на шаг выше среднего;
- `4`: жалюзи установлены в среднее положение;
- `5`: жалюзи установлены в положение на шаг ниже среднего;
- `6`: жалюзи установлены в нижнее положение. 

```yaml
on_...:
  then:
    - aux_ac.vlouver_set:
        id: aux_id
        position: 3 # устанавливаем жалюзи в среднее положение
```
- **aux_id** (**Обязательный**, строка): ID компонента `aux_ac`.
- **position** (**Обязательный**, целое число): состояние вертикальных жалюзи.

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

### ``aux_ac.power_limit_off`` ###
Отключает лимит мощности инверторного кондиционера, если такой лимит был установлен.

```yaml
on_...:
  then:
    - aux_ac.power_limit_off: aux_id
```
- **aux_id** (**Обязательный**, строка): ID компонента `aux_ac`.

### ``aux_ac.power_limit_on`` ###
Включает ограничение мощности для инверторного кондиционера, а также может задавать предельное значение мощности. Для кондиционеров "старт-стоп" не работает, вызов игнорируется.

```yaml
on_...:
  then:
    - aux_ac.power_limit_on:
        id: aux_id
        limit: 46 # ограничивает максимальную мощность инверторного кондиционера на уровне 46%
```
- **aux_id** (**Обязательный**, строка): ID компонента `aux_ac`.
- **limit** (**Опциональный**, целое число): задаваемое пользователем максимальное значение мощности инверторного кондиционера.  
  При установленном лимите кондиционер не будет превышать это значение в работе.  
  > **Обратите внимание**, что задание лимита повлияет на эффективность работы сплит-системы. Например, при низком значении лимита кондиционеру может не хватать мощности, чтобы охладить или нагреть комнату до заданной пользователем температуры. Либо время, затраченное кондиционером на нагрев или охлаждение, может вырасти. Имейте это ввиду при установке ограничений.

  В силу ограничений на уровне железа, лимит мощности должен быть в пределах от `30%` до `100%`. Некорректные значения будут приведены к диапазону.   
  В случае, если включение лимита вызывается без указания параметра `limit`, то будет использовано значение по умолчанию `30%`.


## Простейший пример ##
Исходный код простейшего примера можно найти в файле [aux_ac_simple.yaml](https://github.com/GrKoR/esphome_aux_ac_component/blob/master/examples/simple/aux_ac_simple.yaml).

Все настройки в нем тривиальны и подробно описаны [в официальной документации на ESPHome](https://esphome.io/index.html) и дополнены в разделе о настройке компонента выше.<br />
Просто скопируйте yaml-файл примера в локальную папку у себя на компьютере, пропишите настройки вашей сети Wi-Fi и откомпилируйте YAML с использованием ESPHome. 


## Продвинутый пример ##
Все исходники продвинутого примера лежат [в соответствующей папке](https://github.com/GrKoR/esphome_aux_ac_component/tree/master/examples/advanced).

В этом примере мы конфигурируем два относительно одинаковых кондиционера на работу с `aux_ac`.<br />
Вводные: представим, что у нас есть два кондея, расположенных в кухне и в гостиной. Эти кондиционеры могут и не быть одного бренда. Главное, чтобы они были совместимы с `aux_ac`.<br />  
Поскольку мы ленивы, мы пропишем все общие настройки обоих кондиционеров в общем конфигурационном файле `ac_common.yaml`.<br />
А все параметры, специфичные для каждого конкретного устройства, вынесем в отдельные файлы. Это файлы `ac_kitchen.yaml` и `ac_livingroom.yaml`. В них мы установим значения для подстановок `devicename` и `upper_devicename`, чтобы у устройств в сети были корректные имена самого компонента и его сенсоров. И здесь же мы указываем уникальные для каждого устройства IP-адреса, спрятанные в `secrets.yaml`.<br />
Кстати да! **Не забудьте** присвоить корректные значения `wifi_ip_kitchen`, `wifi_ota_ip_kitchen`, `wifi_ip_livingroom` и `wifi_ota_ip_livingroom` в файле `secrets.yaml` наряду с остальной "секретной" информацией (например пароли, токены и т.п.). Файл `secrets.yaml` по понятным причинам на гитхаб не выложен.

Если попытаться компилировать файл `ac_common.yaml`, то ESPHome выдаст ошибку. Для корректной прошивки необходимо компилировать `ac_kitchen.yaml` или `ac_livingroom.yaml`.
