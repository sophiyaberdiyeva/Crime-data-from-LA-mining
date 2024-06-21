Преступность в Лос-Анджелесе
================
Басараб Диана и Бердыева София
2023-11-15

# Знакомство с данными

## “Паспортичка” датасета

Набор данных отражает преступления в Лос-Анджелесе с 2020 года по
настоящее время (выгружены 12.11.2023). Данные были перенесены из
оригинальных протоколов о преступлениях, набранных на бумаге, поэтому в
них могут быть некоторые неточности. Некоторые ячейки с местоположением
с отсутствующими данными отмечены как (0°, 0°).

Описание переменных:

1.  ‘DR_NO’ (Division of Records Number): Официальный номер файла,
    состоящий из двухзначного года, идентификатора района и пяти цифр.

2.  ‘Date Rptd’ (Date Reported): Дата, когда поступило сообщение о
    преступлении

3.  ‘DATE OCC’ (Date of Occurrence): Дата происшествия - MM/DD/YYYY.

4.  ‘TIME OCC’ (Time of Occurrence): Время в 24-часовом формате
    (military time).

5.  ‘AREA’: Лос-Анджелесский полицейский департамент (LAPD) делится на
    21 районный участок, по одному на каждый (географический) район. В
    столбце указаны номера этих районов (с 1 по 21).

6.  ‘AREA NAME’: 21 (географический) район также имеет название,
    относящееся к знаковому объекту или окружающему сообществу, за
    которое он отвечает.

7.  ‘Rpt Dist No’ (Report District Number): Четырехзначный код,
    представляющий подрайон в географическом районе. Все записи о
    преступлениях ссылаются на “RD” - reporting district-ы, где они
    произошли, для статистического сравнения. Список этих дистриктов
    можно найти тут:
    <https://geohub.lacity.org/maps/39b404bd22804807ba0f0e1628e585f2_8/about>

8.  ‘Part.1.2’ **смысл неизвестен**

9.  ‘Crm Cd’ (Crime Code): Код преступления.

10. ‘Crm Cd Desc’ (Crime Code Description): Описание преступления.

11. ‘Mocodes’ (Modus Operandi Codes): Коды действий, связанных с
    подозреваемым в совершении преступления. Список кодов МО в числовом
    порядке можно посмотреть здесь:
    <https://data.lacity.org/api/views/d5tf-ez2w/files/8957b3b1-771a-4686-8f19-281d23a11f1b?download=true&filename=MO_CODES_Numerical_20180627.pdf>

12. ‘Vict Age’ (Victim Age): Возраст пострадавшего (в годах).

13. ‘Vict Sex’ (Victim Sex): F: Женский, M: Мужской, X: Неизвестно.

14. ‘Vict Descent’ (Victim Descent): Происхождение пострадавшего: A -
    Другие азиаты; B - Афроамериканцы; C - Китайцы; D - Камбоджийцы; F -
    Филиппинцы; G - Гуамцы; H - Латиноамериканцы/мексиканцы; I -
    Американские индейцы/эскимосы; J - Японцы; K - Корейцы; L - Лаосцы;
    O - Другие; P - Тихоокеанские островитяне; S - Самоанцы; U -
    Гавайцы; V - Вьетнамцы; W - Белые; X - Неизвестно; Z - Индусы.

15. ‘Premis Cd’ (Premise Code): Код для типа структуры, транспортного
    средства или места, где произошло преступление.

16. ‘Premis Desc’ (Premise Description): Описание соответствующего кода
    ‘Premis Cd’.

17. ‘Weapon Used Cd’ (Weapon Used Code): Тип использованного оружия в
    преступлении.

18. ‘Weapon Desc’ (Weapon Description): Описание использованного оружия

19. ‘Status’ Код статуса дела. (IC используется по умолчанию)

20. ‘Status Desc’ (Status Description): Статус дела.

21. ‘Crm Cd 1’ (Crime Code 1): Указывает на совершенное преступление.
    Код преступления 1 является основным и наиболее серьезным. Коды 2, 3
    и 4 соответственно содержат менее серьезные правонарушения. Более
    низкий класс преступности более серьезен.

22. ‘Crm Cd 2’ (Crime Code 1): Может содержать код дополнительного
    преступления, менее серьезного, чем Код преступления 1.

23. ‘Crm Cd 3’ (Crime Code 1): Может содержать код дополнительного
    преступления, менее серьезного, чем Код преступления 1.

24. ‘Crm Cd 4’ (Crime Code 1): Может содержать код дополнительного
    преступления, менее серьезного, чем Код преступления 1.

25. ‘LOCATION’: Адрес места преступления.

26. ‘Cross Street’: ближайший к адресу перекресток (?)

27. ‘LAT’ (Latitude): Широта места преступления.

28. ‘LON’ (Longitude): Долгота места преступления.

Загрузим датасет в рабочую среду и посмотрим его верхние строки, чтобы
ознакомиться с внешним видом значений. Также посмотрим первоначальный
объем данных в памяти.

``` r
d <- read.csv2("C:/Users/Admin/Documents/СПбГУ/4 курс/7 семестр/Практикум по датамайнингу/Crime_Data_from_2020_to_Present.csv", sep=",")

library(formattable)
#Выводим первые 5 строк
formattable(head(d))
```

<table class="table table-condensed">
<thead>
<tr>
<th style="text-align:right;">
DR_NO
</th>
<th style="text-align:right;">
Date.Rptd
</th>
<th style="text-align:right;">
DATE.OCC
</th>
<th style="text-align:right;">
TIME.OCC
</th>
<th style="text-align:right;">
AREA
</th>
<th style="text-align:right;">
AREA.NAME
</th>
<th style="text-align:right;">
Rpt.Dist.No
</th>
<th style="text-align:right;">
Part.1.2
</th>
<th style="text-align:right;">
Crm.Cd
</th>
<th style="text-align:right;">
Crm.Cd.Desc
</th>
<th style="text-align:right;">
Mocodes
</th>
<th style="text-align:right;">
Vict.Age
</th>
<th style="text-align:right;">
Vict.Sex
</th>
<th style="text-align:right;">
Vict.Descent
</th>
<th style="text-align:right;">
Premis.Cd
</th>
<th style="text-align:right;">
Premis.Desc
</th>
<th style="text-align:right;">
Weapon.Used.Cd
</th>
<th style="text-align:right;">
Weapon.Desc
</th>
<th style="text-align:right;">
Status
</th>
<th style="text-align:right;">
Status.Desc
</th>
<th style="text-align:right;">
Crm.Cd.1
</th>
<th style="text-align:right;">
Crm.Cd.2
</th>
<th style="text-align:right;">
Crm.Cd.3
</th>
<th style="text-align:right;">
Crm.Cd.4
</th>
<th style="text-align:right;">
LOCATION
</th>
<th style="text-align:right;">
Cross.Street
</th>
<th style="text-align:right;">
LAT
</th>
<th style="text-align:right;">
LON
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:right;">
10304468
</td>
<td style="text-align:right;">
01/08/2020 12:00:00 AM
</td>
<td style="text-align:right;">
01/08/2020 12:00:00 AM
</td>
<td style="text-align:right;">
2230
</td>
<td style="text-align:right;">
3
</td>
<td style="text-align:right;">
Southwest
</td>
<td style="text-align:right;">
377
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
624
</td>
<td style="text-align:right;">
BATTERY - SIMPLE ASSAULT
</td>
<td style="text-align:right;">
0444 0913
</td>
<td style="text-align:right;">
36
</td>
<td style="text-align:right;">
F
</td>
<td style="text-align:right;">
B
</td>
<td style="text-align:right;">
501
</td>
<td style="text-align:right;">
SINGLE FAMILY DWELLING
</td>
<td style="text-align:right;">
400
</td>
<td style="text-align:right;">
STRONG-ARM (HANDS, FIST, FEET OR BODILY FORCE)
</td>
<td style="text-align:right;">
AO
</td>
<td style="text-align:right;">
Adult Other
</td>
<td style="text-align:right;">
624
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
1100 W 39TH PL
</td>
<td style="text-align:right;">
</td>
<td style="text-align:right;">
34.0141
</td>
<td style="text-align:right;">
-118.2978
</td>
</tr>
<tr>
<td style="text-align:right;">
190101086
</td>
<td style="text-align:right;">
01/02/2020 12:00:00 AM
</td>
<td style="text-align:right;">
01/01/2020 12:00:00 AM
</td>
<td style="text-align:right;">
330
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
Central
</td>
<td style="text-align:right;">
163
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
624
</td>
<td style="text-align:right;">
BATTERY - SIMPLE ASSAULT
</td>
<td style="text-align:right;">
0416 1822 1414
</td>
<td style="text-align:right;">
25
</td>
<td style="text-align:right;">
M
</td>
<td style="text-align:right;">
H
</td>
<td style="text-align:right;">
102
</td>
<td style="text-align:right;">
SIDEWALK
</td>
<td style="text-align:right;">
500
</td>
<td style="text-align:right;">
UNKNOWN WEAPON/OTHER WEAPON
</td>
<td style="text-align:right;">
IC
</td>
<td style="text-align:right;">
Invest Cont
</td>
<td style="text-align:right;">
624
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
700 S HILL ST
</td>
<td style="text-align:right;">
</td>
<td style="text-align:right;">
34.0459
</td>
<td style="text-align:right;">
-118.2545
</td>
</tr>
<tr>
<td style="text-align:right;">
200110444
</td>
<td style="text-align:right;">
04/14/2020 12:00:00 AM
</td>
<td style="text-align:right;">
02/13/2020 12:00:00 AM
</td>
<td style="text-align:right;">
1200
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
Central
</td>
<td style="text-align:right;">
155
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
845
</td>
<td style="text-align:right;">
SEX OFFENDER REGISTRANT OUT OF COMPLIANCE
</td>
<td style="text-align:right;">
1501
</td>
<td style="text-align:right;">
0
</td>
<td style="text-align:right;">
X
</td>
<td style="text-align:right;">
X
</td>
<td style="text-align:right;">
726
</td>
<td style="text-align:right;">
POLICE FACILITY
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
</td>
<td style="text-align:right;">
AA
</td>
<td style="text-align:right;">
Adult Arrest
</td>
<td style="text-align:right;">
845
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
200 E 6TH ST
</td>
<td style="text-align:right;">
</td>
<td style="text-align:right;">
34.0448
</td>
<td style="text-align:right;">
-118.2474
</td>
</tr>
<tr>
<td style="text-align:right;">
191501505
</td>
<td style="text-align:right;">
01/01/2020 12:00:00 AM
</td>
<td style="text-align:right;">
01/01/2020 12:00:00 AM
</td>
<td style="text-align:right;">
1730
</td>
<td style="text-align:right;">
15
</td>
<td style="text-align:right;">
N Hollywood
</td>
<td style="text-align:right;">
1543
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
745
</td>
<td style="text-align:right;">
VANDALISM - MISDEAMEANOR (\$399 OR UNDER)
</td>
<td style="text-align:right;">
0329 1402
</td>
<td style="text-align:right;">
76
</td>
<td style="text-align:right;">
F
</td>
<td style="text-align:right;">
W
</td>
<td style="text-align:right;">
502
</td>
<td style="text-align:right;">
MULTI-UNIT DWELLING (APARTMENT, DUPLEX, ETC)
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
</td>
<td style="text-align:right;">
IC
</td>
<td style="text-align:right;">
Invest Cont
</td>
<td style="text-align:right;">
745
</td>
<td style="text-align:right;">
998
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
5400 CORTEEN PL
</td>
<td style="text-align:right;">
</td>
<td style="text-align:right;">
34.1685
</td>
<td style="text-align:right;">
-118.4019
</td>
</tr>
<tr>
<td style="text-align:right;">
191921269
</td>
<td style="text-align:right;">
01/01/2020 12:00:00 AM
</td>
<td style="text-align:right;">
01/01/2020 12:00:00 AM
</td>
<td style="text-align:right;">
415
</td>
<td style="text-align:right;">
19
</td>
<td style="text-align:right;">
Mission
</td>
<td style="text-align:right;">
1998
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
740
</td>
<td style="text-align:right;">
VANDALISM - FELONY (\$400 & OVER, ALL CHURCH VANDALISMS)
</td>
<td style="text-align:right;">
0329
</td>
<td style="text-align:right;">
31
</td>
<td style="text-align:right;">
X
</td>
<td style="text-align:right;">
X
</td>
<td style="text-align:right;">
409
</td>
<td style="text-align:right;">
BEAUTY SUPPLY STORE
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
</td>
<td style="text-align:right;">
IC
</td>
<td style="text-align:right;">
Invest Cont
</td>
<td style="text-align:right;">
740
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
14400 TITUS ST
</td>
<td style="text-align:right;">
</td>
<td style="text-align:right;">
34.2198
</td>
<td style="text-align:right;">
-118.4468
</td>
</tr>
<tr>
<td style="text-align:right;">
200100501
</td>
<td style="text-align:right;">
01/02/2020 12:00:00 AM
</td>
<td style="text-align:right;">
01/01/2020 12:00:00 AM
</td>
<td style="text-align:right;">
30
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
Central
</td>
<td style="text-align:right;">
163
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
121
</td>
<td style="text-align:right;">
RAPE, FORCIBLE
</td>
<td style="text-align:right;">
0413 1822 1262 1415
</td>
<td style="text-align:right;">
25
</td>
<td style="text-align:right;">
F
</td>
<td style="text-align:right;">
H
</td>
<td style="text-align:right;">
735
</td>
<td style="text-align:right;">
NIGHT CLUB (OPEN EVENINGS ONLY)
</td>
<td style="text-align:right;">
500
</td>
<td style="text-align:right;">
UNKNOWN WEAPON/OTHER WEAPON
</td>
<td style="text-align:right;">
IC
</td>
<td style="text-align:right;">
Invest Cont
</td>
<td style="text-align:right;">
121
</td>
<td style="text-align:right;">
998
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
700 S BROADWAY
</td>
<td style="text-align:right;">
</td>
<td style="text-align:right;">
34.0452
</td>
<td style="text-align:right;">
-118.2534
</td>
</tr>
</tbody>
</table>

``` r
#Выводим занимаемый данными объем
print(object.size(d),units="MB")
```

    ## 165.9 Mb

Кроме того, посмотрим, какой тип имеют переменные и сколько в каждом из
столбцов пропущенных значений.

``` r
#Информация о переменных
str(d)
```

    ## 'data.frame':    834320 obs. of  28 variables:
    ##  $ DR_NO         : int  10304468 190101086 200110444 191501505 191921269 200100501 200100502 200100504 200100507 201710201 ...
    ##  $ Date.Rptd     : chr  "01/08/2020 12:00:00 AM" "01/02/2020 12:00:00 AM" "04/14/2020 12:00:00 AM" "01/01/2020 12:00:00 AM" ...
    ##  $ DATE.OCC      : chr  "01/08/2020 12:00:00 AM" "01/01/2020 12:00:00 AM" "02/13/2020 12:00:00 AM" "01/01/2020 12:00:00 AM" ...
    ##  $ TIME.OCC      : int  2230 330 1200 1730 415 30 1315 40 200 1925 ...
    ##  $ AREA          : int  3 1 1 15 19 1 1 1 1 17 ...
    ##  $ AREA.NAME     : chr  "Southwest" "Central" "Central" "N Hollywood" ...
    ##  $ Rpt.Dist.No   : int  377 163 155 1543 1998 163 161 155 101 1708 ...
    ##  $ Part.1.2      : int  2 2 2 2 2 1 1 2 1 1 ...
    ##  $ Crm.Cd        : int  624 624 845 745 740 121 442 946 341 341 ...
    ##  $ Crm.Cd.Desc   : chr  "BATTERY - SIMPLE ASSAULT" "BATTERY - SIMPLE ASSAULT" "SEX OFFENDER REGISTRANT OUT OF COMPLIANCE" "VANDALISM - MISDEAMEANOR ($399 OR UNDER)" ...
    ##  $ Mocodes       : chr  "0444 0913" "0416 1822 1414" "1501" "0329 1402" ...
    ##  $ Vict.Age      : int  36 25 0 76 31 25 23 0 23 0 ...
    ##  $ Vict.Sex      : chr  "F" "M" "X" "F" ...
    ##  $ Vict.Descent  : chr  "B" "H" "X" "W" ...
    ##  $ Premis.Cd     : int  501 102 726 502 409 735 404 726 502 203 ...
    ##  $ Premis.Desc   : chr  "SINGLE FAMILY DWELLING" "SIDEWALK" "POLICE FACILITY" "MULTI-UNIT DWELLING (APARTMENT, DUPLEX, ETC)" ...
    ##  $ Weapon.Used.Cd: int  400 500 NA NA NA 500 NA NA NA NA ...
    ##  $ Weapon.Desc   : chr  "STRONG-ARM (HANDS, FIST, FEET OR BODILY FORCE)" "UNKNOWN WEAPON/OTHER WEAPON" "" "" ...
    ##  $ Status        : chr  "AO" "IC" "AA" "IC" ...
    ##  $ Status.Desc   : chr  "Adult Other" "Invest Cont" "Adult Arrest" "Invest Cont" ...
    ##  $ Crm.Cd.1      : int  624 624 845 745 740 121 442 946 341 341 ...
    ##  $ Crm.Cd.2      : int  NA NA NA 998 NA 998 998 998 998 NA ...
    ##  $ Crm.Cd.3      : int  NA NA NA NA NA NA NA NA NA NA ...
    ##  $ Crm.Cd.4      : int  NA NA NA NA NA NA NA NA NA NA ...
    ##  $ LOCATION      : chr  "1100 W  39TH                         PL" "700 S  HILL                         ST" "200 E  6TH                          ST" "5400    CORTEEN                      PL" ...
    ##  $ Cross.Street  : chr  "" "" "" "" ...
    ##  $ LAT           : chr  "34.0141" "34.0459" "34.0448" "34.1685" ...
    ##  $ LON           : chr  "-118.2978" "-118.2545" "-118.2474" "-118.4019" ...

``` r
#Считаем пропущенные значения в столбцах
missing_values <- colSums(is.na(d))
result_table <- data.frame(Column = names(d), Missing_Values = missing_values, row.names = NULL)
formattable(result_table)
```

<table class="table table-condensed">
<thead>
<tr>
<th style="text-align:right;">
Column
</th>
<th style="text-align:right;">
Missing_Values
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:right;">
DR_NO
</td>
<td style="text-align:right;">
0
</td>
</tr>
<tr>
<td style="text-align:right;">
Date.Rptd
</td>
<td style="text-align:right;">
0
</td>
</tr>
<tr>
<td style="text-align:right;">
DATE.OCC
</td>
<td style="text-align:right;">
0
</td>
</tr>
<tr>
<td style="text-align:right;">
TIME.OCC
</td>
<td style="text-align:right;">
0
</td>
</tr>
<tr>
<td style="text-align:right;">
AREA
</td>
<td style="text-align:right;">
0
</td>
</tr>
<tr>
<td style="text-align:right;">
AREA.NAME
</td>
<td style="text-align:right;">
0
</td>
</tr>
<tr>
<td style="text-align:right;">
Rpt.Dist.No
</td>
<td style="text-align:right;">
0
</td>
</tr>
<tr>
<td style="text-align:right;">
Part.1.2
</td>
<td style="text-align:right;">
0
</td>
</tr>
<tr>
<td style="text-align:right;">
Crm.Cd
</td>
<td style="text-align:right;">
0
</td>
</tr>
<tr>
<td style="text-align:right;">
Crm.Cd.Desc
</td>
<td style="text-align:right;">
0
</td>
</tr>
<tr>
<td style="text-align:right;">
Mocodes
</td>
<td style="text-align:right;">
0
</td>
</tr>
<tr>
<td style="text-align:right;">
Vict.Age
</td>
<td style="text-align:right;">
0
</td>
</tr>
<tr>
<td style="text-align:right;">
Vict.Sex
</td>
<td style="text-align:right;">
0
</td>
</tr>
<tr>
<td style="text-align:right;">
Vict.Descent
</td>
<td style="text-align:right;">
0
</td>
</tr>
<tr>
<td style="text-align:right;">
Premis.Cd
</td>
<td style="text-align:right;">
10
</td>
</tr>
<tr>
<td style="text-align:right;">
Premis.Desc
</td>
<td style="text-align:right;">
0
</td>
</tr>
<tr>
<td style="text-align:right;">
Weapon.Used.Cd
</td>
<td style="text-align:right;">
543395
</td>
</tr>
<tr>
<td style="text-align:right;">
Weapon.Desc
</td>
<td style="text-align:right;">
0
</td>
</tr>
<tr>
<td style="text-align:right;">
Status
</td>
<td style="text-align:right;">
0
</td>
</tr>
<tr>
<td style="text-align:right;">
Status.Desc
</td>
<td style="text-align:right;">
0
</td>
</tr>
<tr>
<td style="text-align:right;">
Crm.Cd.1
</td>
<td style="text-align:right;">
10
</td>
</tr>
<tr>
<td style="text-align:right;">
Crm.Cd.2
</td>
<td style="text-align:right;">
772995
</td>
</tr>
<tr>
<td style="text-align:right;">
Crm.Cd.3
</td>
<td style="text-align:right;">
832249
</td>
</tr>
<tr>
<td style="text-align:right;">
Crm.Cd.4
</td>
<td style="text-align:right;">
834259
</td>
</tr>
<tr>
<td style="text-align:right;">
LOCATION
</td>
<td style="text-align:right;">
0
</td>
</tr>
<tr>
<td style="text-align:right;">
Cross.Street
</td>
<td style="text-align:right;">
0
</td>
</tr>
<tr>
<td style="text-align:right;">
LAT
</td>
<td style="text-align:right;">
0
</td>
</tr>
<tr>
<td style="text-align:right;">
LON
</td>
<td style="text-align:right;">
0
</td>
</tr>
</tbody>
</table>

Наблюдаем несколько “некрасивых” фактов:

1.  Названия переменных выглядят не очень удобно

2.  Переменные с датой воспринимаются как строковые - нужно привести к
    соотв. формату. Столбец со временем записан не в едином
    четырехзначном формате.

3.  Переменные с координатами тоже строковые - также необходима
    конвертация в нужный формат

4.  Некоторые столбцы (особенно про дополнительные преступления)
    содержат очень много пропущенных значений. Также пока трудно
    оценивать количество пропущенных значений в столбцах со строковыми
    данными.

5.  Очень много дублирующихся по смыслу или просто бесполезных столбцов

6.  Столбец LOCATION содержит очень много ненужных пробелов

Из благоприятных фактов:

1.  В датафрейме 834320 наблюдений.

2.  Есть геоданные и данные о времени, что расширяет простор для анализа
    примерно в 3 раза.

# Концептуальная основа

## Тема исследования

Мы посмотрим, как лучше предсказать демографические характеристики
потерпевших от преступления “Нарушение спокойствия” - disturbing the
peace.

Данный вид был выбран потому, что вычислительной мощности наших
компьютеров недостаточно для построения моделей с использованием
изначального датасета, а распределение по полу именно в этом виде
преступления является равномерным.

## Вид анализа

1.  Для построения моделей классификации мы будем использовать метод
    кросс-валидаци для настройки гиперпараметров модели, который
    называется “Leave-Group-Out Cross-Validation” (LGOCV). Для обучения
    используем 80% данных на каждой итерации LGOCV. Всего будет 1
    повторение кросс-валидации. Предсказания и вероятность
    принадлежности к классам сохраняются для дальнейшего анализа. В
    качестве метрики оценки модели мы берем Accuracy.
2.  Также для оценки пространственного влияния на предсказание пола
    пострадавшего применяется модель пространственной регрессии с
    применением ковариационной функции Матерна.
3.  Попытаемся спрогнозировать частоту использования оружия в
    преступлениях в ближайшие недели, используя временные ряды.

# Преодобработка

## Устранение изъянов

Постараемся исправить положение дел с “некрасивыми” фактами по очереди

1.  Переименуем переменные

``` r
colnames(d) <- c('dr_no','date_rep','date_occ','time_occ','area','area_name','rep_dis_no','part_1_2','crime_code','crime_desc','mocodes','victim_age', 'victim_sex','victim_descent','premise_cd','premise_desc','weapon_cd','weapon_desc','status','status_desc','crime_cd_1','crime_cd_2','crime_cd_3','crime_cd_4','location','cross_street','lat','lon')
```

2.  Поменяем формат даты и выделим новые переменные - день недели,
    месяц, год.

``` r
#Подключаем пакет для работы с датами
library(lubridate)
#Конвертируем формат
d$date_occ=mdy_hms(d$date_occ)
d$date_rep=mdy_hms(d$date_rep)

#Выделяем новые переменные
d$month=format(as.Date(d$date_occ),'%b')
d$year=format(as.Date(d$date_occ),'%Y')
d$day=format(as.Date(d$date_occ),'%d')
d$day_of_week=format(as.Date(d$date_occ),'%A')
d$month_year=format(as.Date(d$date_occ),'%b %Y')
```

Приведем к надлежащему виду столбец со временем - добавим нули в начало
строки, если она содержит менее 4 знаков, и конвертируем в формат 24
часов

``` r
#Работаем с часами
library(tidyverse)
d <- d %>%
  mutate(time_occ = ifelse(nchar(time_occ) != 4, str_pad(time_occ, width = 4, side = "left", pad = "0"), time_occ))

d$time_occ <- format(strptime(d$time_occ, format = "%H%M"), format = "%H:%M")
```

3.  Конвертируем координаты и посмотрим, сколько пропущенных значений

``` r
library(sp)

# Конвертируем latitude и longitude в numeric
d$lat <- as.double(d$lat)
d$lon <- as.double(d$lon)

nrow(d[is.na(d$lon),])
```

    ## [1] 0

``` r
nrow(d[d$lat==0,])
```

    ## [1] 2263

``` r
nrow(d[d$lon==0,])
```

    ## [1] 2263

Учитывая, что у нас более 834 000 строк, потерять при анализе 2263 будет
не катастрофично

4.  Продолжим работу с пропущенными значениями.

Удалим все переменные про другие преступления того же “авторства”, кроме
первого (crime_cd_1 - там всего 10 пропущенных), - они сильно разрежают
матрицу.

``` r
d <- subset(d, select = - c(crime_cd_2,crime_cd_3,crime_cd_4))
```

С переменными про использованное оружие поступим так: создадим новый
столбец weapon_used, который будет содержать значения 1, если оружие
применялось, и 0 - если нет (на основе того, пропущено ли значение в
столбце weapon_cd). Переменную с указанием вида оружия (weapon_desc)
факторизуем, а с кодом оружия (weapon_cd) - удалим.

``` r
d$weapon_used <- ifelse(is.na(d$weapon_cd),0,1)

d$weapon_desc[nchar(d$weapon_desc)==0] <- NA
d$weapon_desc <- factor(d$weapon_desc)

d <- subset(d, select = - c(weapon_cd))
```

Посмотрим внимательней на переменную возраста жертвы

``` r
table(d$victim_age)
```

    ## 
    ##     -3     -2     -1      0      2      3      4      5      6      7      8 
    ##      1     13     58 206335    367    437    442    508    507    508    524 
    ##      9     10     11     12     13     14     15     16     17     18     19 
    ##    601    698   1057   1561   2133   2554   3070   3451   3727   5223   8699 
    ##     20     21     22     23     24     25     26     27     28     29     30 
    ##  10483  12445  13931  13663  15354  16319  16528  17178  17894  18153  19021 
    ##     31     32     33     34     35     36     37     38     39     40     41 
    ##  18217  17697  17218  16420  18620  15480  14808  14467  13827  13598  12733 
    ##     42     43     44     45     46     47     48     49     50     51     52 
    ##  11889  11718  11079  10829  10076  10100   9513   9484  10910   9428   9137 
    ##     53     54     55     56     57     58     59     60     61     62     63 
    ##   8905   8504   8294   7799   7704   7398   7139   6930   6394   6088   5760 
    ##     64     65     66     67     68     69     70     71     72     73     74 
    ##   5410   4941   4572   4071   3618   3227   2998   2722   2566   2361   2046 
    ##     75     76     77     78     79     80     81     82     83     84     85 
    ##   1723   1615   1420   1277   1070    991    823    790    688    515    527 
    ##     86     87     88     89     90     91     92     93     94     95     96 
    ##    441    332    303    263    239    205    155    112     93     80     84 
    ##     97     98     99    120 
    ##     62     65    308      1

Очевидно, возраст не может быть отрицательным, и не могло быть так много
жертв среди младенцев - при отутствии данных писали “0”. Также можно
заметить, что в других переменных про потерпевших (victim_sex и
victim_descent) нужно заменить “X” и прочие обозначения на NA.

``` r
d$victim_age[d$victim_age %in% c(-3, -2, -1, 0)] <- NA

table(d$victim_sex)
```

    ## 
    ##             -      F      H      M      X 
    ## 109888      1 307149     91 344140  73051

``` r
d$victim_sex[d$victim_sex %in% c("X", "H", "-")] <- NA

table(d$victim_descent)
```

    ## 
    ##             -      A      B      C      D      F      G      H      I      J 
    ## 109896      2  18274 118704   3216     64   3475     59 255888    783   1155 
    ##      K      L      O      P      S      U      V      W      X      Z 
    ##   4453     50  66113    224     46    167    867 169802  80668    414

``` r
d$victim_descent[d$victim_descent %in% c("X", "-")] <- NA
```

Также внимание надо уделить географическим пропущенным данным - сейчас
там стоят “0”.

``` r
d$lat[d$lat==0] <- NA
d$lat[d$lon==0] <- NA
```

5.  Удалим бесполезные столбцы и факторизуем полезные строковые
    переменные.

``` r
d <- subset(d, select = - c(dr_no, area, part_1_2, crime_code, premise_cd, status,cross_street))
d$area_name <- factor(d$area_name)
d$crime_desc <- factor(d$crime_desc)

d$victim_sex[nchar(d$victim_sex)==0] <- NA
d$victim_sex <- factor(d$victim_sex)

d$victim_descent[nchar(d$victim_descent)==0] <- NA
d$victim_descent <- factor(d$victim_descent)

d$premise_desc[nchar(d$premise_desc)==0] <- NA
d$premise_desc <- factor(d$premise_desc)

d$status_desc[d$status_desc=="UNK"] <- NA
d$status_desc <- factor(d$status_desc)

d$crime_cd_1 <- factor(d$crime_cd_1)
d$rep_dis_no <- factor(d$rep_dis_no)
```

Особое внимание уделим столбцу mocodes с дополнительной информацией о
деле. Обработаем их так, чтобы выявить самые часто встречающиеся коды, и
вынесем их в отдельные бинарные переменные.

``` r
#Расчет самых популярных кодов
library(dplyr)

# Выделяем коды в отдельные строки и "свертываем" по частоте встречаемости
d_codes <- d %>%
  tidyr::separate_rows(mocodes, sep = " ") %>%
  dplyr::group_by(mocodes) %>%
  dplyr::summarize(count = n()) %>%
  dplyr::arrange(dplyr::desc(count))

# Выводим топ самых встречающихся
head(d_codes, 7)
```

    ## # A tibble: 7 × 2
    ##   mocodes  count
    ##   <chr>    <int>
    ## 1 "1822"  285999
    ## 2 "0344"  245571
    ## 3 "0913"  135413
    ## 4 ""      115576
    ## 5 "0329"  110447
    ## 6 "0416"  108146
    ## 7 "1300"   81550

Показанным кодам соответствуют следующие значения (напомним, что их
можно посмотреть тут:
<https://data.lacity.org/api/views/d5tf-ez2w/files/8957b3b1-771a-4686-8f19-281d23a11f1b?download=true&filename=MO_CODES_Numerical_20180627.pdf>)
:

1822 - Stranger - жертва не была знакома с подозреваемым (?)

0344 - Removes vict property - имущество жертвы убрали

0329 - Vandalized - произошел погром

0416 - Hit-Hit w/ weapon - вероятно, перестрелка с оружием

1300 - Vehicle involved - в преступлении задействовали транспортное
средство

``` r
#Добавим бинарные переменные
d$stranger <- as.numeric(grepl("1822", d$mocodes))
d$rm_prop <- as.numeric(grepl("0344", d$mocodes))
d$vandalized <- as.numeric(grepl("0329", d$mocodes))
d$hh_wpn <- as.numeric(grepl("0416", d$mocodes))
d$veh_inv <- as.numeric(grepl("1300", d$mocodes))

#Удалим столбец с исходными кодами о деталях
d <- subset(d, select = - mocodes)
```

6.  Для переменной с локацией воспользуемся функцией, превращающей все
    ненужные пробелы в один нужный, и тоже факторизуем ее

``` r
d$location=str_squish(d$location)
d$location=factor(d$location)
```

Посмотрим на объем после преобразований

``` r
print(object.size(d),units="MB")
```

    ## 141.9 Mb

## Подготовка датафрейма преступлений вида “DISTURBING THE PEACE”

Для построения моделей мы выбираем следующие переменные: 1.
‘victim_age’: Возраст пострадавшего 2. ‘victim_sex’: Пол пострадавшего
3. ‘victim_descent’: Происхождение пострадавшего 4. ‘status_desc’:
Статус дела 5. ‘month’: Месяц происшествия 6. ‘year’: Год происшествия
7. ‘day_of_week’: День недели происшествия 8. ‘weapon_used’: Применение
оружия 9. ‘stranger’: Жертва не знает подозреваемого 10. ‘rm_prop’:
Кража имущества 11. ‘vandalized’: Погром 12. ‘hh_wpn’: Перестрелка с
оружием 13. ‘veh_inv’: Задействование транспортного средства

``` r
table(d$victim_sex[d$crime_desc=="DISTURBING THE PEACE"])  
```

    ## 
    ##   F   M 
    ## 632 658

``` r
library(dplyr)

d_sf=d[d$crime_desc=="DISTURBING THE PEACE"&(d$victim_sex=="F"|d$victim_sex=="M"),-c(1,2,3,4,5,6,10,11,13,14, 15,16,19,21)]
d_sf=na.omit(d_sf)
d_sf[,-1] <- d_sf[,-1] %>%
  mutate_all(factor)
```

## Визуализация данных по нарушению тишины и спокойствия граждан

Как и было отмечено, распределение пола стремится к равномерному. Самая
многочисленная группа пострадавших от нарушения тишины и покоя - белые.
В ноябре и декабре зафиксированных происшествий меньше, чем в другие
месяцы. Это можно связать с проведением различных мероприятий,
посвященных Хеллоуину и Рождеству. Возможно, людям скучно или им не
нравится их скучная жизнь, поэтому в другие месяцы поступает больше
обращений. По годам выбивается только 22 год. Возможно, шумные вечеринки
по окончанию COVID не были радостно приняты окружающими. В распределении
по дням недели ничего интересного. Минимальное число происшествий было с
применением оружия или перестрелкой, кражей имущества, погромом и с
использованием транспортного средства.

``` r
ggplot(d_sf, aes(x = victim_age)) +
  geom_histogram(binwidth = 5, fill = "skyblue", color = "darkgray") +
  labs(title = "Распределение возраста пострадавших", x = "Возраст", y = "Частота")
```

![](Crime_data_project_Basarab_Berdiyeva_github_files/figure-gfm/unnamed-chunk-18-1.png)<!-- -->

``` r
ggplot(d_sf, aes(x = victim_sex)) + geom_bar(fill = "skyblue") + labs(title = "Распределение по полу пострадавших", x = "Пол", y = "Частота")
```

![](Crime_data_project_Basarab_Berdiyeva_github_files/figure-gfm/unnamed-chunk-18-2.png)<!-- -->

``` r
ggplot(d_sf, aes(x = victim_descent)) + geom_bar(fill = "skyblue") + labs(title = "Распределение по происхождению пострадавших", x = "Происхождение", y = "Частота")
```

![](Crime_data_project_Basarab_Berdiyeva_github_files/figure-gfm/unnamed-chunk-18-3.png)<!-- -->

``` r
ggplot(d_sf, aes(x = status_desc)) + geom_bar(fill = "skyblue") + labs(title = "Распределение статуса дела", x = "Статус", y = "Частота")
```

![](Crime_data_project_Basarab_Berdiyeva_github_files/figure-gfm/unnamed-chunk-18-4.png)<!-- -->

``` r
ggplot(d_sf, aes(x = month)) + geom_bar(fill = "skyblue") + labs(title = "Распределение по месяцу происшествия", x = "Месяц", y = "Частота")
```

![](Crime_data_project_Basarab_Berdiyeva_github_files/figure-gfm/unnamed-chunk-18-5.png)<!-- -->

``` r
ggplot(d_sf, aes(x = year)) + geom_bar(fill = "skyblue") + labs(title = "Распределение по году происшествия", x = "Год", y = "Частота")
```

![](Crime_data_project_Basarab_Berdiyeva_github_files/figure-gfm/unnamed-chunk-18-6.png)<!-- -->

``` r
ggplot(d_sf, aes(x = day_of_week)) + geom_bar(fill = "skyblue") + labs(title = "Распределение по дню недели происшествия", x = "День недели", y = "Частота")
```

![](Crime_data_project_Basarab_Berdiyeva_github_files/figure-gfm/unnamed-chunk-18-7.png)<!-- -->

``` r
ggplot(d_sf, aes(x = weapon_used)) + geom_bar(fill = "skyblue") + labs(title = "Распределение применения оружия", x = "Оружие", y = "Частота")
```

![](Crime_data_project_Basarab_Berdiyeva_github_files/figure-gfm/unnamed-chunk-18-8.png)<!-- -->

``` r
ggplot(d_sf, aes(x = stranger)) + geom_bar(fill = "skyblue") + labs(title = "Распределение по знанию пострадавшим подозреваемого", x = "Знание пострадавшим подозреваемого", y = "Частота")
```

![](Crime_data_project_Basarab_Berdiyeva_github_files/figure-gfm/unnamed-chunk-18-9.png)<!-- -->

``` r
ggplot(d_sf, aes(x = rm_prop)) + geom_bar(fill = "skyblue") + labs(title = "Распределение кражи имущества", x = "Кража имущества", y = "Частота")
```

![](Crime_data_project_Basarab_Berdiyeva_github_files/figure-gfm/unnamed-chunk-18-10.png)<!-- -->

``` r
ggplot(d_sf, aes(x = vandalized)) + geom_bar(fill = "skyblue") + labs(title = "Распределение по фактам погрома", x = "Погром", y = "Частота")
```

![](Crime_data_project_Basarab_Berdiyeva_github_files/figure-gfm/unnamed-chunk-18-11.png)<!-- -->

``` r
ggplot(d_sf, aes(x = hh_wpn)) + geom_bar(fill = "skyblue") + labs(title = "Распределение по перестрелке с оружием", x = "Перестрелка с оружием", y = "Частота")
```

![](Crime_data_project_Basarab_Berdiyeva_github_files/figure-gfm/unnamed-chunk-18-12.png)<!-- -->

``` r
ggplot(d_sf, aes(x = veh_inv)) + geom_bar(fill = "skyblue") + labs(title = "Распределение по задействованию транспортного средства", x = "Задействование транспорта", y = "Частота")
```

![](Crime_data_project_Basarab_Berdiyeva_github_files/figure-gfm/unnamed-chunk-18-13.png)<!-- -->

## Дополнительная предобработка данных по нарушению спокойствия

Визуализации показали, что в некоторых переменных часть факторов имеет
очень малое число наблюдений: национальность пострадавшего, статус дела
(почти нет задержанных детей), и факты кражи имущества, погрома,
перестрелки и использования транспортных средств. Уберем строки с
малочисленными значениями факторов или полностью столбцы в случае
бинарных переменных.

``` r
d_sf=d_sf[(d_sf$victim_descent!="A"&d_sf$victim_descent!="K")&(d_sf$status_desc!="Juv Arrest"&d_sf$status_desc!="Juv Other"),-c(10,11,12,13)]

#Обновим факторы
d_sf$victim_descent <- factor(d_sf$victim_descent)
d_sf$status_desc <- factor(d_sf$status_desc)
```

# Датамайнинг

## Предсказание пола жертв преступления “DISTURBING THE PEACE” - нарушения спокойствия

``` r
library(caret)
metric = 'Accuracy'
set.seed(42)
control = trainControl(method = "LGOCV", p = 0.8, number = 1,
                       savePredictions = T, classProbs = TRUE)

#Создаем таблицу для записи результатов
res_sx =data.frame(mod = character(), Accuracy = numeric())


# Логистическая регрессия 
sx_fit.glm <- train(victim_sex ~ ., data=d_sf, method = "glm", metric = metric, preProc = c("center", "scale"), trControl = control, family="binomial")
res_sx = rbind(res_sx, data.frame(mod = 'Logistic Regression', Accuracy = sx_fit.glm$results$Accuracy))

# Partial Least Squares
sx_fit.pls <- train(victim_sex ~ ., data=d_sf, method = "pls", metric = metric, preProc = c("center", "scale"), trControl = control) 
res_sx = rbind(res_sx, data.frame(mod = 'Partial Least Squares', Accuracy = max(sx_fit.pls$results$Accuracy))) 

# GLMNET
tunegrid <- expand.grid(.alpha=seq(0,1,by=0.1), .lambda=c(1e-1, 1e-2, 1e-3, 1e-4, 1e-5, 1e-6)) 
sx_fit.glmnet <- train(victim_sex~., data=d_sf, method="glmnet", metric=metric, tuneGrid=tunegrid, preProc=c("center", "scale"), trControl=control)
res_sx =rbind(res_sx, data.frame(mod='GLMNET', Accuracy=max(sx_fit.glmnet$results$Accuracy)))


# Nearest Shrunken Centroids 
tunegrid <- expand.grid(.threshold=seq(0,1,by=0.1)) 
sx_fit.pam <- train(victim_sex~., data=d_sf, method="pam", metric=metric, tuneGrid=tunegrid, preProc=c("center", "scale"), trControl=control) 
res_sx =rbind(res_sx, data.frame(mod='Nearest Shrunken Centroids', Accuracy=max(sx_fit.pam$results$Accuracy)))

# Neural net
tunegrid <- expand.grid(.size=seq(1:10), .decay=c(0, .1, 1, 2)) 
maxSize <- max(tunegrid$.size) 
numWeights <- 1*(maxSize * (length(d) + 1) + maxSize + 1) 
maxit <- 2000 
sx_fit.nnet <- train(victim_sex~., data=d_sf, method="nnet", metric=metric, tuneGrid=tunegrid, preProc=c("center", "scale", "spatialSign"), trControl=control, trace=FALSE, maxit=maxit, MaxNWts=numWeights) 
res_sx =rbind(res_sx, data.frame(mod='Neural net', Accuracy=max(sx_fit.nnet$results$Accuracy[is.finite(sx_fit.nnet$results$Accuracy)])))

# FDA
sx_fit.fda <- train(victim_sex~., data=d_sf, method="fda", metric=metric, preProc=c("center", "scale"), trControl=control) 
res_sx =rbind(res_sx, data.frame(mod='FDA', Accuracy = max(sx_fit.fda$results$Accuracy)))

#k-nearest neighbors
tunegrid <- expand.grid(.k=c(4*(0:5)+1, 20*(1:5)+1, 50*(2:9)+1)) 
sx_fit.knn <- train(victim_sex~., data=d_sf, method="knn", metric=metric, tuneGrid=tunegrid,                   preProc=c("center", "scale"), trControl=control) 
res_sx = rbind(res_sx, data.frame(mod='k-nearest neighbors', Accuracy = max(sx_fit.knn$results$Accuracy))) 

# knn 2 версия
sx_fit.knn2 <- train(victim_sex ~ ., data=d_sf, method = "knn", 
                  tuneGrid = expand.grid(k = 1:30), 
                  metric = metric,
                  trControl = control)
res_sx = rbind(res_sx,data.frame(mod = "k-nearest neighbors 1-30", Accuracy = max(sx_fit.knn2$results$Accuracy)))  


# Learning Vector Quantization
sx_fit.lvq <- train(victim_sex~., data=d_sf, method="lvq", metric=metric, trControl=control)
res_sx =rbind(res_sx, data.frame(mod='Learning Vector Quantization', Accuracy=max(sx_fit.lvq$results$Accuracy)))

# Recursive Partitioning and Regression Trees
tunegrid <- expand.grid(.cp=seq(0,0.1,by=0.01)) 
sx_fit.cart <- train(victim_sex~., data=d_sf, method="rpart", metric=metric, tuneGrid=tunegrid, trControl=control) 
res_sx =rbind(res_sx, data.frame(mod='Recursive Partitioning and Regression Trees seq(0,0.1,by=0.01)', Accuracy=max(sx_fit.cart$results$Accuracy)))

# Recursive Partitioning and Regression Trees как делали в классе
sx_fit.rpart2 <- train(victim_sex ~ ., data=d_sf, method = "rpart", 
                    tuneGrid = expand.grid(cp = seq(0, 0.1, 0.001)),
                    metric = metric,
                    trControl = control)

res_sx = rbind(res_sx, data.frame(mod = 'Recursive Partitioning and Regression Trees seq(0, 0.1, 0.001)', Accuracy = max(sx_fit.rpart2$results$Accuracy)))

# Logistic Model Trees 
sx_fit.LMT <- train(victim_sex~., data=d_sf, method="LMT", metric=metric, trControl=control) 
res_sx =rbind(res_sx, data.frame(mod='Logistic Model Trees', Accuracy=max(sx_fit.LMT$results$Accuracy)))

# PART Rule-Based Classifier 
sx_fit.part <- train(victim_sex~., data=d_sf, method="PART", metric=metric, trControl=control) 
res_sx =rbind(res_sx, data.frame(mod='PART Rule-Based Classifier', Accuracy=max(sx_fit.part$results$Accuracy)))

# Rule-Based Classifier 
sx_fit.JRIP <- train(victim_sex~., data=d_sf, method="JRip", metric=metric, trControl=control) 
res_sx =rbind(res_sx, data.frame(mod='Rule-Based Classifier', Accuracy=max(sx_fit.JRIP$results$Accuracy)))

# Boosted Linear Model 
sx_fit.BstLm <- train(victim_sex~., data=d_sf, method="BstLm", metric=metric, trControl=control)
res_sx = rbind(res_sx, data.frame(mod='Boosted Linear Model', Accuracy=max(sx_fit.BstLm$results$Accuracy)))

# Boosted Logistic Regression 
library(caTools)
sx_fit.LogitBoost <- train(victim_sex~., data=d_sf, method="LogitBoost", metric=metric, trControl=control) 
res_sx = rbind(res_sx, data.frame(mod='Boosted Logistic Regression', Accuracy=max(sx_fit.LogitBoost$results$Accuracy)))


#'Cost-Sensitive C5.0 
sx_fit.C5.0Cost <- train(victim_sex~., data=d_sf, method="C5.0Cost", metric=metric, trControl=control) 
res_sx =rbind(res_sx, data.frame(mod='Cost-Sensitive C5.0', Accuracy = max(sx_fit.C5.0Cost$results$Accuracy)))

#eXtreme Gradient Boosting 
sx_fit.xgbLinear <- train(victim_sex ~., data=d_sf, method="xgbLinear", metric=metric, trControl=control) 
res_sx =rbind(res_sx, data.frame(mod='eXtreme Gradient Boosting', Accuracy=max(sx_fit.xgbLinear$results$Accuracy)))

#eXtreme Gradient Boosting2
sx_fit.xgbTree <- train(victim_sex ~., data=d_sf, method="xgbTree", metric=metric, trControl=control) 
res_sx =rbind(res_sx, data.frame(mod='eXtreme Gradient Boosting2', Accuracy=max(sx_fit.xgbTree$results$Accuracy)))

#Stochastic Gradient Boosting 
tunegrid <- expand.grid(.n.trees=c(5, 100, 500), .interaction.depth=c(1, 3, 5, 7, 9), .shrinkage=c(0, 1e-1, 1e-2, 1e-3, 1e-4), .n.minobsinnode=c(5, 10)) 
sx_fit.gbm <- train(victim_sex~., data=d_sf, method="gbm", metric=metric, tuneGrid=tunegrid, trControl=control, verbose=FALSE) 
res_sx =rbind(res_sx, data.frame(mod='Stochastic Gradient Boosting', Accuracy=max(sx_fit.gbm$results$Accuracy)))

# Bagged CART  
sx_fit.treebag <- train(victim_sex~., data=d_sf, method="treebag", metric=metric, trControl=control)
res_sx =rbind(res_sx, data.frame(mod='Bagged CART', Accuracy=max(sx_fit.treebag$results$Accuracy))) 

# Bagged Flexible Discriminant Analysis 
sx_fit.bagFDA <- train(victim_sex~., data=d_sf, method="bagFDA", metric=metric, trControl=control) 
res_sx =rbind(res_sx, data.frame(mod='Bagged Flexible Discriminant Analysis', Accuracy = max(sx_fit.bagFDA$results$Accuracy)))

# Bagged MARS using gCV Pruning 
library(earth)
sx_fit.bagEarthGCV <- train(victim_sex~., data=d_sf, method="bagEarthGCV", metric=metric, trControl=control) 
res_sx = rbind(res_sx, data.frame(mod='Bagged MARS', Accuracy=max(sx_fit.bagEarthGCV$results$Accuracy)))

# Bagged MARS 
sx_fit.bagEarth <- train(victim_sex~., data=d_sf, method="bagEarth", metric=metric, trControl=control) 
res_sx = rbind(res_sx, data.frame(mod='Bagged MARS using gCV Pruning', Accuracy=max(sx_fit.bagEarth$results$Accuracy)))

# Conditional Inference Random Forest  
sx_fit.cforest <- train(victim_sex~., data=d_sf, method="cforest", metric=metric, trControl=control)
res_sx =rbind(res_sx, data.frame(mod='Conditional Inference Random Forest', Accuracy=max(sx_fit.cforest$results$Accuracy))) 

#Model Averaged Neural Network 
sx_fit.avNNet <- train(victim_sex~., data=d_sf, method="avNNet", metric=metric, trControl=control)  
res_sx =rbind(res_sx, data.frame(mod='Model Averaged Neural Network', Accuracy=max(sx_fit.avNNet$results$Accuracy)))

#Parallel Random Forest
sx_fit.parRF <- train(victim_sex~., data=d_sf, method="parRF", metric=metric, trControl=control)  
res_sx =rbind(res_sx, data.frame(mod='Parallel Random Forest', Accuracy=max(sx_fit.parRF$results$Accuracy)))

# Random Ferns 
sx_fit.rFerns <- train(victim_sex~., data=d_sf, method="rFerns", metric=metric, trControl=control)  
res_sx =rbind(res_sx, data.frame(mod='Random Ferns', Accuracy=max(sx_fit.rFerns$results$Accuracy)))

# Random Forest 
sx_fit.ranger <- train(victim_sex~., data=d_sf, method="ranger", metric=metric, trControl=control) 
res_sx =rbind(res_sx, data.frame(mod='Random Forest', Accuracy=max(sx_fit.ranger$results$Accuracy)))

# Random Forest (classical) 
sx_fit.rf <- train(victim_sex ~ ., data=d_sf, method = "rf", metric = metric, trControl = control) 
res_sx = rbind(res_sx, data.frame(mod = 'Random Forest (classical)', Accuracy = max(sx_fit.rf$results$Accuracy)))

# Random Forest Rule-Based Model 
sx_fit.rfRules <- train(victim_sex~., data=d_sf, method="rfRules", metric=metric, trControl=control)
res_sx = rbind(res_sx, data.frame(mod='Random Forest Rule-Based Model', Accuracy=max(sx_fit.rfRules$results$Accuracy)))

# Regularized Random Forest
sx_fit.RRF <- train(victim_sex~., data=d_sf, method="RRF", metric=metric, trControl=control) 
res_sx = rbind(res_sx, data.frame(mod='Regularized Random Forest', Accuracy=max(sx_fit.RRF$results$Accuracy)))

# Regularized Random Forest (другой) 
sx_fit.RRFglobal <- train(victim_sex~., data=d_sf, method="RRFglobal", metric=metric, trControl=control) 
res_sx = rbind(res_sx, data.frame(mod='Regularized Random Forest (другой)', Accuracy=max(sx_fit.RRFglobal$results$Accuracy)))

# Weighted Subspace Random Forest
sx_fit.wsrf <- train(victim_sex~., data=d_sf, method="wsrf", metric=metric, trControl=control) 
res_sx = rbind(res_sx, data.frame(mod='Weighted Subspace Random Forest', Accuracy=max(sx_fit.wsrf$results$Accuracy)))
```

``` r
#Выведем максимальное аккураси
res_sx[which.max(res_sx$Accuracy), ]
```

    ##                   mod Accuracy
    ## 1 Logistic Regression 0.623431

``` r
library(formattable)  

color_scale <- color_tile("white", "lightblue")
res_sx$Accuracy <- color_scale(res_sx$Accuracy)

formattable(res_sx[order(res_sx$Accuracy, decreasing = FALSE), ], align="l")
```

<table class="table table-condensed">
<thead>
<tr>
<th style="text-align:left;">
</th>
<th style="text-align:left;">
mod
</th>
<th style="text-align:left;">
Accuracy
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
1
</td>
<td style="text-align:left;">
Logistic Regression
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #add8e6">0.6234310</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
17
</td>
<td style="text-align:left;">
Cost-Sensitive C5.0
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #b0d9e6">0.6150628</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
33
</td>
<td style="text-align:left;">
Regularized Random Forest (другой)
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #b0d9e6">0.6150628</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
20
</td>
<td style="text-align:left;">
Stochastic Gradient Boosting
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #b3dbe7">0.6066946</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
6
</td>
<td style="text-align:left;">
FDA
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #b4dbe8">0.6025105</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
8
</td>
<td style="text-align:left;">
k-nearest neighbors 1-30
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #b6dce8">0.5983264</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
13
</td>
<td style="text-align:left;">
PART Rule-Based Classifier
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #b6dce8">0.5983264</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
3
</td>
<td style="text-align:left;">
GLMNET
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #b8dde9">0.5941423</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
5
</td>
<td style="text-align:left;">
Neural net
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #b8dde9">0.5941423</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
19
</td>
<td style="text-align:left;">
eXtreme Gradient Boosting2
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #b8dde9">0.5941423</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
28
</td>
<td style="text-align:left;">
Random Ferns
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #b8dde9">0.5941423</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
4
</td>
<td style="text-align:left;">
Nearest Shrunken Centroids
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #b9dee9">0.5899582</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
18
</td>
<td style="text-align:left;">
eXtreme Gradient Boosting
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #b9dee9">0.5899582</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
22
</td>
<td style="text-align:left;">
Bagged Flexible Discriminant Analysis
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #bcdfea">0.5815900</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
26
</td>
<td style="text-align:left;">
Model Averaged Neural Network
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #bcdfea">0.5815900</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
27
</td>
<td style="text-align:left;">
Parallel Random Forest
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #bcdfea">0.5815900</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
34
</td>
<td style="text-align:left;">
Weighted Subspace Random Forest
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #bee0eb">0.5774059</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
25
</td>
<td style="text-align:left;">
Conditional Inference Random Forest
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #bfe1eb">0.5732218</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
32
</td>
<td style="text-align:left;">
Regularized Random Forest
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #bfe1eb">0.5732218</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
7
</td>
<td style="text-align:left;">
k-nearest neighbors
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #c1e1ec">0.5690377</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
11
</td>
<td style="text-align:left;">
Recursive Partitioning and Regression Trees seq(0, 0.1, 0.001)
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #c1e1ec">0.5690377</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
14
</td>
<td style="text-align:left;">
Rule-Based Classifier
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #c1e1ec">0.5690377</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
30
</td>
<td style="text-align:left;">
Random Forest (classical)
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #c1e1ec">0.5690377</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
2
</td>
<td style="text-align:left;">
Partial Least Squares
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #c3e2ec">0.5648536</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
21
</td>
<td style="text-align:left;">
Bagged CART
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #c6e4ed">0.5564854</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
29
</td>
<td style="text-align:left;">
Random Forest
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #cae6ef">0.5439331</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
10
</td>
<td style="text-align:left;">
Recursive Partitioning and Regression Trees seq(0,0.1,by=0.01)
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #cce7ef">0.5397490</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
31
</td>
<td style="text-align:left;">
Random Forest Rule-Based Model
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #cfe8f0">0.5313808</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
9
</td>
<td style="text-align:left;">
Learning Vector Quantization
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #d2eaf1">0.5230126</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
12
</td>
<td style="text-align:left;">
Logistic Model Trees
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #d2eaf1">0.5230126</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
16
</td>
<td style="text-align:left;">
Boosted Logistic Regression
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #d7ecf2">0.5104603</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
15
</td>
<td style="text-align:left;">
Boosted Linear Model
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #dceef4">0.4979079</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
24
</td>
<td style="text-align:left;">
Bagged MARS using gCV Pruning
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #f8fcfd">0.4225941</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
23
</td>
<td style="text-align:left;">
Bagged MARS
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #ffffff">0.4058577</span>
</td>
</tr>
</tbody>
</table>

### Доработка моделей для предсказания пола

В одном из прогонов победили модели Nearest Shrunken Centroids, Neural
Net и k-nearest neighbors. Ожидаем, что похожие результаты будут и при
других.

#### Nearest Shrunken Centroids

Настраиваемый параметр этой модели - threshold.

``` r
plot(sx_fit.pam)
```

![](Crime_data_project_Basarab_Berdiyeva_github_files/figure-gfm/unnamed-chunk-22-1.png)<!-- -->

``` r
sx_fit.pam$bestTune$threshold
```

    ## [1] 0

``` r
#при погонке выходило "0", поэтому в дальнейшем решили просто тюнить с большим дроблением


# Nearest Shrunken Centroids 
tunegrid <- expand.grid(.threshold=seq(0,1,by=0.0001)) 
sx_fit.pam_tuned <- train(victim_sex~., data=d_sf, method="pam", metric=metric, tuneGrid=tunegrid, preProc=c("center", "scale"), trControl=control) 
```

    ## 11

``` r
Accuracy=max(sx_fit.pam_tuned$results$Accuracy)
Accuracy
```

    ## [1] 0.5690377

``` r
sx_fit.pam_tuned$bestTune$threshold
```

    ## [1] 0.3206

После многочисленных вариантов подбора значений параметра мы пришли к
выводу, что при его уменьшении точность не повышается “на порядок”, а
при увеличении - закономерно уменьшается.

#### Neural Net с одним скрытым слоем

Настраиваемые параметры этой модели - size (число нейронов в скрытом
слое) и decay (величина лямбды - штрафа за переобучение при
регуляризации). Первый параметр попробуем поувеличивать в промежутке от
10 до 40 нейронов (было от 1 до 10), второй - раздробить более мелко и
выйти за пределы от 0 до 2 (было (0, .1, 1, 2))

``` r
# Neural net
plot(sx_fit.nnet)
```

![](Crime_data_project_Basarab_Berdiyeva_github_files/figure-gfm/unnamed-chunk-23-1.png)<!-- -->

``` r
sx_fit.nnet$bestTune$size
```

    ## [1] 7

``` r
sx_fit.nnet$bestTune$decay
```

    ## [1] 0

``` r
tunegrid <- expand.grid(.size=seq(1:40), .decay=c(0.05, 0.7, 0.1, 0.15, 2.5, 3, 3.5)) 
maxSize <- max(tunegrid$.size) 
numWeights <- 1*(maxSize * (length(d) + 1) + maxSize + 1) 
maxit <- 2000 
sx_fit.nnet_tuned <- train(victim_sex~., data=d_sf, method="nnet", metric=metric, tuneGrid=tunegrid, preProc=c("center", "scale", "spatialSign"), trControl=control, trace=FALSE, maxit=maxit, MaxNWts=numWeights) 
Accuracy=max(sx_fit.nnet_tuned$results$Accuracy[is.finite(sx_fit.nnet_tuned$results$Accuracy)])
print(c("Точность: ", Accuracy))
```

    ## [1] "Точность: "        "0.610878661087866"

``` r
print(c("Число нейронов: ", sx_fit.nnet_tuned$bestTune$size))
```

    ## [1] "Число нейронов: " "10"

``` r
print(c("Lambda: ",sx_fit.nnet_tuned$bestTune$decay))
```

    ## [1] "Lambda: " "0.1"

Вновь ничего не меняется существенным образом - мы не столь успешны в
тюнинге

#### k-nearest neighbors

Здесь настраиваемый параметр один - число соседей K. Ранее в моделях
пробовали следующие значения k: от 1 до 30, а также 41 61 81 101 151 201
251 301 351 401 451

``` r
plot(sx_fit.knn)
```

![](Crime_data_project_Basarab_Berdiyeva_github_files/figure-gfm/unnamed-chunk-24-1.png)<!-- -->

``` r
sx_fit.knn$bestTune$k
```

    ## [1] 351

``` r
#k-nearest neighbors
tunegrid <- expand.grid(.k=c(40:100, 300:400)) 
sx_fit.knn_tuned <- train(victim_sex~., data=d_sf, method="knn", metric=metric, tuneGrid=tunegrid, preProc=c("center", "scale"), trControl=control) 
Accuracy = max(sx_fit.knn_tuned$results$Accuracy)
Accuracy
```

    ## [1] 0.6066946

``` r
print(c("Число соседей: ", sx_fit.nnet_tuned$bestTune$k))
```

    ## [1] "Число соседей: "

Раз на раз не приходится, но, кажется, увеличить число соседей было бы
хорошим решением (при разных прогонках кода число k было больше 10).

## Предсказание национальности жертв преступления “DISTURBING THE PEACE” - нарушения спокойствия

Вновь обучаем много моделей, чтобы найти те самые. Однако из-за того,
что теперь у нас 4 класса, от некоторых моделей придется отказаться.

Параметры кросс-валидации оставляем прежними.

``` r
#Создаем таблицу для записи результатов
res_des=data.frame(mod = character(), Accuracy = numeric())

# Partial Least Squares
des_fit.pls <- train(victim_descent ~ ., data=d_sf, method = "pls", metric = metric, preProc = c("center", "scale"), trControl = control) 
res_des <- rbind(res_des, data.frame(mod = 'Partial Least Squares', Accuracy = max(des_fit.pls$results$Accuracy))) 

# GLMNET
tunegrid <- expand.grid(.alpha=seq(0,1,by=0.1), .lambda=c(1e-1, 1e-2, 1e-3, 1e-4, 1e-5, 1e-6)) 
des_fit.glmnet <- train(victim_descent~., data=d_sf, method="glmnet", metric=metric, tuneGrid=tunegrid, preProc=c("center", "scale"), trControl=control)
res_des=rbind(res_des, data.frame(mod='GLMNET', Accuracy=max(des_fit.glmnet$results$Accuracy)))

#Nearest Shrunken Centroids
tunegrid <- expand.grid(.threshold=seq(0,1,by=0.1))
des_fit.pam <- train(victim_descent~., data=d_sf, method="pam", metric=metric, tuneGrid=tunegrid, preProc=c("center", "scale"), trControl=control)
res_des=rbind(res_des, data.frame(mod='Nearest Shrunken Centroids', Accuracy=max(des_fit.pam$results$Accuracy)))

# Neural net
tunegrid <- expand.grid(.size=seq(1:10), .decay=c(0, .1, 1, 2)) 
maxSize <- max(tunegrid$.size) 
numWeights <- 1*(maxSize * (length(d) + 1) + maxSize + 1) 
maxit <- 2000 
des_fit.nnet <- train(victim_descent~., data=d_sf, method="nnet", metric=metric, tuneGrid=tunegrid, preProc=c("center", "scale", "spatialSign"), trControl=control, trace=FALSE, maxit=maxit, MaxNWts=numWeights) 
res_des=rbind(res_des, data.frame(mod='Neural net', Accuracy=max(des_fit.nnet$results$Accuracy[is.finite(des_fit.nnet$results$Accuracy)])))

# FDA
des_fit.fda <- train(victim_descent~., data=d_sf, method="fda", metric=metric, preProc=c("center", "scale"), trControl=control) 
res_des=rbind(res_des, data.frame(mod='FDA', Accuracy = max(des_fit.fda$results$Accuracy)))

#k-nearest neighbors
tunegrid <- expand.grid(.k=c(4*(0:5)+1, 20*(1:5)+1, 50*(2:9)+1)) 
des_fit.knn <- train(victim_descent~., data=d_sf, method="knn", metric=metric, tuneGrid=tunegrid,                   preProc=c("center", "scale"), trControl=control) 
res_des = rbind(res_des, data.frame(mod='k-nearest neighbors', Accuracy = max(des_fit.knn$results$Accuracy))) 

# knn как делали в классе
des_fit.knn2 <- train(victim_descent ~ ., data=d_sf, method = "knn", 
                  tuneGrid = expand.grid(k = 1:30), 
                  metric = metric,
                  trControl = control)
res_des = rbind(res_des,data.frame(mod = "k-nearest neighbors 1-30", Accuracy = max(des_fit.knn2$results$Accuracy)))  


# Learning Vector Quantization
des_fit.lvq <- train(victim_descent~., data=d_sf, method="lvq", metric=metric, trControl=control)
res_des=rbind(res_des, data.frame(mod='Learning Vector Quantization', Accuracy=max(des_fit.lvq$results$Accuracy)))

# Self-Organizing Maps
des_fit.xyf <- train(victim_descent~., data=d_sf, method="xyf", metric=metric, trControl=control) 
res_des=rbind(res_des, data.frame(mod='Self-Organizing Maps', Accuracy = max(des_fit.xyf$results$Accuracy[is.finite(des_fit.xyf$results$Accuracy)])))

# Recursive Partitioning and Regression Trees
tunegrid <- expand.grid(.cp=seq(0,0.1,by=0.01)) 
des_fit.cart <- train(victim_descent~., data=d_sf, method="rpart", metric=metric, tuneGrid=tunegrid, trControl=control) 
res_des=rbind(res_des, data.frame(mod='Recursive Partitioning and Regression Trees seq(0,0.1,by=0.01)', Accuracy=max(des_fit.cart$results$Accuracy)))

# Recursive Partitioning and Regression Trees
des_fit.rpart2 <- train(victim_descent ~ ., data=d_sf, method = "rpart", 
                    tuneGrid = expand.grid(cp = seq(0, 0.1, 0.001)),
                    metric = metric,
                    trControl = control)

res_des = rbind(res_des, data.frame(mod = 'Recursive Partitioning and Regression Trees seq(0, 0.1, 0.001)', Accuracy = max(des_fit.rpart2$results$Accuracy)))

library('RWeka')
# Logistic Model Trees 
des_fit.LMT <- train(victim_descent~., data=d_sf, method="LMT", metric=metric, trControl=control) 
res_des=rbind(res_des, data.frame(mod='Logistic Model Trees', Accuracy=max(des_fit.LMT$results$Accuracy)))

# PART Rule-Based Classifier 
des_fit.part <- train(victim_descent~., data=d_sf, method="PART", metric=metric, trControl=control) 
res_des=rbind(res_des, data.frame(mod='PART Rule-Based Classifier', Accuracy=max(des_fit.part$results$Accuracy)))

# Rule-Based Classifier 
des_fit.JRIP <- train(victim_descent~., data=d_sf, method="JRip", metric=metric, trControl=control) 
res_des=rbind(res_des, data.frame(mod='Rule-Based Classifier', Accuracy=max(des_fit.JRIP$results$Accuracy)))

# Boosted Linear Model 
des_fit.BstLm <- train(victim_descent~., data=d_sf, method="BstLm", metric=metric, trControl=control)
res_des = rbind(res_des, data.frame(mod='Boosted Linear Model', Accuracy=max(des_fit.BstLm$results$Accuracy)))

# Boosted Logistic Regression 
library(caTools)
des_fit.LogitBoost <- train(victim_descent~., data=d_sf, method="LogitBoost", metric=metric, trControl=control) 
res_des = rbind(res_des, data.frame(mod='Boosted Logistic Regression', Accuracy=max(des_fit.LogitBoost$results$Accuracy)))

#eXtreme Gradient Boosting 
des_fit.xgbLinear <- train(victim_descent ~., data=d_sf, method="xgbLinear", metric=metric, trControl=control) 
res_des=rbind(res_des, data.frame(mod='eXtreme Gradient Boosting', Accuracy=max(des_fit.xgbLinear$results$Accuracy)))

#eXtreme Gradient Boosting2
des_fit.xgbTree <- train(victim_descent ~., data=d_sf, method="xgbTree", metric=metric, trControl=control) 
res_des=rbind(res_des, data.frame(mod='eXtreme Gradient Boosting2', Accuracy=max(des_fit.xgbTree$results$Accuracy)))

#Stochastic Gradient Boosting 
tunegrid <- expand.grid(.n.trees=c(5, 100, 500), .interaction.depth=c(1, 3, 5, 7, 9), .shrinkage=c(0, 1e-1, 1e-2, 1e-3, 1e-4), .n.minobsinnode=c(5, 10)) 
des_fit.gbm <- train(victim_descent~., data=d_sf, method="gbm", metric=metric, tuneGrid=tunegrid, trControl=control, verbose=FALSE) 
res_des=rbind(res_des, data.frame(mod='Stochastic Gradient Boosting', Accuracy=max(des_fit.gbm$results$Accuracy)))

# Bagged CART  
des_fit.treebag <- train(victim_descent~., data=d_sf, method="treebag", metric=metric, trControl=control)
res_des=rbind(res_des, data.frame(mod='Bagged CART', Accuracy=max(des_fit.treebag$results$Accuracy))) 

# Bagged Flexible Discriminant Analysis 
des_fit.bagFDA <- train(victim_descent~., data=d_sf, method="bagFDA", metric=metric, trControl=control) 
res_des=rbind(res_des, data.frame(mod='Bagged Flexible Discriminant Analysis', Accuracy = max(des_fit.bagFDA$results$Accuracy[is.na(des_fit.bagFDA$results$Accuracy)==F])))

# Bagged MARS 
library(earth)
des_fit.bagEarthGCV <- train(victim_descent~., data=d_sf, method="bagEarthGCV", metric=metric, trControl=control) 
res_des = rbind(res_des, data.frame(mod='Bagged MARS', Accuracy=max(des_fit.bagEarthGCV$results$Accuracy)))

# Bagged MARS using gCV Pruning 
des_fit.bagEarth <- train(victim_descent~., data=d_sf, method="bagEarth", metric=metric, trControl=control) 
res_des = rbind(res_des, data.frame(mod='Bagged MARS using gCV Pruning', Accuracy=max(des_fit.bagEarth$results$Accuracy)))

# Conditional Inference Random Forest  
des_fit.cforest <- train(victim_descent~., data=d_sf, method="cforest", metric=metric, trControl=control)
res_des=rbind(res_des, data.frame(mod='Conditional Inference Random Forest', Accuracy=max(des_fit.cforest$results$Accuracy))) 

#Model Averaged Neural Network 
des_fit.avNNet <- train(victim_descent~., data=d_sf, method="avNNet", metric=metric, trControl=control)  
res_des=rbind(res_des, data.frame(mod='Model Averaged Neural Network', Accuracy=max(des_fit.avNNet$results$Accuracy)))

#Parallel Random Forest
des_fit.parRF <- train(victim_descent~., data=d_sf, method="parRF", metric=metric, trControl=control)  
res_des=rbind(res_des, data.frame(mod='Parallel Random Forest', Accuracy=max(des_fit.parRF$results$Accuracy)))

# Random Ferns 
des_fit.rFerns <- train(victim_descent~., data=d_sf, method="rFerns", metric=metric, trControl=control)  
res_des=rbind(res_des, data.frame(mod='Random Ferns', Accuracy=max(des_fit.rFerns$results$Accuracy)))

# Random Forest 
des_fit.ranger <- train(victim_descent~., data=d_sf, method="ranger", metric=metric, trControl=control) 
res_des=rbind(res_des, data.frame(mod='Random Forest', Accuracy=max(des_fit.ranger$results$Accuracy)))

# Random Forest (classical) 
des_fit.rf <- train(victim_descent ~ ., data=d_sf, method = "rf", metric = metric, trControl = control) 
res_des = rbind(res_des, data.frame(mod = 'Random Forest (classical)', Accuracy = max(des_fit.rf$results$Accuracy)))

# Random Forest Rule-Based Model 
des_fit.rfRules <- train(victim_descent~., data=d_sf, method="rfRules", metric=metric, trControl=control)
res_des = rbind(res_des, data.frame(mod='Random Forest Rule-Based Model', Accuracy=max(des_fit.rfRules$results$Accuracy)))

# Regularized Random Forest
des_fit.RRF <- train(victim_descent~., data=d_sf, method="RRF", metric=metric, trControl=control) 
res_des = rbind(res_des, data.frame(mod='Regularized Random Forest', Accuracy=max(des_fit.RRF$results$Accuracy)))

# Regularized Random Forest (другой) 
des_fit.RRFglobal <- train(victim_descent~., data=d_sf, method="RRFglobal", metric=metric, trControl=control) 
res_des = rbind(res_des, data.frame(mod='Regularized Random Forest (другой)', Accuracy=max(des_fit.RRFglobal$results$Accuracy)))

# Weighted Subspace Random Forest
des_fit.wsrf <- train(victim_descent~., data=d_sf, method="wsrf", metric=metric, trControl=control) 
res_des = rbind(res_des, data.frame(mod='Weighted Subspace Random Forest', Accuracy=max(des_fit.wsrf$results$Accuracy)))
```

``` r
#Выведем максимальное аккураси
res_des[which.max(res_des$Accuracy), ]
```

    ##          mod  Accuracy
    ## 4 Neural net 0.4831933

``` r
library(formattable)  

color_scale <- color_tile("white", "lightblue")
res_des$Accuracy <- color_scale(res_des$Accuracy)

formattable(res_des[order(res_des$Accuracy, decreasing = FALSE), ], align="l")
```

<table class="table table-condensed">
<thead>
<tr>
<th style="text-align:left;">
</th>
<th style="text-align:left;">
mod
</th>
<th style="text-align:left;">
Accuracy
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
4
</td>
<td style="text-align:left;">
Neural net
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #add8e6">0.4831933</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
18
</td>
<td style="text-align:left;">
eXtreme Gradient Boosting2
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #b9dee9">0.4537815</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
31
</td>
<td style="text-align:left;">
Regularized Random Forest
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #b9dee9">0.4537815</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
19
</td>
<td style="text-align:left;">
Stochastic Gradient Boosting
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #bddfeb">0.4453782</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
21
</td>
<td style="text-align:left;">
Bagged Flexible Discriminant Analysis
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #bfe0eb">0.4411765</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
26
</td>
<td style="text-align:left;">
Parallel Random Forest
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #bfe0eb">0.4411765</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
22
</td>
<td style="text-align:left;">
Bagged MARS
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #c1e1ec">0.4369748</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
8
</td>
<td style="text-align:left;">
Learning Vector Quantization
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #c4e3ed">0.4285714</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
23
</td>
<td style="text-align:left;">
Bagged MARS using gCV Pruning
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #c4e3ed">0.4285714</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
24
</td>
<td style="text-align:left;">
Conditional Inference Random Forest
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #c4e3ed">0.4285714</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
7
</td>
<td style="text-align:left;">
k-nearest neighbors 1-30
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #c8e5ee">0.4201681</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
9
</td>
<td style="text-align:left;">
Self-Organizing Maps
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #c8e5ee">0.4201681</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
11
</td>
<td style="text-align:left;">
Recursive Partitioning and Regression Trees seq(0, 0.1, 0.001)
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #c8e5ee">0.4201681</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
14
</td>
<td style="text-align:left;">
Rule-Based Classifier
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #c8e5ee">0.4201681</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
28
</td>
<td style="text-align:left;">
Random Forest
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #c8e5ee">0.4201681</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
10
</td>
<td style="text-align:left;">
Recursive Partitioning and Regression Trees seq(0,0.1,by=0.01)
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #cae5ee">0.4159664</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
2
</td>
<td style="text-align:left;">
GLMNET
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #cbe6ef">0.4117647</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
17
</td>
<td style="text-align:left;">
eXtreme Gradient Boosting
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #cbe6ef">0.4117647</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
25
</td>
<td style="text-align:left;">
Model Averaged Neural Network
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #cbe6ef">0.4117647</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
16
</td>
<td style="text-align:left;">
Boosted Logistic Regression
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #cde7ef">0.4090909</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
1
</td>
<td style="text-align:left;">
Partial Least Squares
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #cde7f0">0.4075630</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
3
</td>
<td style="text-align:left;">
Nearest Shrunken Centroids
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #cde7f0">0.4075630</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
6
</td>
<td style="text-align:left;">
k-nearest neighbors
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #cfe8f0">0.4033613</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
20
</td>
<td style="text-align:left;">
Bagged CART
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #cfe8f0">0.4033613</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
32
</td>
<td style="text-align:left;">
Regularized Random Forest (другой)
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #cfe8f0">0.4033613</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
5
</td>
<td style="text-align:left;">
FDA
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #d3eaf1">0.3949580</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
30
</td>
<td style="text-align:left;">
Random Forest Rule-Based Model
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #d3eaf1">0.3949580</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
33
</td>
<td style="text-align:left;">
Weighted Subspace Random Forest
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #d8ecf3">0.3823529</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
12
</td>
<td style="text-align:left;">
Logistic Model Trees
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #dceef4">0.3739496</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
29
</td>
<td style="text-align:left;">
Random Forest (classical)
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #e0f0f5">0.3655462</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
13
</td>
<td style="text-align:left;">
PART Rule-Based Classifier
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #e1f1f6">0.3613445</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
15
</td>
<td style="text-align:left;">
Boosted Linear Model
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #f7fbfc">0.3109244</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
27
</td>
<td style="text-align:left;">
Random Ferns
</td>
<td style="text-align:left;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #ffffff">0.2941176</span>
</td>
</tr>
</tbody>
</table>

### Доработка модели для предсказания национальности

Результаты точности намного хуже, чем в предсказании пола. Попробуем
потюнить модель стохастического градиентного бустинга

Настраиваемые параметры этой модели:

- n.trees - число обучаемых деревьев аkа число итераций обучения

- interaction.depth - максимальная глубина каждого из деревьев аkа
  максимальный уровень взаимодействия переменных

- shrinkage - learning rate для расширения деревьев. Чем меньше
  параметр, тем больше деревьев нужно

- n.minobsinnode - минимальное значение наблюдений на концах деревьев

Посмотрим, какие значения параметров выиграли при первичном обучении,
затем переберем новые.

``` r
plot(des_fit.gbm)
```

![](Crime_data_project_Basarab_Berdiyeva_github_files/figure-gfm/unnamed-chunk-27-1.png)<!-- -->

``` r
des_fit.gbm$bestTune$n.trees
```

    ## [1] 100

``` r
des_fit.gbm$bestTune$interaction.depth
```

    ## [1] 7

``` r
des_fit.gbm$bestTune$shrinkage
```

    ## [1] 0.01

``` r
des_fit.gbm$bestTune$n.minobsinnode
```

    ## [1] 5

``` r
#Stochastic Gradient Boosting 
tunegrid <- expand.grid(.n.trees=c(10, 30, 50, 200), .interaction.depth=c(2, 4, 6), .shrinkage=c(0, 0.05, 1e-1, 1e-2), .n.minobsinnode=c(3, 6, 8)) 
des_fit.gbm_tuned <- train(victim_descent~., data=d_sf, method="gbm", metric=metric, tuneGrid=tunegrid, trControl=control, verbose=FALSE)
des_fit.gbm_tuned$bestTune$n.trees
```

    ## [1] 50

``` r
des_fit.gbm_tuned$bestTune$interaction.depth
```

    ## [1] 6

``` r
des_fit.gbm_tuned$bestTune$shrinkage
```

    ## [1] 0.05

``` r
des_fit.gbm_tuned$bestTune$n.minobsinnode
```

    ## [1] 8

``` r
max(des_fit.gbm_tuned$Accuracy)
```

    ## [1] -Inf

# Выводы и результаты

Нам не удалось добиться точности выше, чем 65%, при этом процедура
анализа очень нестабильна из-за того, что каждый раз мы получаем новые
результаты.

Зато мы узнали, какие параметры можно настраивать в нейронных сетях,
градиентном бустинге, knn и shrunken центроидах.

## Бонус. Временные ряды по использованию оружия

Попытаемся спрогнозировать частоту использования оружия в преступлениях
в ближайшие недели. Для этого создадим отдельный датафрейм, в котором
посчитаем количество преступлений с использованием оружия для каждой
недели.

``` r
#Добавляем в датафрейм столбец про неделю
d$year_week <- format(d$date_occ, "%Y-%U")

# Создаем датафрейм d_ts
d_ts <- aggregate(weapon_used ~ year_week, data = d, FUN = function(x) sum(x))
colnames(d_ts) <- c("month_year", "weapon_used_crimes")

head(d_ts)
```

    ##   month_year weapon_used_crimes
    ## 1    2020-00               1090
    ## 2    2020-01               1339
    ## 3    2020-02               1355
    ## 4    2020-03               1489
    ## 5    2020-04               1481
    ## 6    2020-05               1462

``` r
#Создаем временной ряд
ts_weapon <- ts(d_ts$weapon_used_crimes, frequency = 52, start = c(2020, 0), end = c(2023, 44))

boxplot(ts_weapon~cycle(ts_weapon))
```

![](Crime_data_project_Basarab_Berdiyeva_github_files/figure-gfm/unnamed-chunk-28-1.png)<!-- -->

``` r
dec_weapon <- decompose(ts_weapon, type="additive")
fit_weapon <- stl(ts_weapon, s.window = "periodic")
plot(fit_weapon)
```

![](Crime_data_project_Basarab_Berdiyeva_github_files/figure-gfm/unnamed-chunk-28-2.png)<!-- -->

``` r
head(d_ts[ order (d_ts$weapon_used_crimes), ])
```

    ##     month_year weapon_used_crimes
    ## 204    2023-45                236
    ## 107    2022-00                308
    ## 54     2021-00                526
    ## 53     2020-52                822
    ## 106    2021-52                960
    ## 1      2020-00               1090

Как видим, “просадка” объясняется тем, что по одному из наблюдений (45
неделя 2023) накопление данных в течение недели еще не закончилось в
момент их обновления, а остальные - первые недели январей или последние
недели декабрей - не самые криминальные дни для владельцев оружия.

Используем несколько моделей для предсказания будущего числа
преступлений с оружием в ближайшие недели - ETS, ARIMA и две нейронные
сети - NNAR и MLP.

``` r
#ETS
library(fpp2)
# Различия в преступлениях по месяцам
diffPr <- diff(ts_weapon)
WeaponForecastETS <- ets(ts_weapon) 
summary(WeaponForecastETS)
```

    ## ETS(A,N,N) 
    ## 
    ## Call:
    ##  ets(y = ts_weapon) 
    ## 
    ##   Smoothing parameters:
    ##     alpha = 0.5277 
    ## 
    ##   Initial states:
    ##     l = 1224.6838 
    ## 
    ##   sigma:  128.7914
    ## 
    ##      AIC     AICc      BIC 
    ## 3022.948 3023.070 3032.858 
    ## 
    ## Training set error measures:
    ##                    ME    RMSE      MAE       MPE    MAPE      MASE       ACF1
    ## Training set 3.625535 128.149 80.62597 -1.408408 7.26788 0.6195601 0.09290602

``` r
checkresiduals(WeaponForecastETS)
```

![](Crime_data_project_Basarab_Berdiyeva_github_files/figure-gfm/unnamed-chunk-29-1.png)<!-- -->

    ## 
    ##  Ljung-Box test
    ## 
    ## data:  Residuals from ETS(A,N,N)
    ## Q* = 40.513, df = 40, p-value = 0.4476
    ## 
    ## Model df: 0.   Total lags used: 40

``` r
weapon_ETS_f<-forecast(WeaponForecastETS, h = 12)


#ARIMA 
WeaponForecastARIMA <- auto.arima(ts_weapon, d=1, D=1, 
                                 stepwise = FALSE, approximation = FALSE, 
                                 trace = F) 
summary(WeaponForecastARIMA) 
```

    ## Series: ts_weapon 
    ## ARIMA(0,1,4)(1,1,0)[52] 
    ## 
    ## Coefficients:
    ##           ma1      ma2      ma3     ma4     sar1
    ##       -0.5333  -0.2988  -0.0334  0.0527  -0.5897
    ## s.e.   0.0868   0.0974   0.0991  0.0831   0.0690
    ## 
    ## sigma^2 = 21230:  log likelihood = -956.34
    ## AIC=1924.69   AICc=1925.29   BIC=1942.67
    ## 
    ## Training set error measures:
    ##                    ME     RMSE      MAE        MPE     MAPE      MASE
    ## Training set 11.38384 122.8988 70.61831 -0.6625624 6.379585 0.5426575
    ##                     ACF1
    ## Training set -0.02273461

``` r
checkresiduals(WeaponForecastARIMA)
```

![](Crime_data_project_Basarab_Berdiyeva_github_files/figure-gfm/unnamed-chunk-29-2.png)<!-- -->

    ## 
    ##  Ljung-Box test
    ## 
    ## data:  Residuals from ARIMA(0,1,4)(1,1,0)[52]
    ## Q* = 33.875, df = 35, p-value = 0.5223
    ## 
    ## Model df: 5.   Total lags used: 40

``` r
Weapon_ARIMA_f<-forecast(WeaponForecastARIMA, h = 12)
summary(Weapon_ARIMA_f)
```

    ## 
    ## Forecast method: ARIMA(0,1,4)(1,1,0)[52]
    ## 
    ## Model Information:
    ## Series: ts_weapon 
    ## ARIMA(0,1,4)(1,1,0)[52] 
    ## 
    ## Coefficients:
    ##           ma1      ma2      ma3     ma4     sar1
    ##       -0.5333  -0.2988  -0.0334  0.0527  -0.5897
    ## s.e.   0.0868   0.0974   0.0991  0.0831   0.0690
    ## 
    ## sigma^2 = 21230:  log likelihood = -956.34
    ## AIC=1924.69   AICc=1925.29   BIC=1942.67
    ## 
    ## Error measures:
    ##                    ME     RMSE      MAE        MPE     MAPE      MASE
    ## Training set 11.38384 122.8988 70.61831 -0.6625624 6.379585 0.5426575
    ##                     ACF1
    ## Training set -0.02273461
    ## 
    ## Forecasts:
    ##          Point Forecast     Lo 80    Hi 80     Lo 95    Hi 95
    ## 2023.846      1548.9679 1362.2381 1735.698 1263.3893 1834.547
    ## 2023.865      1548.2767 1342.2112 1754.342 1233.1268 1863.427
    ## 2023.885      1487.1430 1278.7072 1695.579 1168.3680 1805.918
    ## 2023.904      1431.7174 1221.7744 1641.660 1110.6373 1752.798
    ## 2023.923      1509.2944 1296.4603 1722.129 1183.7927 1834.796
    ## 2023.942      1416.0685 1200.3820 1631.755 1086.2044 1745.933
    ## 2023.962      1338.4839 1119.9823 1556.986 1004.3145 1672.653
    ## 2023.981      1363.9780 1142.6970 1585.259 1025.5579 1702.398
    ## 2024.000      1170.1235  946.0977 1394.149  827.5055 1512.742
    ## 2024.019       811.9137  585.1763 1038.651  465.1487 1158.679
    ## 2024.038      1354.6438 1125.2268 1584.061 1003.7807 1705.507
    ## 2024.058      1339.1548 1107.0891 1571.221  984.2409 1694.069

``` r
library(tsibble)  #для работы с рядами по принципам tidy data
library(fable)  #для tidy прогнозирования
library(forecast)  #для функции forecast и сети nnetar
library(nnfor) #для функции mlp

set.seed(42)

#NNAR
nnetar_fit_weapon <- nnetar(ts_weapon)
nnetar_fit_weapon
```

    ## Series: ts_weapon 
    ## Model:  NNAR(10,1,6)[52] 
    ## Call:   nnetar(y = ts_weapon)
    ## 
    ## Average of 20 networks, each of which is
    ## a 11-6-1 network with 79 weights
    ## options were - linear output units 
    ## 
    ## sigma^2 estimated as 1019

``` r
checkresiduals(nnetar_fit_weapon)
```

![](Crime_data_project_Basarab_Berdiyeva_github_files/figure-gfm/unnamed-chunk-29-3.png)<!-- -->

    ## 
    ##  Ljung-Box test
    ## 
    ## data:  Residuals from NNAR(10,1,6)[52]
    ## Q* = 35.524, df = 40, p-value = 0.6719
    ## 
    ## Model df: 0.   Total lags used: 40

``` r
nnetar_pred_weapon <- forecast(nnetar_fit_weapon, h = 12, PI = F)


#MLP
mlp_fit_weapon <- mlp(ts_weapon)
print(mlp_fit_weapon)
```

    ## MLP fit with 5 hidden nodes and 20 repetitions.
    ## Series modelled in differences: D1D52.
    ## Univariate lags: (1,2,3,4,5,6,7,8,9,10,11,12,14,18,25,26,27,31,32,36,40,47,48,50,51,52)
    ## Forecast combined using the median operator.
    ## MSE: 177.4306.

``` r
mlp_pred_weapon <- forecast(mlp_fit_weapon)
```

Везде (кроме MLP, где нет остатков) остатки То есть мы хотели бы, чтобы
значение p теста было больше 0,05, потому что это означает, что остатки
для нашей модели временных рядов независимы, и у нас нет серийной
корреляции (p-value везде в тестах Ljung-Box сильно больше 0,05).

Далее сравним показатели точности моделей и определим, какая лучше.

``` r
all_models_weapon=list(WeaponForecastETS,WeaponForecastARIMA ,nnetar_fit_weapon,mlp_pred_weapon)
row_n=c("ETS","ARIMA","NNETAR","MLP")
all_weapon_acc <- data.frame()
for (mod in all_models_weapon){
  ac=as.data.frame(accuracy(mod))
  all_weapon_acc=rbind(all_weapon_acc,ac)
}  
row.names(all_weapon_acc)=row_n
all_weapon_acc
```

    ##                 ME      RMSE      MAE        MPE      MAPE      MASE
    ## ETS     3.62553518 128.14903 80.62597 -1.4084080 7.2678796 0.6195601
    ## ARIMA  11.38384218 122.89880 70.61831 -0.6625624 6.3795853 0.5426575
    ## NNETAR  0.06707054  31.92558 23.08953 -0.1357986 1.6235720 0.1774286
    ## MLP     0.50405085  13.32031  9.34278  0.0220205 0.6780743 0.0674016
    ##                ACF1
    ## ETS     0.092906023
    ## ARIMA  -0.022734614
    ## NNETAR  0.102336705
    ## MLP    -0.001701594

``` r
plot(ts_weapon, main = "Модели прогнозирования временных рядов по использованию преступниками оружия в Лос-Анджелесе")
lines(weapon_ETS_f$mean, col = "blue")
lines(Weapon_ARIMA_f$mean, col = "green")
lines(nnetar_pred_weapon$mean, col = "violet")
lines(mlp_pred_weapon$mean, col = "orange")
legend("topleft", row_n, col = c("blue", "green","violet","orange"), lty = 1)
```

![](Crime_data_project_Basarab_Berdiyeva_github_files/figure-gfm/unnamed-chunk-30-1.png)<!-- -->

Победителем можно назвать MLP, так как практически все виды ошибок
меньше.
