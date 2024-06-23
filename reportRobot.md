# Робот-фармацевт
Учебный пример для курса по кибериммунной разработке


- [Учебный пример "Робот-фармацевт.](#Учебный-пример-"Робот-Фрамацевт") 
- [Краткое описание назначения и применения системы.](#Краткое-описание-назначения-и-применения-системы)
-  [Ключевые ценности, ущербы, неприемлемые события)](#Ключевые-ценности,ущербы,неприемлимые_события)
- [Контекст работы системы](#Контекст-работы-системы)
       - [Вариант 1 ](#Вариант-1)
       - [Вариант 2 ](#Вариант-1)
- [Основные функциональные сценарии.](#Основные-функциональные-сценарии) 
- [Высокоуровневая архитектура системы.](#Высокоуровневая-архитектура-системы) 
- [Компоненты:  описание подсистем](#Компоненты:-описание-подсистем)
- [Описание Сценариев (последовательности выполнения операций), при которых ЦБ нарушаются](#описание-сценариев-последовательности-выполнения-операций-при-которых-цб-нарушаются)
- [Указание "доверенных компонент" на архитектурной диаграмме.](#указание-доверенных-компонент-на-архитектурной-диаграмме)
- [Политики безопасности](#Политики-безопасности)
- [Анализ векторов атак и эффекта.](#Анализ-векторов-атак-и-эффекта-безопасности.)
- [Упражнение.](#Упражнение)

## Учебный пример "Робот-фармацевт

Робот-фармацевт

![image](https://github.com/DarimaU/desktop-tutorial/blob/dom_zadanie/image.jpg)

Продукт - робот-фармацевт, который производит лекарство по индивидуальному рецепту.
Рецепт включает в себя

а) точный состав и количество компонентов, порядок и условия изготовления конечного продукта

б) уникальный идентификатор лекарства, который изготавливается в определённом объёме для индивидуального курса лечения

Основные этапы процесса изготовления лекарства по рецепту

![](https://github.com/DarimaU/desktop-tutorial/blob/dom_zadanie/%D0%9E%D1%81%D0%BD%20%D1%8D%D1%82%D0%B0%D0%BF%D1%8B.png)

 ## Высокоуровневая архитектура системы 
![Высокоуровневая архитектура системы.](https://www.plantuml.com/plantuml/png/RPC_RnD14CNx-nGZqq0HS_vlImY5ZeAFaCO20v628oK7jCb5YK29P4eA4AAXNYuSFkpu_1NUV2FUxdab5csn8ptllD--6UlsJxFfIVRspL6I7MP7CsdXavxf9IhDKMAbkLxe6OoWq6izHuqLporgSR_NAB3HXTn_-kp90tdNJjjfsagIazdpR3f_HTozzwyFCr8xRS5tCXPOwarBfgVoylYu4sdiil4pbhX3INw93IgKSZ0NmHR6Hd5NUVEuwBbUu2Th3iCaL-p-u_5TYV1xvF-mN8SmMEiDDWGl3kOShtAaaayO8NZhMWgico2wyEXUXDot8xfuDNunXy4jJRKbKgrWMh9pzoFk0TtVcfdTW1_zx1pTxVmEMzPD4ztExhCC8hJXVxGF91Km3T4RXn7ZYCOlRiyhLCsERNHl6KKiOpktvkwr2ckU9G5N_wvh7B5DQFjgb-H25W_v7wFMIm8CVdE1PHXs4a5qKZkcUxQmIzThtzr9awJzQ6_liHE9BU9bpyekfLSiihiR16eOg56WnawHOaK_k9fODV2AKImgbADGZaCv2IGherlPJVPdynVyLly2)

## Краткое описание назначения и применения системы

а) Робот-фармацевт управляется центральной системой по беспроводному интерфейсу

б) Робот-фармацевт передаёт состояние в центральную систему

Ценности продукта и негативные события в их отношении
|Ценность|	Негативное событие|	Величина ущерба|	Комментарий|
|----|----|----|----|
|Лекарство|Нарушение технологического процесса	|Высокий|возможно причинение вреда здоровью клиентов|
|Рецептура	| Неавторизованный доступ к рецептуре (раскрытие торгового секрета)	|Высокий|конкуренты смогут производить аналоги|
|Персональные данные|Неавторизованный доступ к персональным данным клиентов|Высокий|оборотный штраф для организации|
|Робот|невозможность производства лекарства из-за отказа оборудования|Средний	|при необходимости сотрудник фармацевт сможет вручную приготовить небольшие партии лекарств|
|Люди	|отравление из-за приёма неправильного лекарства|Высокий|возможно причинение вреда здоровью клиентов||

Роли пользователей
 - Оператор-фармацевт - вводит задание на производство и получает лекарство для передачи клиенту 

 - Пациент - получает рецепт от врача в клинике и по этому рецепту получает лекарство в аптеке

## Контекст работы системы
 ### Вариант 1. Лекарства общего назначения

 - Не предполагает льготного получения, не является наркотиком, не предполагает существенных ограничений для клиентов.
Однако лекарство может быть очень дорогим или с очень коротким сроком годности, поэтому клиенту важно получить свежее лекарство в минимально достаточной дозировке

![](https://github.com/SvPolyanskaya/CyberImmunity/blob/Robot-in-Pharmacy/-Контекст%201.png)

Упрощение

Чтобы не отвлекаться на систему управления складскими запасами предположим, что это реализовано на уровне аптечной сети - только тем роботам будет передано задание на производство, которые располагают достаточным запасом субстанций

 ### Вариант 2. Лекарства из специального списка
Варианты
-	входит в список жизненно-необходимых, производство полностью или частично оплачивается государством

-	содержит наркотические вещества или прекурсоры для их получения, авторизованное получение такого лекарства должно строго контролироваться
-	всё остальное из варианта 1.

  ![](https://github.com/SvPolyanskaya/CyberImmunity/blob/Robot-in-Pharmacy/-Контекст%202.png)

 ## Цели и предположения безопасности
 
Цели безопасности

 - Выполняются только аутентичные задания на производство
 
Предположения безопасности

- "доктор плохого не посоветует" - врачи, выписывающие рецепты, благонадёжны.
 
## Компоненты:  описание подсистем
| Название | Назначение | Комментарий |
|----|----|----|
|*1. Связь*|	отвечает за взаимодействие с системой распределения задач на изготовление и с базой данных рецептов|	получает полный рецепт или его идентификатор|
|*2. Измерение параметров субстанций*|контролирует массу и/или объём компонентов| 	---|
|*3. Центральная система управления*|	осуществляет общее управление процессом приготовления лекарства	|---|
|*4. Самодиагностика*|	осуществляет сбор и анализ телеметрии всех подсистем для оценки работоспособности системы|---|	
|*5. Перемещение компонентов*|	отвечает за расчёт траекторий перемещения робота на каждом этапе тех. процесса|	---|
|*6. Перемешивание*|осуществляет комплекс действий для достижения требуемого уровня смешения компонентов|	используется в том числе для подготовки промежуточных ёмкостей|---|
|*7. Маркировка*|изготавливает и наклеивает на ёмкость описание лекарства	|---|
|*8. Стерилизация*|осуществляет комплекс действий по стерилизации ёмкости с лекарством|включает контроль качества стерилизации|
|*9. Нагрев/охлаждение*|	обеспечивает требуемые по тех. процессу температурные условия для химических реакций|---|
|*10. Приводы*|	управляют захватами робота для реализации рассчитанных траекторий и механических воздействий на субстанции (в т.ч. измельчение и перемешивание)	|---|

### Основные функциональные сценарии получения лекарства
 Сценарий генерации событий
![Сценарий генерации событий](https://www.plantuml.com/plantuml/png/pLFDpfD05DtFKzom_OA9MnQchpAb99AqqC2mS4TfrHXDrAqRzGqgbeZMuYlSUIFFPJerj8s9EpUKJC_FcNEvizBembIh9GLLcSIwJCf0APEQPK81VxOlkECJxstDFN-dnu-8F_B0HxkrB-KVd7R4Hxp-493Ts8PRtXCmN-mh77_bWKI0lydJa-nRcEZOv0LCFe3Voxbj0j8bnSiqoOnQ8rSQfskT6GyIgXXvM9R6Lx1t_0i9kWje_LGNAnq_kuAzbq0Iyu2N4vnVs-U4EtRZVKLYu7OKM6YZvsX5_MzvfWAVf70UR1FQtJYjdtWAjpsNMkJptA3pokHPjPedXLAkPmgVdAD7X9W3p3TsYmc_WQjeO5W4cNgStbuvhB1yb6YIbBYNQkJdu8OAXPthIUvXwplVY_AzGDT5ZVvHO2HDKqcZI5I3ifb41DoZAFI63myHEJItWDQYFv6uc7Z6BVxAnUD1yFUxxuBDaCxGByg-xI8CGHhu83C6nQ_TdpXkae0vxTu3RVEN7LLApP9iWTN_3G00)
![Сценарий генерации событий](https://www.plantuml.com/plantuml/png/bLFDZfH04BxtKrIuRZ3noi7ig_ImdKZ2m0IQWpTWLetHPFLclAXlWEEIHSTbNg7gZQngbiumCKxcCaFW-_dgg-xhqkh2LkiKWgeqiIvD6IXb4viQ2F0xlS4U7x6Z6WVy1S-V0Nx54VUqfRVkou0zu9uVVmk86cfnXnqmvWUzuzS_SGGHm0VvdKbqnoOwjdd19b-OFyXxQWFG9SHfOZAhDfmhYPEDpgm7CLMCPbYMn2UmZtZW1Bq7RLxgOgtZLoUmRv8FHsf3kdN3_S7EZRfxob3ag_mqmYUPGcQxvuT7ZlkUNWDpUySKtn5tZdsZhLvnbJnZPVEiMgzCeTGK6C8NJnD6m357rcbeour-e5P2I3d0EMhNLgScBBFyB5TNqS8MS91ovEz-gf4rRgUc91JL_zYGcjMEbIFPsq6qdTBURvZgkJ3iGbPly22dmAso5IJTBGHTVP9J2dEA8pNBhhhpiJcbqga5NfVdAIVjFIAXFyWfc-e_oYmH5vQqLIOj3U3d2thoVdwfqOL5ppm8VUX5B6Mo6pNR72qZ3ADpUvlEXWDAnuCioKct_xcRIbsp8z_ulm00)

### Описание Сценариев (последовательности выполнения операций), при которых ЦБ нарушаются
![Описание Сценариев:](https://www.planttext.com/api/plantuml/png/hLRBJXj14BpFLqny3_BxTOZua5msZgKW6MDvRQJSi2q84GHop25Hn2NdmS7W-FaBCt-KwkxPnRiOHKQvm7hSrTrLNTFh_R0NT7lzmvREzCDc8mYROKQfta6lrTGPU-FExCGkhN4dTch_wDoUjZ_nlCAd1pl6_pitS4DwqdQEq1c5-YEZyVsj-upZt_GzqW14oJvnqgcxHgaEoXyq3Zf1kuU2N-qQMCwJqK6eEn-2xc7G-9WCepPkxDXTsmTtoN7XSIfJ0I6_g8mRebzZv-wIIr-_RMitGEq1rrbOGmSZbAMeCPEGrYXj8Pcqo7KDK20E2Go8BUsASqtZdej9K9L0L8mrdBDo1hf6DQh9y199pC7KtOJbGqDsWZvHOeN3DVukXHkUnfobbCoIHvPlABHWjC-WASMQXsauzv17EMP9eC4j4p78UqRJvhpvbF9Pxu2fd_u5H-MooR1oYiGvnnjfWn7b9A2sPt-Gd8oWXg3gASGozXvAJpQ0jIImWahVcT8CYZATU10L5VHxH-t-uRjc5_RmLjAlty0kTKrZuB5ZVcnEBPz0QcHdRaXIhJGrn9S0ldGZ5Hu3NdWXk4Yb0HQPwGXWc54CjVRTJuIBAb1qrKTlceU227sfMTrPP41L9KGkkmiab_LLw8gAdUnA4XLIXwfrTDJHTAl8wdDgV8K0p0XFIs9BDK-z44GRDM0h8LAgaoIFZk3otD5JwxahRSUHeEJWUoY5Dh0tbdYwqYpV2LANA7M-hhdDXL0McWY4TT0MRC_N1aBGtedMbSf7Ohq0AwhbKmBb8vwRXwMupFzdBssabOqNXfYK3OKBI8U-dS8k29vUhQurkLMwP6g-VLcYaaqiJPtLFEjTCCA6AYK4h6tp8ZTLJj4u5ukhybR9es-bJ3cLiFni5HOhSJNDPbIy_bCBm1gbckttIf9KwlBwc_7xnSlmnRyri8U16CaQYOTRYLdi21I2bHINohC4dx-PVgyXcAl4I7V1rto3B0x_wVJTiZrw-ybjsig2Dtfg1ST1hvJQnp3mA-Sl)

**Отдельная диаграмма для первого негативного сценария 
![](https://www.planttext.com/api/plantuml/png/hLPDRzf04BtlhzZISoemiGqSgloFjWUNM2fIGX0saNfBG4bJ9KrwxA5LbKlF3Yq9XG1_OVSVzStiuc83HKIz9CioR-RDcuzbBug3TjmvF925JXJMWoYC2aB4ZVWWb0Lrgy_LG4rKea_KKFsMfHTIVSTvYayFge__l_Ifxj99gZ5CHsHghnA9x-_qHrp_fE_X1Y1oze6T3lKDGhKGlb5lj89cZ82VrGnOzbEGGIHRxuBsOL1_dpKZ6hUghs_KWxvYk-XOIlcy7Uxd79PX-OEYwIve9sgihvZ1pUkcrAUWSChX7bL25pr49wi-vs8OalTorkakXq-0GlvG8a5-4pLbNyEK-cuML24G1MCfnonW0dddCIfPSvUKPcDYDs0LGKWDm1CXfhYSuU_4v8PJdxsuMIyEl7n1e4T6Mm-INCoufWdxxd95-om9DBZZH1BuFQUYirydLu2YROIXRO9BjYeLisPUBeaBjayC3KPuMK3rXVf6SZA2247LCuYLg7ieFLW0LhD07v6-SaeZAChff8NmHT29ZvgTmxTX6-rXEqhkl4JNr2ILWSkE-d6FIlC9IVNKI7T9ggaaGZmBQ4_T4z7npYlgjZTmKfPFTB9B5CerQUIcAu3HbAQnPZQBWSb91FMuSHp48PgnJC2A1Ixs4zcJeol9We_cFIdsmmLuUgo82dag5RTnbQ9Hx5BHCg41Drsefel1O5EnMQupgGWX3ewEMZozagQLHcXCGao1GUrncf1wHF3C2aioWX3QLGBFWhWrKlblip5Tpc2vg_MrLFrvZMWuxY4-o64pJN2wbboH4nGfvUaAbw8uDSbvF1grZ4B0e4514iF5mmaDQSdDTwDmvZe_0PioSApUpden7HF9pLcuQVZ_Bv3Xb1S_NLTcDBYDCVvqcI7i2aEkl0q-FmhLcfGqF8O-vsppChlTE3OJHfHNJqDLLArCJ_HLjLeGdOpyrLKZa4_2oobmOSPl3LbFU2jhEaSP9bukfhTX5Zr3XOkHMJ_98YHzwd9BJYL2XCrzEuv-pRpu8tvBhOQVx0k9DmU8dbcLoxFc2p_DRaiVA_QJ_y_zv6_Gn5-grFf5OpS_3p5JIttgIrvT2sBXSarjtOtpkcsSPKto6oAhYRj14zS8mSzdxfrB4S-4s4Ctu9Vb7m00)

![](https://github.com/SvPolyanskaya/CyberImmunity/blob/Robot-in-Pharmacy/Нарушение%20связи.png)

Упрощение
Чтобы не отвлекаться на систему управления складскими запасами предположим, что это реализовано на уровне аптечной сети - только тем роботам будет передано задание на производство, которые располагают достаточным запасом субстанций
 
задание на производство для конкретного робота-фармацевта

Робот-фармацевт
 
запрос рецепта рецепт

База данных рецептов
![](https://github.com/SvPolyanskaya/CyberImmunity/blob/Robot-in-Pharmacy/Нарушение%20связи.png)

Вариант 2. Лекарства из специального списка
варианты
- входит в список жизненно-необходимых, производство полностью или частично оплачивается государством
- содержит наркотические вещества или прекурсоры для их получения, авторизованное получение такого лекарства должно строго контролироваться
- всё остальное из варианта 1.
![](https://planttext.com/api/plantuml/png/hLRBKXf15DttLtJOMbey71wpIFaXReP7LQnIf6ImAZk5CZ6baMINHHxbnlK47KKG-8NkFygvjvkH6I04AXiSndlFFVVSSxlPQ_hUYTywEfIfLhDMyPgrPae8_y0_hCcKkjKVLAX6Aj1dgg-UPNP7gbzu7kFRa-hXxuC-rsrwacg8q065sbU1f2YfpzKOC7qLgA6-1jXOtICShoUgZq-ae683B0ug1mslxgFk5pK11CEbfDUKZNVUoP5NUPy8-mhC9whpW8UH6kahVR5V1x-GUHF6MFKOeLoDvsRGoQtgwQvwqjSSqJoLKiQ3SWYw8m5q6w1J_e7kxjU9VvyR3TMB2kX51mKfgiTAZF3lBWFdug2xN3b05jHZMUv95CRgHntlnfEAb4J5U113bZyWLMsDOZpSeJbnCB4BzIT3I8NWYH9Zl9pWSsHwYqHouYWqxMyezCBP5a4In8GT4J1sc_tGOqcWmMzk1EFWcJypRZQXVThQg6yjTCLHcNGyB9zeufBZ0qE3C_BnXDAE-a5oSWOHWgeN42jGZr0wd4ainHCBgFITMnf0KMud6aH1U2t_kDuwAjTEO5DhHBdz5ePn9Os1nuxvIVA6DD_GL4SDT9kaWjTd7AaxedcAx9pSCFlm-BWXrK-831leZpmJ0BH9_fbjrLsP4Jd3SsihKIks8cPFQIcD5Lxj2wO4KAvk352k6WRRssuiPrN9tBydrEfLiSivhZJU8vc8uxdTieaTQMW6BBoAVt3g-JLi9WjKj8cpoqNn17GjsNs3wOAAQcqcFNeiYY8XPTBhG4NPS7ucRPdCz3YUBOQOekroMKXH2EkEEpv9Xdps8XehWASHUOceNLYRaRQWWgsLmYZXk6IvrvLZdanzVhVrZLIzgM7fY7Y4wc05IuxmT2Dv56TmR4JG4GvLoRfiMAvmPl4f1sjAjqDeZYZZxd1wluZiLE0DSYC6MIjqThcAMLF9IKGuKVd_Bv3Xb1G_EhJDwh5_SGZIonXXHnXokNNoapjGSgMahJ7qkMVRbxdX3B1PBQAyU0rAecHbsX2hPBKWEZ7vIukydsmYdr3WqkpT4h9vaLyuqscMOP9FrColMCAyeSB3Y9qxmMnATE4dJdmL23xG34Z1vLk1LXdSh8QVxUy4tBp8w9XxOtxN2g8GTRScneA3gV3NWwcmGfF2tAIM7pJs6kGbPceH9lswC_-PYeMNIsRhhDpNTUlCQv8y8UAQE2iqSQQNipjtwKSPRuJOWnlmw_mF)
	
 ### Алгоритм работы решения
  
### Анализ векторов атак и эффекта 
| Название | Назначение | Результат атаки |
|----|----|----| 
|1. Связь|	отвечает за взаимодействие с системой распределения задач на изготовление и с базой данных рецептов|в результате компрометации произошла подмена задания на производство|
|2. Измерение параметров субстанциЙ|контролирует массу и/или объём компонентов	||
|3. Центральная система управления|осуществляет общее управление процессом приготовления лекарства||
|4. Самодиагностика|осуществляет сбор и анализ телеметрии всех подсистем для оценки работоспособности системы||
|5. Перемещение компонентов|отвечает за расчёт траекторий перемещения робота на каждом этапе тех. процесса||
|6. Перемешивание|осуществляет комплекс действий для достижения требуемого уровня смешения компонентов||
|7. Маркировка|изготавливает и наклеивает на ёмкость описание лекарства	||
|8. Стерилизация|осуществляет комплекс действий по стерилизации ёмкости с лекарством||
|9. Нагрев/охлаждение|обеспечивает требуемые по тех. процессу температурные условия для химических реакций||
|10. Приводы|	управляют захватами робота для реализации рассчитанных траекторий и механических воздействий на субстанции (в т.ч. измельчение и перемешивание)	||
 ### Упражнение
Используя пример выше, изобразите развитие атаки через другие скомпрометированные компоненты (по одному в сценарии)

Если в результате развития атаки можно нарушить какую-либо ЦБ, то компонент обязан стать частью доверенной кодовой базы, если нет, то его следует рассматривать как недоверенный код.

Цели безопасности
1.	Выполняются только аутентичные задания на производство

2.	Для производства используются только авторизованные вещества

3.	Продукт имеет аутентичную маркировку



Предположения безопасности
- "доктор плохого не посоветует" - врачи, выписывающие рецепты, благонадёжны
 
Политика архитектуры


Легенда
недоверенная сущность


доверенная сущность


доверенная сущность,
повышающая целостность данных

высокоцелостные данные


низкоцелостные данные


Качественные оценки доменов
Сложность - S (simple), M(medium), C (complex) - простой, средней сложности, сложный
Размер (объём) кода - S, M, L, XL - маленький, среднего размера, большой, очень большой
- простой и маленький
 
 Обоснование уровня доверия доменов безопасности
| Домен безопасности | Уровень доверия	 | Обоснование |Комментарий|
|----|----|----| ----|
|1. Связь|недоверенный|   |    |
|2. Измерение параметров субстанций|недоверенный|   |    |
|3. Центральная система управления|недоверенный|   |    |
|4. Самодиагностика|недоверенный|   |    |	
|5. Перемещение компонентов|недоверенный|   |    |	
|6. Перемешиваниея|недоверенный|   |    |	
|7. Маркировка	|недоверенный|   |    |
|8. Стерилизация	|недоверенный|   |    |
|9. Нагрев/охлаждение|недоверенный|   |    |	
|10. Приводы	|недоверенный|   |    |
 
Домашнее задание: переработка политики архитектуры

Критерии хорошей политики архитектуры:

-	минимизировать размер и сложность TCB под заданные ЦПБ 1-3
-	обоснование уровня доверия приведено в таблице 1.
-	минимальное количество интерфейсов у доверенных компонентов

Другими словами
-	каждый доверенный домен безопасности, особенно "жёлтый", нужно стремиться делать простым и маленьким, количество входящих стрелок следует стремиться сделать минимальным

Что можно сделать
-	декомпозировать существующие домены безопасности
-	добавить новые домены безопасности, обеспечивающие достижение ЦБ при уменьшении размера довереной кодовой базы
-	следует заполнить таблицу 2 на следующей вкладке с описанием новых доменов безопасности и заполнить таблицу 3 с обоснованием выбора уровня доверия
