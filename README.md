# Лабораторная Работа №1, по теме "Разработка модели для анализа данных о транспортных средствах с целью оптимизации технического обслуживания и безопасности"
## Суть проекта
Написать код для  работы с данными (Таблице Ексель) о транспортных средствах с целью оптимизации технического обслуживания и безопасности"
 Реализация:
 На основе готовой базы данных транспорта в Таблице Есель, Мы можем работать с его содежанием, узнать краткую информацию о каждом транспорте,  добавить новый транспорт и описание к нему или удалить опр элемент
Таблица Ексель с Базой данных (https://docs.google.com/spreadsheets/d/1AOY39RaiVnOsi12ICJ1PUpsUWVBQ49tg/edit?usp=sharing&ouid=100520035339836256316&rtpof=true&sd=true)
Желательно  скачать, чтобы вы могли проверить работу кода, или можете использовать свои данные.

Для работы нужен файл с базой данных техники или для проверки можете использовать этот файл (https://docs.google.com/spreadsheets/d/1AOY39RaiVnOsi12ICJ1PUpsUWVBQ49tg/edit?usp=sharing&ouid=100520035339836256316&rtpof=true&sd=true)
## Шаги по созданию и использования.
-----
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

-----
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

Эти данные можно удалить но для этого нужно использовать библиотеку openpyxl которую мы импортировали в самом начале.
Имейте ввиду после удаления соседняя строка займет собой место удалённой строки.
-----
```Ruby
# Открываем файл Excel
workbook = load_workbook('base_demo.xlsx')

# Выбираем лист, на котором находятся строки для удаления
sheet = workbook['cars-base.ru']  # В данном файле это имя листа если использовали другой файл то имя будет другое.
rows_to_delete = [572,571,179,176,177]  # Список номеров строк, которые нужно удалить

# Удаляем строки
for row_number in sorted(rows_to_delete, reverse=True):
    sheet.delete_rows(row_number)

# Сохраняем изменения
workbook.save('base_new.xlsx')
```
-----
Можем добавить новую строк в имеющуюся таблицу. Для дальнейшей работы советуем выбирать файл "base_new", чтобы полноценно увидеть все изменения.
```Ruby
data2 = load_workbook('base_demo.xlsx') # Это исходная таблица, но можете выбрать 'base_new.xlsx' которую мы создавали для сохранения изменний в предыдущей функции.
sheet = data2.active # Выбираем активный лист
new_row=('AA', 'AA', 'AA', 'Да') #Даём информацию для новой строки, значения могут быть любые, но знайте (,) разделяет значения по столбцам
sheet.append(new_row)
data2.save('base_new.xlsx') #Откройте файл base.xlsx и убедитесь что строка под этим номером пропала и была автоматически заменена соседом рядом
```
-----
Если вы решите внести свои корректировки то можете использовать следующую функцию. Подробности в коде ниже
```Ruby
# Заменяем значения в любой строке и любом столбце
data3 = openpyxl.load_workbook('base_demo.xlsx') #Это исходная таблица, но можете выбрать 'base_new.xlsx'
worksheet = data3['cars-base.ru']
row_index=2 #Указываем строку в котой хотим вносить изменения
worksheet.cell(row=row_index, column=6).value = 'ACE' # с помощбю "column=6" Указываем столбец в которой хотим вносить изменения
data3.save('base_new.xlsx')
```
-----
Можете комплексно убрать строки с определёнными данными на ваш выбор. Ввод ручной.
```Ruby
df = pd.read_excel('base_demo.xlsx') #Это исходная таблица, но можете выбрать 'base_new.xlsx'
value_to_delete = input('Введите элемент: ') #Введите условие по которму функция будет удалять строки
df = df[df[input('Введите Столбец: ')] != value_to_delete] #Введите столбец впределах которого функция будет удалять строки
df.to_excel('base_new.xlsx', index=False)
```
С помощью функции pd.read_excel('base_demo.xlsx') загружается содержимое файла Excel с именем "base_demo.xlsx" в объект DataFrame df. Файл должен находиться в том же каталоге, где выполняется код.

Пользователю предлагается ввести значение, которое будет использоваться для удаления строк из DataFrame. Значение сохраняется в переменную value_to_delete с помощью функции input('Введите элемент: ').

Пользователю также предлагается ввести имя столбца, по которому будет производиться фильтрация. Имя столбца сохраняется в переменную Столбец с помощью функции input('Введите Столбец: ').

С помощью выражения df[df[Столбец] != value_to_delete] создается новый DataFrame, содержащий только те строки из исходного DataFrame df, где значение в столбце Столбец не совпадает со значением value_to_delete.

Новый DataFrame сохраняется в файл Excel с именем "base_new.xlsx" с помощью метода to_excel('base_new.xlsx', index=False). Параметр index=False указывает, что индексы строк не должны быть сохранены в файле.
-----
Если в вашей таблице есть пустые строки и столбцы, то можем это быстро подчистить исползуя следующий метод. Под кодом будут пояснения к нему.
```Ruby
wb = load_workbook('base_demo.xlsx') # Загрузка файла Excel
ws = wb.active  # Выбор активного листа
columns_to_delete = []  # Список для хранения столбцов, которые нужно удалить
for column in range(1, ws.max_column + 1): # Перебор столбцов по индексу (начиная с 1)
    column_values = [cell.value for cell in ws[column] if cell.value] # Проверка, есть ли значения в столбце
    if len(column_values) == 0:
        columns_to_delete.append(column)
for column in reversed(columns_to_delete):# Удаление столбцов, начиная с последнего, чтобы избежать сдвига индексов
    ws.delete_cols(column)

wb.save('base_new.xlsx')
```
Все изменения модно будет увидеть в файле "base_new", если вы не решили поменять названия файла который будет создан для сохранения всех изменений.

-----
# Лабораторная Работа №2 . Создание инструмента для автоматической генерации описаний изображений: использование текстовых данных для описания визуального содержимого

```Ruby
import random
import numpy as np
import torch
import torchvision as tv
import collections
import os
import re

import matplotlib.pyplot as plt
from scipy import ndimage
from scipy import misc
from nltk.translate.bleu_score import corpus_bleu

from tqdm import tqdm
from torch.nn.utils.rnn import pack_padded_sequence
from torchvision import transforms as T
from PIL import Image

import warnings
warnings.filterwarnings("ignore", category=UserWarning)

%matplotlib inline  
!nvidia-smi

# Данная ячейка загружает изображения
#!wget http://images.cocodataset.org/zips/val2014.zip
#!unzip val2014.zip

# Данная ячейка загружает описания к изображениям
#!wget http://images.cocodataset.org/annotations/annotations_trainval2014.zip
#!unzip annotations_trainval2014.zip
```
