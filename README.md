@startuml "базовый сценарий"

title Базовый сценарий

actor "Оператор" as op
participant "Система управления\nгородским движением" as tm
participant "Светофор" as tl

group Установка режимов

op -> tm++: задание режима
tm -> tl++: режим работы

note over tm
Возможные варианты
- длительность зелёного по направлениям 
(если 0 по всем направлениям - движение блокируется, всем красный)
- отключить светофор (моргающий жёлтый)
end note

tl --> tm--: подтверждение
tm --> op--: подтвеждение

end

group Самодиагностика и статус
tl -> tl: самодиагностика
tl -> tm: состояние светофора
tm -> op: состояние светофоров
end

group Ручное управление

op -> tm++: принудительная смена состояния
tm -> tl++: принудительная смена состояния
tl --> tm--: подтверждение
tm --> op--: подтверждение

end

@enduml

@startuml "базовый сценарий + hla"

actor "Оператор" as op
participant "Система управления\nгородским движением" as tm
participant "1. Связь" as conn
participant "2. Система управления\nсветофора" as control_tl #red
participant "3. Управление\nсветодиодами" as control_leds
participant "4. Система\nдиагностики" as self_diag

group Установка режимов

op -> tm++: задание режима
tm -> conn: режим работы
conn -> control_tl++: режим работы
control_tl -#red> control_tl: запись режима
control_tl --#red> conn--: подтверждение

conn --#red> tm: подтверждение
tm --#red> op--: подтверждение

end

group Самодиагностика и статус
control_leds -> self_diag: статус
self_diag -> control_tl: статус 
control_tl -#red> conn: состояние светофора
conn -#red> tm: состояние светофора
note over conn 
Компрометация сообщений от светофора в городскую систему 
может замедлить время реакции на поломку, 
но это не нарушает имеющиеся цели безопасности
end note
tm -#red> op: состояние светофоров
end

group Ручное управление

op -> tm++: принудительная смена состояния
tm -> conn: принудительная смена состояния
conn -> control_tl++: принудительная смена состояния
control_tl -> control_leds++: принудительная смена состояния
control_leds --> control_tl--: подтверждение
control_tl --#red> conn--: подтверждение
conn --#red> tm: подтверждение
tm --#red> op--: подтверждение

end

@enduml

@startuml "Негативный сценарий 1. Связь"

title Негативный сценарий №1. Связь\nНарушения ЦБ нет

actor "Оператор" as op
participant "Система управления\nгородским движением" as tm
participant "1. Связь" as conn 
participant "2. Система управления\nсветофора" as control_tl #red
participant "3. Управление\nсветодиодами" as control_leds
participant "4. Система\nдиагностики" as self_diag

group Установка режимов
op -> tm++: задание режима
tm -> conn: режим работы
conn -#red> control_tl++: режим работы
note over conn 
Компрометация режима работы в худшем случае приведёт к пробкам, 
но при условии проверки режима в системе управления, 
запрещённые комбинации будут заблокированы
end note
control_tl -> control_tl: запись режима
control_tl --#red> conn--: подтверждение
conn --#red> tm: подтверждение
tm --#red> op--: подтвеждение

end

group Самодиагностика и статус
control_leds -> self_diag: статус
self_diag -> control_tl: статус 
control_tl -> conn: состояние светофора
conn -#red> tm: состояние светофора
note over conn 
Компрометация сообщений от светофора в городскую систему 
может замедлить время реакции на поломку, 
но это не нарушает имеющиеся цели безопасности
end note
tm -> op: состояние светофоров
end

group Ручное управление

op -> tm++: принудительная смена состояния
tm -> conn: принудительная смена состояния
conn -#red> control_tl++: принудительная смена состояния
note over conn 
Компрометация режима работы в худшем случае приведёт к пробкам, 
но при условии проверки режима в системе управления, 
запрещённые комбинации будут заблокированы
end note
control_tl -> control_leds++: принудительная смена состояния
control_leds --> control_tl--: подтверждение
control_tl --#red> conn--: подтверждение
conn --#red> tm: подтверждение
tm --#red> op--: подтверждение

end

@enduml
