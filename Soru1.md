# Soru 1: dsmbootcamp.sample.semi_structured_hw tablosunu kullanarak dsmbootcamp.sample.semi_structured_hw_expected tablosundaki veriyi oluşturmak

car ve manufacture "car.id = manufacture.id" olacak şekilde unnest edilerek aliasları tanımlandı. 
İlgili sütunların isimleri tanımlandı.
Purchase'ın unnest edilmesinden gelen sütunlar, id değeri ve ((date +3 saat)) değerleri ile array olarak tanımlandı.

```SQL
select 
  name, 
  c.id as car_id, 
  c.model as car_model, 
  m.year as manufacture_year, 
  array(select as struct f.id, timestamp_add(f.date, INTERVAL 3 HOUR) as date from unnest(purchase) as f) as purchase
from can_yazici.semi_structured_hw as main
  cross join unnest(car) as c
  cross join unnest(manufacture) as m
  on m.id = c.id;
```
