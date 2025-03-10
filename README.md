# VK

## Содержание
  ### [1. Тема и целевая аудитория](#topic)
  ### [2. Расчет нагрузки](#load)
  ### [3. Глобальная балансировка нагрузки](#balancing)
  ### [Список источников](#sources)

<a name="topic"></a>
## 1. Тема и целевая аудитория

### Тема

**ВКонтакте (VK)** – крупнейшая в России социальная сеть.

### Целевая аудитория

- Средняя месячная аудитория (MAU) составляет 126 млн в месяц [^3]
- Средняя месячная аудитория в России (MAU) составляет 90 млн в месяц [^4]
- Средняя дневная аудитория (DAU) в России составляет 56,5 млн пользователей [^18]
- Во ВКонтакте зарегистрировано 22,4 млн авторов [^5]
- Пользователи ВКонтакте проводят в социальной сети в среднем 45 минут в день (по данным на 2024 год) [^6]
- По данным на конец 2023 года пользователи ВКонтакте отправляют 395 млн заявок в друзья в месяц [^7]
- У женщин обычно больше друзей: в среднем — 132, тогда как у мужчин — 111. То есть в среднем у пользователя ВКонтакте 121,5 друг [^7]
- В 2024 году во ВКонтакте было опубликовано 7,6 миллиардов единиц контента (посты, клипы, видео, истории) [^8]
- В среднем сообщество во ВКонтакте в 2024 году выпускало 71,16 поста в месяц (без учета VK Видео и VK Клипов) [^9]
- В среднем пользователь ВКонтакте публикует в месяц 16,9 сообщений [^12]
- Посты с картинками смотрят 64% пользователей ВКонтакте (по данным на 2024 год) [^10]
- В среднем активный пользователь подписан на 121 сообщество [^11]
- 68% пользователей смотрят контент в ленте [^11]
- 64% пользователей смотрят контент в сообществах [^11]
- Средний Visibility Rate на пост в 2024-м — 17,27% [^13]
- 1 млрд лайков в сутки на 2022 год [^15]
- Количество просмотров разных видов контента: 10,3 млрд в сутки (на 2022 год) [^14]

### Веб-трафик по странам 

[![Traffic by Country](img/countries.jpeg)](https://www.similarweb.com/ru/website/vk.com/#overview) [^1]

### MVP

**Ключевой функционал** - просмотр новостной ленты пользователя
- Регистрация и авторизация пользователей
- Публикация постов на странице пользователя (текст, фото, видео)
- Добавление пользователей в друзья
- Создание сообществ, в которые могут вступать пользователи
- Публикация постов на странице сообщества (текст, фото, видео)
- Просмотр страниц пользователя и сообществ
- Возможность ставить лайки на пост от лица пользователя
- Комментарии под постами от лица пользователя
- Система рекомендаций постов в ленте пользователя, основанная на просмотренных постах, лайках, комментариях пользователя

<a name="load"></a>
## 2. Расчет нагрузки 

### Продуктовые метрики

Средняя дневная аудитория (DAU) в России составляет 56,5 млн пользователей [^2]. 88.94% аудитории ВКонтакте из России [^1]. Тогда общий DAU: 56,5 : 0,8894 = 63,53 млн чел в день.

| Характеристика | Значение                 |
|----------------|--------------------------|
| MAU            | 126 млн чел в месяц [^3] |
| DAU            | 63,53 млн чел в день     |

В среднем пользователь ВКонтакте публикует в месяц 16,9 сообщений [^12]. Тогда в день это примерно 16,9 : 30 = 0,56 сообщения.

В среднем сообщество во ВКонтакте выпускает 71,16 поста в месяц [^9]. Тогда в день это примерно 71,16 : 30 = 2,37 поста.

Пользователи ВКонтакте отправляют 395 млн заявок в друзья в месяц [^7]. Поделим на MAU, чтобы получить примерную статистику для 1 пользователя в месяц. 395 млн : 126 млн = 3,135 заявок в друзья в месяц делает 1 пользователь. Тогда в день это примерно 3,135 : 30 = 0,1 заявка.

Количество просмотров разных видов контента в социальной сети в 2022-м достигло показателя 10,3 млрд в сутки [^14]. DAU на 2022 год в России составлял 51,1 млн, на 2024 год в России - 56,5 млн. То есть DAU увеличился на 10,6%. Предположим, что количество просмотра контента увеличивается пропорционально DAU, тогда в сутки в 2024 эта цифра предположительно будет равна 10,3 млрд * 1,106 = 11,4 млрд в сутки. Поделим на DAU, чтобы узнать статистику на одного пользователя. 11,4 млрд : 63,53 млн = 179,4 просмотра на одного пользователя в сутки.

Бесконечная лента прогружается по 15 постов в чанке (включая рекламные посты). Тогда запросов на обновление ленты на 1 пользователя 179,4 : 15 = 11,96.

1 млрд лайков в сутки на 2022 год [^15]. DAU на 2022 год в России составлял 51,1 млн, на 2024 год в России - 56,5 млн. То есть DAU увеличился на 10,6%. Предположим, что количество лайков увеличивается пропорционально DAU, тогда в сутки в 2024 эта цифра предположительно будет равна 1 млрд * 1,106 = 1,106 млрд в сутки. Поделим на DAU, чтобы узнать статистику на одного пользователя. 1,106 млрд : 63,53 млн = 17,4 лайка на одного пользователя в сутки.

Данные по комментариям отсутствуют. Был проведен анализ на небольшой выборке постов из ленты ВК. Коэффициент корреляции лайков к комментариям получился 0,11. Это говорит о слабой связности данных. Но в виду отсутствия других данных возьмем получившиеся результаты: число комментариев в 26,5 раз меньше, чем лайков. Тогда в сутки это 17,4 : 26,5 = 0,66 комментария.

В среднем у пользователя ВКонтакте 121,5 друг [^7]. В среднем активный пользователь подписан на 121 сообщество [^11]. Можно предположить, что подписок на сообщества оформляется примерно столько же, сколько отправляется заявок в друзья. Примем это число за 0,1 подписки в сутки.

| Действие пользователя                 | Количество в день |
|---------------------------------------|-------------------|
| Публикация поста от лица пользователя | 0,56              |
| Публикация поста от лица сообщества   | 2,37              |
| Отправка заявки в друзья              | 0,1               |
| Просмотр поста                        | 179,4             |
| Запросов на обновление ленты          | 11,96             |
| Лайк на пост                          | 17,4              |
| Комментарий                           | 0,66              |
| Подписка на сообщество                | 0,1               |

#### Хранилище на пользователя

- Для аватарки и обложки учитываем максимально допустимый размер [^17]
- Средний размер фотографии - 2,2 МБ. Предполагаем, что у среднестатистического пользователя в профиле ~40 фотографий. Тогда около 88 МБ занимают фотографии в профиле
- Предполагаем, что у среднестатистического пользователя в профиле ~5 видео, видео хранятся ссылкой на vkvideo. На хранение одной ссылки нужно 100 байт, тогда всего надо 500 байт=~0,0005 МБ
- Предполагаем, что у среднестатистического пользователя в профиле около 60 постов, содержащих текст. Один символ кодируется 1 байтом, в среднем в одном посте 250 символов. Тогда это около 250 * 60 = 15 000 байт = 0,014 МБ
- В среднем у пользователя 121,5 друг. На хранение подписки на друга нужно около 20 байт. 20 * 121,5 = 2 430 байт = 0,0023 МБ
- В среднем пользователь подписан на 121 сообщество. На хранение подписки на сообщество нужно около 20 байт. 20 * 121 = 2 420 байт = 0,0023 МБ
- В среднем на пользователя надо хранить около 10000 лайков. На хранение лайка нужно около 20 байт. 20 * 10000 = 200 000 байт = 0,2 МБ

| Тип                                 | Размер     |
|-------------------------------------|------------|
| Аватарка                            | 5 МБ       |
| Обложка                             | 20 МБ      |
| Текстовая информация о пользователе | ~0,003 МБ  |
| Опубликованные фото                 | 88 МБ      |
| Опубликованные видео                | ~0,0005 МБ |
| Опубликованные текстовые посты      | 0,014 МБ   |
| Подписки на друзей                  | 0,0023 МБ  |
| Подписки на сообщества              | 0,0023 МБ  |
| Лайки                               | 0,2 МБ     |
| Итого                               | 113,222 МБ |

### Технические метрики

#### Размер хранилища

- ВКонтакте был запущен в 2006 году. То есть ВКонтакте функционирует уже 19 лет. За это время было выпущено около 1 500 млрд постов.
- В месяц публикуется 71,16 + 16,9 = 88,06 постов [^9] [^12]. Умножим на MAU: 88,06 * 126 = 11 095,56 млн постов в месяц
- Размер одного поста с фото 5 КБ (аватарка) + 2252,8 КБ (фотография) + 0,1 КБ (небольшая подпись) = 2257,9 КБ. Постов с фото 64%. 0,64 * 11 095,56 = 7 101,158 млн постов с фото в месяц. Это 7 101,158 * 2257,9 = 16 033 065,544 млн КБ в месяц = 14 933 ТБ в месяц. За все время это примерно 0,64 * 1 500 = 960 млрд постов. 960 000 000 000 * 2257,9 = 2 167 584 млрд КБ = 201 871,99 ТБ
- Размер одного поста с видео 5 КБ (аватарка) + 0,1 КБ (видео ссылкой) + 0,1 КБ (небольшая подпись) = 5,2 КБ. Постов с видео 20%. 0,2 * 11 095,56 = 2 219,112 млн постов с видео в месяц. Это 2 219 112 000 * 5,2 = 1,154×10¹⁰ КБ в месяц = 10,75 ТБ в месяц. За все время это примерно 0,2 * 1 500 = 300 млрд постов. 300 000 000 000 * 5,2 = 1 560 млрд КБ = 1 452,86 ТБ
- Размер одного текстового поста 5 КБ (аватарка) + 0,5 КБ = 5,5 КБ. Текстовых постов 16%. 0,16 * 11 095,56 = 1 775,29 млн постов с текстом в месяц. Это 1 775 290 000 * 5,5 = 9 764 095 000 КБ в месяц = 9,09 ТБ в месяц. За все время это примерно 0,16 * 1 500 = 240 млрд постов. 240 000 000 000 * 5,5 = 1 320 млрд КБ = 1 229,35 ТБ
- Данные одного пользователя без постов: 25,208 МБ. Допутим, что в месяц мы бы хранили данные активных пользователей: 25,208 * 126 000 000 = 3 176 208 000 МБ = 3 029,1 ТБ. За все время во ВКонтакте было зарегистрировано около 650 млн пользователей, около 30% - пустые/неактивные аккаунты или боты. Тогда за все время это около 25,208 * 650 000 000 * 0,7 = 11 469 640 000 МБ = 11 469,64 ТБ  

| Тип                  | Объем в ТБ на месяц | Общий объем в ТБ |
|----------------------|---------------------|------------------|
| Текстовые посты      | 9,09                | 1 229,35         |
| Посты с фото         | 14 933              | 201 871,99       |
| Посты с видео        | 10,75               | 1 452,86         |
| Данные пользователей | 3 029,1 ТБ          | 11 469,64        |


#### Сетевой трафик

Формула: трафик на действие * RPS

- Лайк: 18 * 12 794,236 = 230 296,248 КБ/с = 0,22 Гбит/с. Пиковое: 0,22 * 2 = 0,44 Гбит/с. Суммарный суточный: 0,22 * 86400 * 0,125 = 2 376  Гбайт/сутки
- Комментарий: 2,97 * 485,299 = 1 441,338 КБ/с = 0,01 Гбит/с. Пиковое: 0,01 * 2 = 0,02 Гбит/с. Суммарный суточный: 0,01 * 86400 * 0,125 = 108 Гбайт/сутки
- Прогрузка одной страницы в ленте: 1 * 8 794,199 = 8 794,199 МБ/с = 68,7 Гбит/с. Пиковое: 68,7 * 2 = 137,4 Гбит/с. Суммарный суточный: 68,7 * 86400 * 0,125 = 741 960 Гбайт/сутки
- Публикация поста: 30 * (411,769 + 1 742,663) / 2 = 32 316,48 КБ/с = 0,25 Гбит/с. Пиковое: 0,25 * 2 = 0,5 Гбит/с. Суммарный суточный: 0,25 * 86400 * 0,125 = 2 700 Гбайт/сутки
- Отправка заявки в друзья: 758 * 73,53 = 55 735,74 байт/с = 0,00042 Гбит/с. Пиковое: ,00042 * 2 = 0,00084 Гбит/с. Суммарный суточный: 0,00042 * 86400 * 0,125 = 4,536 Гбайт/сутки
- Подписка на сообщество: 13,98 * 73,53 = 1 027,949 КБ/с = 0,008 Гбит/с. Пиковое: 0,008 * 2 = 0,016 Гбит/с. Суммарный суточный: 0,008 * 86400 * 0,125 = 86,4 Гбайт/сутки

| Действие                         | Трафик на действие | Среднее потребление Гбит/с | Пиковое потребление Гбит/с | Суммарный суточный трафик Гбайт/сутки |
|----------------------------------|--------------------|----------------------------|----------------------------|---------------------------------------|
| Лайк                             | 18 КБ              | 0,22                       | 0,44                       | 2 376                                 |
| Комментарий                      | 2,97 КБ            | 0,01                       | 0,02                       | 108                                   |
| Прогрузка одной страницы в ленте | 1 МБ               | 68,7                       | 137,4                      | 741 960                               |
| Публикация поста                 | 30 КБ              | 0,25                       | 0,5                        | 2 700                                 |
| Отправка заявки в друзья         | 758 байт           | 0,00042                    | 0,00084                    | 4,536                                 |
| Подписка на сообщество           | 13,98 КБ           | 0,008                      | 0,016                      | 86,4                                  |

#### RPS

Формула: (количество запросов в день от одного пользователя * DAU) / 86400 секунд

- Публикация поста от лица пользователя: (0,56 * 63530000) / 86400 = 412 
- Публикация поста от лица сообщества: (2,37 * 63530000) / 86400 = 1 743 
- Отправка заявки в друзья: (0,1 * 63530000) / 86400 = 74 
- Запрос на обновление ленты: (11,96 * 63530000) / 86400 = 8 794 
- Лайк на пост: (17,4 * 63530000) / 86400 = 12 794 
- Комментарий: (0,66 * 63530000) / 86400 = 485 
- Подписка на сообщество: (0,1 * 63530000) / 86400 = 74

Ввиду отсутствия данных считаем, что пиковое значение RPS в 2 раза больше среднего.

| Тип запроса                           | Средний RPS | Пиковый RPS |
|---------------------------------------|-------------|-------------|
| Публикация поста от лица пользователя | 412         | 824         |
| Публикация поста от лица сообщества   | 1 743       | 3 486       |
| Отправка заявки в друзья              | 74          | 148         |
| Запрос на обновление ленты            | 8 794       | 17 588      |
| Лайк на пост                          | 12 794      | 25 588      |
| Комментарий                           | 485         | 970         |
| Подписка на сообщество                | 74          | 148         |
| Итого                                 | 24 376      | 48 752      |

<a name="balancing"></a>
## 3. Глобальная балансировка нагрузки

### Функциональное разбиение по доменам

- Основной домен: vk.com
- Мобильная версия: m.vk.com
- api.vk.com
- Отдача статики: st1-86.vk.com
- Отдача медиаконтента: sun1-55.userapi.com
- Внешняя зависимость (видеоконтент): vkvideo.ru

### Расположение датацентров

Основная аудитория ВКонтакте находится в РФ (88,94%) [^1], следовательно датацентры рационально будет расположить тоже в РФ.

Исходя из карты распределения плотности населения РФ [^19], наибольшая плотность населения наблюдается в европейской части РФ. Предполагаем, что нагрузка больше там, где выше плотность населения (чем больше людей, тем больше среди них пользователей ВКонтакте => больше RPS в этой области). Следовательно наибольшая часть датацентров должны располагаться в европейской части РФ.

[![Population density](img/population.PNG)](https://www.yaklass.ru/p/geografiya/8-klass/naselenie-rossiiskoi-federatcii-6828521/plotnost-i-razmeshchenie-naseleniia-6861455/re-66ba7fe7-4b4f-4a1c-bb65-2b0d3df04898?ysclid=m7sr725fym43469354) [^19]

Обратим внимание на города, которые находятся на пересечении нескольких крупных магистральных сетей связи [^21]. Расположение датацентров в таких городах поможет снизить latency, обеспечить более высокую пропускную способность.

[![Trunk networks](img/trunk_networks.png)](https://www.comnews.ru/content/236040/2024-11-29/2024-w48/1180/magistralnye-seti-svyazi-rossii-2024) [^21]

Месторасположение датацентров:

- Москва (крупнейший город РФ по численности населения => высокая концентрация пользователей. Также может обслуживать небольшой трафик с Белоруссии, Германии)
- Санкт-Петербург (второй крупнейший город РФ по численности населения => высокая концентрация пользователей)
- Ростов-на-Дону (обслуживает юго-западную густозаселенную часть РФ. Также может обслуживать небольшой трафик с Белоруссии, Германии)
- Екатеринбург (Обслуживает центральную часть РФ. Также может обслуживать небольшой трафик с Казахстана)
- Новосибирск (обслуживает восточную часть РФ)

![Data centers](img/data_centers.png)

### Расчет распределения запросов

Исходя из плотности населения и региональной структуры пользователей, распределение нагрузки можно оценить следующим образом:

- Москва: 35%
- Санкт-Петербург: 25%
- Ростов-на-Дону: 15%
- Екатеринбург: 15%
- Новосибирск: 10%

Тогда распределение нагрузки будет следующим:

| Тип запроса                           | Москва, средний RPS | Санкт-Петербург, средний RPS | Ростов-на-Дону, средний RPS | Екатеринбург, средний RPS | Красноярск, средний RPS |
|---------------------------------------|---------------------|------------------------------|-----------------------------|---------------------------|-------------------------|
| Публикация поста от лица пользователя | 144                 | 103                          | 62                          | 62                        | 41                      |
| Публикация поста от лица сообщества   | 610                 | 436                          | 261                         | 261                       | 174                     |       
| Отправка заявки в друзья              | 26                  | 19                           | 11                          | 11                        | 7                       |         
| Запрос на обновление ленты            | 3 078               | 2 199                        | 1 319                       | 1 319                     | 879                     |
| Лайк на пост                          | 4 478               | 3 199                        | 1 919                       | 1 919                     | 1 279                   |    
| Комментарий                           | 170                 | 121                          | 73                          | 73                        | 49                      |       
| Подписка на сообщество                | 26                  | 19                           | 11                          | 11                        | 7                       |       
| Итого                                 | 8 532               | 6 096                        | 3 656                       | 3 656                     | 2 436                   |

### Схема балансировки

Запросы будут распределяться с помощью BGP Anycast. Входящий трафик (vk.com, m.vk.com) → маршрутизируется через BGP Anycast → направляется в ближайший датацентр.

- Все датацентры анонсируют один и тот же IP-адрес в глобальной сети
- Когда пользователь отправляет запрос, его интернет-провайдер определяет маршрут на основе BGP и направляет его в ближайший датацентр
- Если один из датацентров выходит из строя, трафик автоматически перенаправляется в другой ближайший датацентр без участия пользователя

| Регион пользователя    | Ожидаемый датацентр | Резервный датацентр |
|------------------------|---------------------|---------------------|
| Москва и ЦФО	         | Москва              | Санкт-Петербург     |
| Северо-Запад РФ        | Санкт-Петербург     | Москва              |
| Юг России              | Ростов-на-Дону      | Москва              |
| Поволжье, Урал	       | Екатеринбург        | Москва              |
| Сибирь, Дальний Восток | Красноярск          | Екатеринбург        |
| Казахстан	             | Екатеринбург        | Ростов-на-Дону      |
| Беларусь               | Москва              | Санкт-Петербург     |

<a name="sources"></a>
## Список источников

[^1]: [Анализ трафика vk.com от simularweb](https://www.similarweb.com/ru/website/vk.com/#overview)

[^2]: [Исследование аудитории крупнейших социальных сетей в России в 2025 году](https://ppc.world/articles/auditoriya-vosmi-krupneyshih-socsetey-v-rossii-issledovaniya-i-cifry/)

[^3]: [Пост ВК со статистикой за 2024](https://vk.com/wall-22822305_1575041)

[^4]: [Статистика ВКонтакте от inclient](https://inclient.ru/vk-stats/)

[^5]: [Исследование brand analytics](https://vk.com/press/brand-analytics-october-2024)

[^6]: [Исследование Mediascope](https://mediascope.net/upload/iblock/438/37qf2vk4di1n4ncguevk3mufyzb11qfx/Аудитория_социальных_медиа_Mediascope.pdf)

[^7]: [Исследование дружбы ВКонтакте](https://vk.com/press/friends-research)

[^8]: [Итоги 2024 года ВКонтакте: контент](https://m.vk.com/press/content-2024)

[^9]: [Независимое исследование ВКонтакте от «Студии Чижова», LiveDune и TargetHunter](https://dzen.ru/a/Z4931DOF_D_ajSrJ)

[^10]: [Главные тренды потребления контента во ВКонтакте](https://ppc.world/news/glavnye-trendy-potrebleniya-kontenta-vo-vkontakte-issledovanie/)

[^11]: [Исследование трендов ВКонтакте](https://vk.com/press/trends-2024)

[^12]: [Исследование brand analytics](https://brandanalytics.ru/blog/social-media-russia-autumn-2024)

[^13]: [Независимое исследование ВКонтакте от «Студии Чижова», LiveDune и TargetHunter](https://targethunter.ru/blog/bolshoe-nezavisimoe-issledovanie-vkontakte-2024-reklama-ohvaty-vovlechennost/?ysclid=m7c68zp3a6795536690)

[^14]: [Продуктовые итоги ВКонтакте](https://vk.com/main.php?subdir=main.php&subdir=press&subsubdir=products-2022)

[^15]: [О ВКонтакте с официального сайта](https://vk.com/about)

[^16]: [Таблица с анализом ленты ВК](https://docs.google.com/spreadsheets/d/1zFiU8v4MFD6x-sa2T_FB_nZ0zRJVGL7j8tcHc32HvrI/edit?usp=sharing)

[^17]: [Размеры файлов в ВК](https://martrending.ru/smm/razmery-v-vk)

[^18]: [VK. Пресс-релиз по результатам за 3 кв. и 9 мес. 2024](https://vk.company/ru/press/releases/11912/)

[^19]: [Карта плотности населения РФ](https://www.yaklass.ru/p/geografiya/8-klass/naselenie-rossiiskoi-federatcii-6828521/plotnost-i-razmeshchenie-naseleniia-6861455/re-66ba7fe7-4b4f-4a1c-bb65-2b0d3df04898?ysclid=m7sr725fym43469354)

[^20]: [Платформа для мониторинга](https://pr-cy.ru)

[^21]: [Данные о магистральных сетях связи в РФ на 2022 год](https://www.comnews.ru/content/236040/2024-11-29/2024-w48/1180/magistralnye-seti-svyazi-rossii-2024)
