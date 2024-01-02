# Лабораторная Работа №1, по теме "Разработка модели для анализа данных о транспортных средствах с целью оптимизации технического обслуживания и безопасности"
## Суть проекта
Написать код для  работы с данными (Таблице Ексель) о транспортных средствах с целью оптимизации технического обслуживания и безопасности"
 Реализация:
 На основе готовой базы данных транспорта в Таблице Есель, Мы можем работать с его содежанием, узнать краткую информацию о каждом транспорте,  добавить новый транспорт и описание к нему или удалить опр элемент
Таблица Ексель с Базой данных (https://docs.google.com/spreadsheets/d/1AOY39RaiVnOsi12ICJ1PUpsUWVBQ49tg/edit?usp=sharing&ouid=100520035339836256316&rtpof=true&sd=true)
Желательно  скачать, чтобы вы могли проверить работу кода, или можете использовать свои данные.

Для работы нужен файл с базой данных техники или для проверки можете использовать этот файл (https://docs.google.com/spreadsheets/d/1AOY39RaiVnOsi12ICJ1PUpsUWVBQ49tg/edit?usp=sharing&ouid=100520035339836256316&rtpof=true&sd=true)
## Шаги по созданию и использования.
Для начала откройте компилятор для работы к примеру (https://colab.google), можете выбрать и другую но инструкция для КОЛАБА.
Сначала вам необходимо  скачайть и импортировать следующие библиотеки:
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
Если вы использовали файл с базой данных предоставленной мной то видите примерно это: 

![image](https://github.com/Vokoon/Laba1_Akimov/assets/120046709/ec0449e8-29d7-4cdd-8f78-ca48a27fad77)

Можем провести проверку есть ли техника вышедшая из эксплуатации или вышел ли его гарантийной срок.
```Ruby
sorted_data_asc = data.sort_values(by="Год начала модели", ascending=True)
sorted_data_asc
```
Если исползовали мой файл с базой данных то увидите следующее: Мы видим строки под номерами (572,571,179,,176,177) это машины у которых на 2023г точно вышел гарантийной срок.

![image](https://github.com/Vokoon/Laba1_Akimov/assets/120046709/bf600f70-85b7-472c-848e-a9a41eed97d3)

Эти данные можно удалить но для этого нужно использовать библиотеку openpyxl которую мы импортировали в самом начале

```Ruby
#Открываем файл Excel
workbook = load_workbook('base_demo.xlsx')

# Выбираем лист, на котором находится строка для удаления
sheet = workbook['cars-base.ru'] #Указываем строку, в данном случае "cars-base.ru"
row_number = 2
sheet.delete_rows(row_number)

# Сохраняем изменения
workbook.save('base_new.xlsx')
```
```Ruby
```
```Ruby
```
