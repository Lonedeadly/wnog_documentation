
# Документация API WNOG

## Содержание <span id="Содержание">
1. [Авторизация ](#Authorization)<span>
2. [Перевозка](#Shipping)
    1. [Получение информации (GET)](#ShippingGet)
        1. [Запрос](#ShippingGetRequest)
        2. [Ответ](#ShippingGetAnswer)

## [1. Авторизация](#Содержание)<span id="Authorization"><span>

Указываем токен в заголовках HTTP запроса под ключем "Authorization"

## [2. Перевозка](#Содержание)<span id="Shipping"><span>

> Наименование метода: **Order**

### [2.1 Получение информации (GET)](#Содержание)<span id="ShippingGet"><span>

### [Запрос:](#Содержание)<span id="ShippingGetRequest"><span>
> Метод запроса: **GET**

Параметры передаются в теле запроса в виде массива: 
#### Структура запроса:
| Ключ | Описание | Тип данных (Макс. длина) |
| :-------------|:-----------|:-----|
| order_number* | Номер заявки | Массив: <br/>`Строка (100)` |
ИЛИ
| delivery_contract_number*| Номер договора поставки | `Строка (50)` |
| application_number* | Номер приложения | `Строка (30)` |

*В параметрах запроса указывается (order_number) или (delivery_contract_number и application_number)

**Пример тела запроса:**
>[<br/>
&emsp;{<br/>
&emsp;&emsp;"order_number": "НомерЗаявки"<br/>
&emsp;},<br/>
&emsp;{<br/>
&emsp;&emsp;"delivery_contract_number": "НомерДоговораПоставки",<br/>
&emsp;&emsp;"application_number": "НомерПриложения"<br/>
&emsp;}<br/>
]<br/>

### [Ответ:](#Содержание)<span id="ShippingGetAnswer"><span>
#### Структура ответа:
| Поле | Описание | Тип данных (Макс. длина) |
| :-------------|:-----------|:-----|
| client_reference | Референс клиента | `Строка (1000)` |
| quote_number | Номер котировки | `Строка (100)` |
| wnog_reference | Референс WNOG | `Строка (8)` | 
| delivery_contract_number| Номер договора поставки | `Строка (50)` |
| application_number | Номер приложения | `Строка (30)` |
| client_coordinators | Координатор клиента | Массив: `Строка (100)` |
| wnog_coordinator | Координатор WNOG | `Строка (100) `|
| product_line | Продуктовая линейка | `Строка (50)` |
| vehicle_type | Тип транспорта <br/> - auto<br/> - air<br/> - sea<br/> - rail | `Строка (5)` | 
| vehicle_number | Номер ТС | `Строка (100)` |
| order_number | Номер заявки | `Строка (100)` |
| service_level | Вид перевозки | `Строка (25)` |
| cargo_name | Наименование груза | `Строка (300) `|
| cargo_count | Количество мест факт. | `Число (10,0)` |
| cargo_weight | Общий вес факт. | `Число (10,2)` |
| cargo_volume | Общий объем факт. | `Число (10,2)` |
| pre_cargo_count | Количество мест план. | `Число (10,0)` |
| pre_cargo_weight | Общий вес план. | `Число (10,2)` |
| pre_cargo_volume | Общий объем план. | `Число (10,2)` |
| etd | ETD | `Дата` |
| eta | ETA | `Дата` |
| atd | ATD | `Дата` |
| ata | ATA | `Дата` |
| point_city | Точка рейса | `Строка (150)` |
| point_status | Статус точки <br/> - Прибытие на погрузку <br/> - Задержка прибытия <br/> - На погрузке <br/> - Простой на погрузке <br/> - Погружено <br/> - В пути <br/> - Задержка в пути <br/> - На выгрузке <br/> - Простой на выгрузке <br/> - Выгружено | `Строка (50)` |
| point_dateStatus | Дата статуса | `Дата` |
| point_fias_id | Код в системе ФИАС | `Строка (36)` |
| point_kladr_id | Код в системе КЛАДР | `Строка (50)` |
| history_points | История точек рейса | Массив [history_point](#history_point)|

#### history_point:<span id="history_point"><span>
| Поле | Описание | Тип данных (Макс. длина) |
| :-------------|:-----------|:-----|
| city | Точка рейса | `Строка (150)` |
| date | Дата статуса | `Дата` |
| status | Статус точки <br/> - Прибытие на погрузку <br/> - Задержка прибытия <br/> - На погрузке <br/> - Простой на погрузке <br/> - Погружено <br/> - В пути <br/> - Задержка в пути <br/> - На выгрузке <br/> - Простой на выгрузке <br/> - Выгружено | `Строка (150)` |
| fias_id | Код в системе ФИАС | `Строка (50)` |
| kladr_id | Код в системе КЛАДР | `Строка (50)` |

**Пример ответа:**
>[<br/> 
&emsp;&emsp;{<br/>
&emsp;&emsp;&emsp;&emsp;"client_reference": "РеференсКлиента",<br/>
&emsp;&emsp;&emsp;&emsp;"quote_number": "НомерКотировки",<br/>
&emsp;&emsp;&emsp;&emsp;"wnog_reference": "000.0000",<br/>
&emsp;&emsp;&emsp;&emsp;"delivery_contract_number": "НомерДоговораПоставки",<br/>
&emsp;&emsp;&emsp;&emsp;"application_number": "НомерПриложения",<br/>
&emsp;&emsp;&emsp;&emsp;"client_coordinators": [<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;"Иван Иванов"<br/>
&emsp;&emsp;&emsp;&emsp;],<br/>
&emsp;&emsp;&emsp;&emsp;"wnog_coordinator": "Петр Петров",<br/>
&emsp;&emsp;&emsp;&emsp;"product_line": "Продуктовая линейка",<br/>
&emsp;&emsp;&emsp;&emsp;"vehicle_type": "auto",<br/>
&emsp;&emsp;&emsp;&emsp;"vehicle_number": "RU050369929",<br/>
&emsp;&emsp;&emsp;&emsp;"order_number": "30996928",<br/>
&emsp;&emsp;&emsp;&emsp;"service_level": "LTL",<br/>
&emsp;&emsp;&emsp;&emsp;"cargo_name": "Оборудование (газовое и нефтегазовое)",<br/>
&emsp;&emsp;&emsp;&emsp;"cargo_count": 1,<br/>
&emsp;&emsp;&emsp;&emsp;"cargo_weight": 3,<br/>
&emsp;&emsp;&emsp;&emsp;"cargo_volume": 0.01,<br/>
&emsp;&emsp;&emsp;&emsp;"cargo_count_plan": 1,<br/>
&emsp;&emsp;&emsp;&emsp;"cargo_weight_plan": 3,<br/>
&emsp;&emsp;&emsp;&emsp;"cargo_volume_plan": 0.02,<br/>
&emsp;&emsp;&emsp;&emsp;"etd": "2021-04-23T00:00:00",<br/>
&emsp;&emsp;&emsp;&emsp;"eta": "2021-04-30T00:00:00",<br/>
&emsp;&emsp;&emsp;&emsp;"atd": "2021-04-23T00:00:00",<br/>
&emsp;&emsp;&emsp;&emsp;"ata": "2021-04-27T00:00:00",<br/>
&emsp;&emsp;&emsp;&emsp;"point_city": "Мегион, Ханты-Манс. авт. окр.",<br/>
&emsp;&emsp;&emsp;&emsp;"point_status": "Выгружено",<br/>
&emsp;&emsp;&emsp;&emsp;"point_fias_id": "d9c157ca-fd05-4efc-ae0c-16927612a0c8",<br/>
&emsp;&emsp;&emsp;&emsp;"point_kladr_id": "8600000400000",<br/>
&emsp;&emsp;&emsp;&emsp;"point_dateStatus": "2021-04-28T12:41:01"<br/>
&emsp;&emsp;&emsp;&emsp;"history_points": [<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;{<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;"city": "Тюмень, Тюменская область",<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;"date": "2021-04-23T14:17:47",<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;"status": "Прибытие на погрузку",<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;"fias_id": "9ae64229-9f7b-4149-b27a-d1f6ec74b5ce",<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;"kladr_id": "7200000100000"<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;},<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;{<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;"city": "Тюмень, Тюменская область",<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;"date": "2021-04-23T15:17:47",<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;"status": "На погрузке",<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;"fias_id": "9ae64229-9f7b-4149-b27a-d1f6ec74b5ce",<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;"kladr_id": "7200000100000"<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;}<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;{<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;"city": "Тюмень, Тюменская область",<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;"date": "2021-04-23T14:20:41",<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;"status": "Погружено",<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;"fias_id": "9ae64229-9f7b-4149-b27a-d1f6ec74b5ce",<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;"kladr_id": "7200000100000"<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;},<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;{<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;"city": "Сургут, Ханты-Манс. авт. окр.",<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;"date": "2021-04-26T14:07:13",<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;"status": "В пути",<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;"fias_id": "",<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;"kladr_id": ""<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;},<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;{<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;"city": "Сургут, Ханты-Манс. авт. окр.",<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;"date": "2021-04-27T00:00:00",<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;"status": "Задержка в пути",<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;"fias_id": "",<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;"kladr_id": ""<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;},<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;{<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;"city": "Мегион, Ханты-Манс. авт. окр.",<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;"date": "2021-04-27T10:35:25",<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;"status": "На выгрузке",<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;"fias_id": "d9c157ca-fd05-4efc-ae0c-16927612a0c8",<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;"kladr_id": "8600000400000"<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;},<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;{<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;"city": "Мегион, Ханты-Манс. авт. окр.",<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;"date": "2021-04-28T12:41:01",<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;"status": "Выгружено",<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;"fias_id": "d9c157ca-fd05-4efc-ae0c-16927612a0c8",<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;"kladr_id": "8600000400000"<br/>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;}<br/>
&emsp;&emsp;&emsp;&emsp;]<br/>
&emsp;&emsp;}<br/>
]<br/>
