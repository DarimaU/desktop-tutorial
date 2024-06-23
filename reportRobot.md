# Робот-фармацевт
![](https://github.com/DarimaU/desktop-tutorial/blob/dom_zadanie/%D0%A0%D0%B8%D1%81%D1%83%D0%BD%D0%BE%D0%BA5.jpg)

Учебный пример для курса по кибериммунной разработке

- [1. Учебный пример "Робот-фармацевт](#Учебный-пример-"Робот-Фрамацевт") 
- [2. Краткое описание назначения и применения системы](#Краткое-описание-назначения-и-применения-системы)
- [3. Ключевые ценности, ущербы, неприемлемые события)](#Ключевые-ценности,ущербы,неприемлимые_события)
- [4. Контекст работы системы](#Контекст-работы-системы)
- 
       - [Вариант 1 ](#Вариант-1)
       - [Вариант 2](#Вариант-2)
  
- [5. Высокоуровневая архитектура системы.](#Высокоуровневая-архитектура-системы)
- [6. Цели и предположения безопасности](#Цели-и-предположения-безопасности)
- [7. Компоненты: описание подсистем](#Компоненты-описание-подсистем)
- [8. Основные функциональные сценарии.](#Основные-функциональные-сценарии) 
- [9. Негативные сценарии](#Негативные-сценарии)
- [10. Анализ векторов атак и эффекта](#Анализ-векторов-атак-и-эффекта)
- [11. Упражнение.](#Упражнение)


## 1. Учебный пример "Робот-фармацевт
![image](https://github.com/DarimaU/desktop-tutorial/blob/dom_zadanie/image.jpg)

Продукт - робот-фармацевт, который производит лекарство по индивидуальному рецепту.
Рецепт включает в себя
а) точный состав и количество компонентов, порядок и условия изготовления конечного продукта
б) уникальный идентификатор лекарства, который изготавливается в определённом объёме для индивидуального курса лечения
Основные этапы процесса изготовления лекарства по рецепту

![](https://github.com/DarimaU/desktop-tutorial/blob/dom_zadanie/%D0%9E%D1%81%D0%BD%20%D1%8D%D1%82%D0%B0%D0%BF%D1%8B.png)

## 2. Краткое описание назначения и применения системы

а) Робот-фармацевт управляется центральной системой по беспроводному интерфейсу

б) Робот-фармацевт передаёт состояние в центральную систему

### 3. Ключевые ценности, ущербы, неприемлемые события
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

## 4. Контекст работы системы
### Вариант 1. Лекарства общего назначения

- Не предполагает льготного получения, не является наркотиком, не предполагает существенных ограничений для клиентов.
Однако лекарство может быть очень дорогим или с очень коротким сроком годности, поэтому клиенту важно получить свежее лекарство в минимально достаточной дозировке

![](https://github.com/SvPolyanskaya/CyberImmunity/blob/Robot-in-Pharmacy/-Контекст%201.png)

***Упрощение***

Чтобы не отвлекаться на систему управления складскими запасами предположим, что это реализовано на уровне аптечной сети - только тем роботам будет передано задание на производство, которые располагают достаточным запасом субстанций

 ### Вариант 2. Лекарства из социального списка
***Варианты***
-	входит в список жизненно-необходимых, производство полностью или частично оплачивается государством

-	содержит наркотические вещества или прекурсоры для их получения, авторизованное получение такого лекарства должно строго контролироваться
-	всё остальное из варианта 1.

  ![](https://github.com/SvPolyanskaya/CyberImmunity/blob/Robot-in-Pharmacy/-Контекст%202.png)

## 5. Высокоуровневая архитектура системы 
![Высокоуровневая архитектура системы.](https://www.plantuml.com/plantuml/png/RPC_RnD14CNx-nGZqq0HS_vlImY5ZeAFaCO20v628oK7jCb5YK29P4eA4AAXNYuSFkpu_1NUV2FUxdab5csn8ptllD--6UlsJxFfIVRspL6I7MP7CsdXavxf9IhDKMAbkLxe6OoWq6izHuqLporgSR_NAB3HXTn_-kp90tdNJjjfsagIazdpR3f_HTozzwyFCr8xRS5tCXPOwarBfgVoylYu4sdiil4pbhX3INw93IgKSZ0NmHR6Hd5NUVEuwBbUu2Th3iCaL-p-u_5TYV1xvF-mN8SmMEiDDWGl3kOShtAaaayO8NZhMWgico2wyEXUXDot8xfuDNunXy4jJRKbKgrWMh9pzoFk0TtVcfdTW1_zx1pTxVmEMzPD4ztExhCC8hJXVxGF91Km3T4RXn7ZYCOlRiyhLCsERNHl6KKiOpktvkwr2ckU9G5N_wvh7B5DQFjgb-H25W_v7wFMIm8CVdE1PHXs4a5qKZkcUxQmIzThtzr9awJzQ6_liHE9BU9bpyekfLSiihiR16eOg56WnawHOaK_k9fODV2AKImgbADGZaCv2IGherlPJVPdynVyLly2)

 ## 6. Цели и предположения безопасности
 
*Цели безопасности*

 - Выполняются только аутентичные задания на производство
 
*Предположения безопасности*

- "доктор плохого не посоветует" - врачи, выписывающие рецепты, благонадёжны.
 
## 7. Компоненты: описание подсистем

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

## 8. Основные функциональные сценарии
![](https://www.plantuml.com/plantuml/png/pLFDpfD05DtFKzom_OA9MnQchpAb99AqqC2mS4TfrHXDrAqRzGqgbeZMuYlSUIFFPJerj8s9EpUKJC_FcNEvizBembIh9GLLcSIwJCf0APEQPK81VxOlkECJxstDFN-dnu-8F_B0HxkrB-KVd7R4Hxp-493Ts8PRtXCmN-mh77_bWKI0lydJa-nRcEZOv0LCFe3Voxbj0j8bnSiqoOnQ8rSQfskT6GyIgXXvM9R6Lx1t_0i9kWje_LGNAnq_kuAzbq0Iyu2N4vnVs-U4EtRZVKLYu7OKM6YZvsX5_MzvfWAVf70UR1FQtJYjdtWAjpsNMkJptA3pokHPjPedXLAkPmgVdAD7X9W3p3TsYmc_WQjeO5W4cNgStbuvhB1yb6YIbBYNQkJdu8OAXPthIUvXwplVY_AzGDT5ZVvHO2HDKqcZI5I3ifb41DoZAFI63myHEJItWDQYFv6uc7Z6BVxAnUD1yFUxxuBDaCxGByg-xI8CGHhu83C6nQ_TdpXkae0vxTu3RVEN7LLApP9iWTN_3G00)
![](https://www.plantuml.com/plantuml/png/bLFDZfH04BxtKrIuRZ3noi7ig_ImdKZ2m0IQWpTWLetHPFLclAXlWEEIHSTbNg7gZQngbiumCKxcCaFW-_dgg-xhqkh2LkiKWgeqiIvD6IXb4viQ2F0xlS4U7x6Z6WVy1S-V0Nx54VUqfRVkou0zu9uVVmk86cfnXnqmvWUzuzS_SGGHm0VvdKbqnoOwjdd19b-OFyXxQWFG9SHfOZAhDfmhYPEDpgm7CLMCPbYMn2UmZtZW1Bq7RLxgOgtZLoUmRv8FHsf3kdN3_S7EZRfxob3ag_mqmYUPGcQxvuT7ZlkUNWDpUySKtn5tZdsZhLvnbJnZPVEiMgzCeTGK6C8NJnD6m357rcbeour-e5P2I3d0EMhNLgScBBFyB5TNqS8MS91ovEz-gf4rRgUc91JL_zYGcjMEbIFPsq6qdTBURvZgkJ3iGbPly22dmAso5IJTBGHTVP9J2dEA8pNBhhhpiJcbqga5NfVdAIVjFIAXFyWfc-e_oYmH5vQqLIOj3U3d2thoVdwfqOL5ppm8VUX5B6Mo6pNR72qZ3ADpUvlEXWDAnuCioKct_xcRIbsp8z_ulm00)

 ### Основные сценарии производства лекарства
![Описание Сценариев:](https://www.planttext.com/api/plantuml/png/hLRBJXj14BpFLqny3_BxTOZua5msZgKW6MDvRQJSi2q84GHop25Hn2NdmS7W-FaBCt-KwkxPnRiOHKQvm7hSrTrLNTFh_R0NT7lzmvREzCDc8mYROKQfta6lrTGPU-FExCGkhN4dTch_wDoUjZ_nlCAd1pl6_pitS4DwqdQEq1c5-YEZyVsj-upZt_GzqW14oJvnqgcxHgaEoXyq3Zf1kuU2N-qQMCwJqK6eEn-2xc7G-9WCepPkxDXTsmTtoN7XSIfJ0I6_g8mRebzZv-wIIr-_RMitGEq1rrbOGmSZbAMeCPEGrYXj8Pcqo7KDK20E2Go8BUsASqtZdej9K9L0L8mrdBDo1hf6DQh9y199pC7KtOJbGqDsWZvHOeN3DVukXHkUnfobbCoIHvPlABHWjC-WASMQXsauzv17EMP9eC4j4p78UqRJvhpvbF9Pxu2fd_u5H-MooR1oYiGvnnjfWn7b9A2sPt-Gd8oWXg3gASGozXvAJpQ0jIImWahVcT8CYZATU10L5VHxH-t-uRjc5_RmLjAlty0kTKrZuB5ZVcnEBPz0QcHdRaXIhJGrn9S0ldGZ5Hu3NdWXk4Yb0HQPwGXWc54CjVRTJuIBAb1qrKTlceU227sfMTrPP41L9KGkkmiab_LLw8gAdUnA4XLIXwfrTDJHTAl8wdDgV8K0p0XFIs9BDK-z44GRDM0h8LAgaoIFZk3otD5JwxahRSUHeEJWUoY5Dh0tbdYwqYpV2LANA7M-hhdDXL0McWY4TT0MRC_N1aBGtedMbSf7Ohq0AwhbKmBb8vwRXwMupFzdBssabOqNXfYK3OKBI8U-dS8k29vUhQurkLMwP6g-VLcYaaqiJPtLFEjTCCA6AYK4h6tp8ZTLJj4u5ukhybR9es-bJ3cLiFni5HOhSJNDPbIy_bCBm1gbckttIf9KwlBwc_7xnSlmnRyri8U16CaQYOTRYLdi21I2bHINohC4dx-PVgyXcAl4I7V1rto3B0x_wVJTiZrw-ybjsig2Dtfg1ST1hvJQnp3mA-Sl)

 ### Вариант 1. Лекарства общего назначения
![](https://planttext.com/api/plantuml/png/hLPDKnf14BtFhvXmZmMB-yKXvG_9PODKXIf5obsioasXDAOqccCEIQMyvBmIKG82Vs7c7-Lrpx1X5mY5bOiEGx_krwy_XhquYOwJpk61B7NYHZsA6t59YAIP73HaITtf2pLG4vNgKpLKlsLbHweVE4_nwKdryVz1d-akdQGQmtH4flOgbVZ-Nd_2zI_w7cu08cSVsUbGto9K6-6RzMOxQYK8-4NDW6K_9Hd5ilq-EZwCwX_oPaJZJlNrhNhIrsmNdqWf2ywgiFf9aNGNb5CrrjSS_VPjI-epX3_ZKCygfOiU8fDLd_CmxCXpDUzqbqEdG25tg90YjucQigzXHdit3me8HC5OnZ6BbqBQUOmWR-wIocnCx0Qi80Yf0NWYn1INC_oTcDnmwhCND-_5WPUl2FJCQEj1aeiPrpDbtrskPfybWGRtd4WAlnTKSFRh5CGlsoOOsWQuOgjAEM_c5PAuPFlKq624bmU4E-exoSa88WHLpo5MgXwXz6016EQ1FY9zuvH6K9JJoGhXYwYJ7BKwX-yQnsWFsqtozHjqJ4rI6RZig1_tfpIVa5HFZNINf9fA8iHpWDRKFH6V05sLBqJlKkngJHgTwGfWTAFfg9cbFp39YAYUD4-Yf84kh18miC35HY9xSdGjMUdHl1d5VcC1dXq34P2dIdaRLnaQLQwKBHEQQjD-QheO33Q1pNATII24E3WwQjE0qjICIO8fh55kd2Qa6r4xjvAIWA223iMG6odS6kdxjx-OA7DVRcHz8rL_NXsQXqV83bfOH1ESRYJNuXJboHYwmgKeJaro1iz69wCDCEX9aCGyyJn2FTffyrKedBd2By1c31ohjBDUHiT4SWiMRXR-_mjaE1N5ppQK6GfkO4myNUO8kyAGgsw3Bmv1M9EIniRGvvnjNcQT6yTcjeZowZa8HMXbUg6lq6f1T7BoXwkQlvY4Lr3WqWpU6hAUy5RMT8uoJBn2J6_357g62XSZjtZIHKZskXNMcqg5QBJsxJZwDVF0Z_Zvj1f-jeyYdXaWUcP9Bi-QB_mikorzhDXC_Zytaxz14t-fKkiNZTtvFCHCBVEfhtXrBOY5opMrTJVEwxPnbZKfReYy9ku6JLmZ1B-OXHSkGxmIOW_TW1-IVm00) 

 ### Вариант 2. Лекарства из социального списка
![](https://planttext.com/api/plantuml/png/hLRBKXf15DttLtJOMbey71wpIFaXReP7LQnIf6ImAZk5CZ6baMINHHxbnlK47KKG-8NkFygvjvkH6I04AXiSndlFFVVSSxlPQ_hUYTywEfIfLhDMyPgrPae8_y0_hCcKkjKVLAX6Aj1dgg-UPNP7gbzu7kFRa-hXxuC-rsrwacg8q065sbU1f2YfpzKOC7qLgA6-1jXOtICShoUgZq-ae683B0ug1mslxgFk5pK11CEbfDUKZNVUoP5NUPy8-mhC9whpW8UH6kahVR5V1x-GUHF6MFKOeLoDvsRGoQtgwQvwqjSSqJoLKiQ3SWYw8m5q6w1J_e7kxjU9VvyR3TMB2kX51mKfgiTAZF3lBWFdug2xN3b05jHZMUv95CRgHntlnfEAb4J5U113bZyWLMsDOZpSeJbnCB4BzIT3I8NWYH9Zl9pWSsHwYqHouYWqxMyezCBP5a4In8GT4J1sc_tGOqcWmMzk1EFWcJypRZQXVThQg6yjTCLHcNGyB9zeufBZ0qE3C_BnXDAE-a5oSWOHWgeN42jGZr0wd4ainHCBgFITMnf0KMud6aH1U2t_kDuwAjTEO5DhHBdz5ePn9Os1nuxvIVA6DD_GL4SDT9kaWjTd7AaxedcAx9pSCFlm-BWXrK-831leZpmJ0BH9_fbjrLsP4Jd3SsihKIks8cPFQIcD5Lxj2wO4KAvk352k6WRRssuiPrN9tBydrEfLiSivhZJU8vc8uxdTieaTQMW6BBoAVt3g-JLi9WjKj8cpoqNn17GjsNs3wOAAQcqcFNeiYY8XPTBhG4NPS7ucRPdCz3YUBOQOekroMKXH2EkEEpv9Xdps8XehWASHUOceNLYRaRQWWgsLmYZXk6IvrvLZdanzVhVrZLIzgM7fY7Y4wc05IuxmT2Dv56TmR4JG4GvLoRfiMAvmPl4f1sjAjqDeZYZZxd1wluZiLE0DSYC6MIjqThcAMLF9IKGuKVd_Bv3Xb1G_EhJDwh5_SGZIonXXHnXokNNoapjGSgMahJ7qkMVRbxdX3B1PBQAyU0rAecHbsX2hPBKWEZ7vIukydsmYdr3WqkpT4h9vaLyuqscMOP9FrColMCAyeSB3Y9qxmMnATE4dJdmL23xG34Z1vLk1LXdSh8QVxUy4tBp8w9XxOtxN2g8GTRScneA3gV3NWwcmGfF2tAIM7pJs6kGbPceH9lswC_-PYeMNIsRhhDpNTUlCQv8y8UAQE2iqSQQNipjtwKSPRuJOWnlmw_mF)

## 9. Негативные сценарии 
### Негативный сценарий получения (последовательности выполнения операций), при которых ЦБ нарушаются
![](https://github.com/SvPolyanskaya/CyberImmunity/blob/Robot-in-Pharmacy/Нарушение%20связи.png)

 ### Негативный сценарий производства 1
![](https://planttext.com/api/plantuml/png/hLPDRzf04BtlhzZISoemiOqvLFaVRGykiLIaX20maNfBG4bJ9KrwxA5LbKlF3Yq9XG1_OVSVzStiuc83HKIz9Cioy-RDcuzbhns7hRXpU20BdNPK2zjHko14N8yF8bbGj_fS3TH49Vf43TLlMNeXrNUSf_ZqeFhu_qkVwYwTf1h3T4IczYgH-FvEVyJrJ_eUC70Yi0yCEjGt2DL4-7gjtWmRCG9-LZFuCav1XctPV1Us3iFQ-wmPqRXLVNsZ7lGLsxMFfNpUYlPb3h0ConyKJNT1Er5ZVSKCRbutf3u5XLCEzwWIkkWXEbdrEHV3aD3BMT1T3f_02_b3YGJvJTIKiOOfzTsiKuMSA1XBEMO14yWxZr79chkaD1iJkm6h249g09u8CSNb37yd9ZUS-epYPb4Se7n1e4VsjWYI86PSquInkrpHFai23UuuaGIuvrHqndLo1IZQHXZQ9hXagr8nQ-RbahXW-yJGO0ylwn2yKDz8JlOWGb3r368bwXvA3nOSWwoZZqXVEQKH5ELqqaBu8kp4HutEuTkeXVQm7ILtNg9hgfBAm6L7_RX7fVc4f7fgfBiarLGI8Pu5jAVk2RJRpYlgjpT0ASidekmIXt9L6htf2ixeIjDPCvl6m2GbmbfSFmxZ2DrO9iUATLniAB8de2l9Ye_cJIdsemNtz5WH5K8g5RU1IhrHxLBHCg49Dssefel1O5EnMQupgGWX3ewEccP-CQqqGcFIOGeNr1wd2Ob7_CwihgGY-A1TCV563xTA8lzjDcRB2IntjRwMgZyl4Gt7FRG7Dsoc2KxNaWjoWXgbD5tXKXIdAZcDHoEM4GW-Q52Gn73nS492MdBptIYSkSnFy4qPE5PkPxsMZedavYpSDFp_5yXmoekVhYip6Tp567-wp11sXI5NtiO_Fmb1LKgQ7KEVSxPvcTrkWCs04UNLmn28mChqHAp0Qa5qCl87goOWduINK-32JDyQifxmLjPqxcMOUBcOtePHz0mLBaPc-oIBBkbJbzjnAX4YQkpRSVIhviKVyLjgDVnaNqYyEV3ecKsvF6k-yDFijiHOiPxyVwudVuCc_bAbrYyQk_XvY9bQYgalUNKjY8NBDRLrDyxhjd6MDSblYAmcxWPDN18YVV_u5SszTgdZCo7sq1JuWVa7)

 ### Негативный сценарий производства 2
![](https://planttext.com/api/plantuml/png/hLPDKnf14BtFhvYGeuKbuEu21yl_4NDOXQfGfKZ1QbLkYcLYIYF9BOTyb1VF6tGLKU0lpFoZlEuPrjrLGh1oWMNfVltwzUlPNUy4VZlOszcMkRrEVSllr3iv8O96i5sNENMXFwX8ZLIe3zH0tSdYibI_S3t6hrlLn_UrFjHTkfBg7g532hMtGabHKX-gCM06AbJt-WnWOtM5SDoUg04-aOAABR1eR3LQVZD0tIzg0WY6oqc_8rll_FQEl_K-4_OLcBTKvneN8pNIf_fuemb-4VCcZB7gCy9cBPrRG2SNggzxwbQVSKHdNyhNxNfDfWDB2Bma4NGNmDCUGjtRQ58F0susKWygf1j7A4fHVLPZXBzx35vAWwvozH1PK92bkI9X66iGTxsQJYfJ4XNZOTpp249IrjOefyCTcXK74xj8VpA4L0IUA376pGa-HwQtM2WdZK8J_uP23vnj4IH1JDWL8MDtsHDzbWGQ_EP6C1AU-ntZ5ZFwhrWh3QoDJZcgi98ESpDDd71yQ6XmXfjEg2oh7oGdPn0Xg7eCiK9r0wMZH68bdUYXqdTkQGX5kPru49xmzuBTvjxEPhqDgrepolmQJ5ELD0OUE-OdoHlI_49JHsgekoGL_9vmfJuIS5l-3TdjBL1AyeKesxkxBMDQzHEAmnFw8my8A5sQHM9zTKyMHCcGNbhA54pjZ5bSsbBZYqSlC-qrBDEB0JPhXa4-Nqtbp2jP-lU4UhCcLZcdAeqHIIlYU6XNRcBd6vbf2tyhQEpxGHrhoWALRM9oqoYUWCuaMt4utLPHgoVIuykoA1DIOMKHg3WRQr1OiKmIFOwJnH1JjbtE2YaBaRJ89PyjztmY8mLBWQiHkOhu7Ll3aS3WWpsMmiZXLCbyZql8P9d_qstNvrBrfzQbG-C6qeCQV3d2rRdaUHp0kp5BHpXKfLXbrtA50ujFELXSUcP4vj0o5e-cJnrHdAhyWjoOGT6gNPmjPT5KSZ8HJbp-_mjaE6N5ZuznitziOXoBT3D5s166N6cH_EmYLAfIqkeO-jopxSiyymomsI-Y_FmkL4J5olH2h8hLWkYavAyyjm3P9joC0YTc-MQGTONxx4odMOQ9cwdfpjb4rr3XOQGEdp2P4hy2PCv-5Ge-rGo8L-Nd0wqok5aDFzit1poBaN5adY1FTyqJNjpTWXZFd4xUNqydRuuctfD9pJvex0EHbvYfnPZqpcV-cOg5cpDcwypTrqNhFDKaUqAaDN7cQEAG4F5x0RzTPDu2uiHNGgp357Xr_mC0)

## 10. Анализ векторов атак и эффекта 
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

## 11. Упражнение
Используя пример выше, изобразите развитие атаки через другие скомпрометированные компоненты (по одному в сценарии)
Если в результате развития атаки можно нарушить какую-либо ЦБ, то компонент обязан стать частью доверенной кодовой базы, если нет, то его следует рассматривать как недоверенный код.

Цели безопасности
1. Выполняются только аутентичные задания на производство
2. Для производства используются только авторизованные вещества
3. Продукт имеет аутентичную маркировку

Предположения безопасности
"доктор плохого не посоветует" - врачи, выписывающие рецепты, благонадёжны
Политика архитектуры

![](https://github.com/DarimaU/desktop-tutorial/blob/dom_zadanie/%D0%A0%D0%B8%D1%81%D1%83%D0%BD%D0%BE%D0%BA7.png)
![](https://github.com/DarimaU/desktop-tutorial/blob/dom_zadanie/%D0%A0%D0%B8%D1%81%D1%83%D0%BD%D0%BE%D0%BA6.png)
 
 ***Обоснование уровня доверия доменов безопасности***
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
 
### Домашнее задание: переработка политики архитектуры

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
