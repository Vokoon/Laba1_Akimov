# Лабораторная Работа №1, по теме "Разработка модели для анализа данных о транспортных средствах с целью оптимизации технического обслуживания и безопасности"
## Суть проекта
Написать код для  работы с данными (Таблице Ексель) о транспортных средствах с целью оптимизации технического обслуживания и безопасности"
 Реализация:
 На основе готовой базы данных транспорта в Таблице Есель, Мы можем работать с его содежанием, узнать краткую информацию о каждом транспорте,  добавить новый транспорт и описание к нему или удалить опр элемент
Таблица Ексель с Базой данных (https://docs.google.com/spreadsheets/d/1AOY39RaiVnOsi12ICJ1PUpsUWVBQ49tg/edit?usp=sharing&ouid=100520035339836256316&rtpof=true&sd=true)
Желательно  скачать, чтобы вы могли проверить работу кода, или можете использовать свои данные.

Для работы нужно имеющийся файл с базой данных техники или для проверки можете использовать этот файл
## Шаги по созданию и использования.
Для начала откройте компилятор для работы к примеру (https://colab.google), можете выбрать и другую но инструкция для КОЛАБА.
Сначла скачайте и импортируйте следующие библиотеки:
```Ruby
import pandas as pd
from openpyxl import load_workbook
!pip install openpyxl
import openpyxl
```
Нужно загрузить файл для работы с ним.
Для загрузки файла, переносим его в это поле.
![image](https://github.com/Vokoon/Laba1_Akimov/assets/120046709/11615305-0946-4884-a06e-f311d9691de2)


Вводим следующее для загрузки и открытия файла в коде.
```Ruby
!wget  -O 'название файла xlsx'
data = pd.read_excel('название файла xlsx')
data
```

```Ruby
```
```Ruby
```
```Ruby
```
```Ruby
```
