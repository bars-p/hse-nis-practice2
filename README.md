# Практика 2: «Оценка сервиса системы ОТ района для буднего дня»

## Районы
1.	Царицино
2.	Коньково
3.	Лосиноостровский
4.	Бибирево
5.	Ховрино
6.	Кунцево
7.	Зюзино
8.	Ясенево
9.	Вешняки
10.	Бирюлево Западное

## Задание
1.	Определить границы района (`"admin_level"="8"`)
2.	Определить все остановки (`highway = «bus_stop»`, `rail_way  = «tram_stop»1) внутри и на границе района (+100 м)
3.	Определить городские маршруты района (`network = «Московский транспорт»`), т.е. маршруты, проходящие по территории района и его границе (+100 м)
4.	Определить все станции метро в границах района и на прилегающей территории (+700 м до центроида платформы)
5.	Построить буферную зону вокруг всех остановок радиусом 400 м 
6.	Построить буферную зону вокруг всех центроидов платформ метро радиусом 800 м
7.	Оценить доступность транспортной инфраструктуры на территории района
    1.	Доля покрытия территории
    2.	Жилые дома вне зоны (оценить численность жителей вне зоны доступности)
    3.	Социальные объекты вне зоны
8.	Построить сайты по остановкам, критерий: удаленность до «примерно» 200 м (проще вручную)
9.	Построить центроиды сайтов (проще через `Dissolve`)
10.	«Привязать» МВН маршрутов района к сайтам – МВН как последовательность сайтов (только для части трассы внутри района)
11.	Определить периоды пика, утро и вечер – максимальная плановая интенсивность маршрутов района (https://transport.mos.ru/transport/schedule) – не забыть выбрать будний день!
12.	Определить интенсивность для каждого маршрута для периодов:
    1.	Утро пик
    2.	День 13:00 – 14:00
    3.	Вечер пик
    4.	Ночь 3:00 – 4:00
13.	Построить карты интенсивности работы МВН для каждого из 4 периодов (толщина линии МВН линейно пропорциональна числу рейсов за час рассматриваемого периода)
14.	Рассчитать показатели интенсивности работы МВН посайтно по каждому из 4 периодов – суммарное число рейсов в час по всем маршрутам
15.	Построить карты производительности сайтов для каждого из 4 периодов (размер круга визуализации сайта квадратично пропорционален суммарному числе рейсов рассматриваемого периода)
16.	Подготовить предложения по возможным направлениям развития системы ОТ в районе на основе имеющихся данных

## Дополнительное задание для Практики 1
1.	Построить карту распределения жилых областей района – категории зданий
2.	
3.	

## Запросы Overpass
### Границы района
```
[out:json][timeout:25];
// fetch area “moscow” to search in
{{geocodeArea:moscow}}->.searchArea;
// gather results
nwr["boundary"="administrative"]["admin_level"="8"]["name"="район Зябликово"](area.searchArea);
// print results
out geom;
```
### Данные ОТ
```
[bbox:{{bbox}}];
(
  rel[type=route][route=tram];
  rel[type=route][route=subway];
  rel[type=route][route=bus];
);
out meta;
>;
out qt;
```
