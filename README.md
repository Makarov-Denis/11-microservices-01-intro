Домашнее задание к занятию «Введение в микросервисы» «Макаров Денис»
Задача
Руководство крупного интернет-магазина, у которого постоянно растёт пользовательская база и количество заказов, рассматривает возможность переделки своей внутренней ИТ-системы на основе микросервисов.

Вас пригласили в качестве консультанта для оценки целесообразности перехода на микросервисную архитектуру.

Опишите, какие выгоды может получить компания от перехода на микросервисную архитектуру и какие проблемы нужно решить в первую очередь.

Решение

По описанию задачи существующий интернет-магазин является монолитом, а значит масштабироваться он может только вертикально - повышение характеристик сервера/ов (если выделенные) или выделение большего объема ресурсов (если виртуальные или облачное решения), что может стоить достаточно дорого, а также есть предел развития, ограниченный доступными мощностями дата-центра. Если рост пользовательской базы и количества заказов существенный и не прогнозируется его замедление, то у данного проекта просто нет выбора - ему придется переходить на микросервисную архитектуру. Иначе либо интернет-магазин когда-нибудь схлопнется из-за катастрофической нехватки ресурсов для нормального функционирования, либо затраты на его содержание (оплата "железа") станут отъедать всё большую часть бюджета. В остальных случаях действительно нужно оценить затраты на внедрение и поддержание новой архитектуры.

Преимущества, которые можно получить:

При внедрении микросервисной архитектуры интернет-магазин главным образом получит возможность гибкого масштабирования, а именно: разделив монолит на функциональные сервисы каждый из них можно будет запускать в нужном количестве, распределяя общую нагрузку их функционала между нодами, причём процесс распараллеливания возможно автоматизировать благодаря технологиям мониторинга и IssC (инфраструктура как код). Последнее в свою очередь может оптимизировать затраты на оборудование при использовании облачных провайдеров: создавать дополнительные ноды при исчерпании возможностей существующих и удаление при снижении нагрузки или реализовать создание/удаление нод по расписанию, обеспечив дополнительные мощности в пиковые часы работы;
Микросервисная архитектура позволит подобрать наиболее подходящие средства реализации сервисов, так как в отличии от монолита для каждого сервиса можно использовать разный стек технологий (язык программирования, тип базы данных и т.п.);
Изолирование функционала в сервисе позволяет чаще его обновлять, не дожидаясь готовности остальных частей монолита;
В монолите сложнее реализовать устойчивость к ошибкам - ошибка в одной функции монолита может привести к сбою всего интернет-магазина, когда в хорошо реализованной микросервисной архитектуре в худшем случае будет заблокирована только часть функционала, а в лучшем ноду можно будет перезагрузить/пересоздать и она вернётся в стабильное состояние.
Однако, нужно учесть следующее (сложности):

Еще до внедрения микросервисной архитектуры нужно определиться с протоколами взаимодействия сервисов между собой и клиентами - каналы связи, синхронный/асинхронный режим обмена данными. При неудачном выборе придётся либо одномоментно обновлять все сервисы (аналогично монолиту, а для этого где-то разворачивать и тестировать дубликат интернет-магазина), либо усложнять разработку реализовывая в сервисах сначала оба протокола обмена, потом когда все сервисы будут готовы обновлять ноды и "выпиливать" старый протокол;

Увеличится стоимость обслуживания интернет-магазина, так как сама архитектура более сложная в реализации и требует больше внимания и компетенций (знаний/умений/опыта) при разработке - учесть при расчете стоимости внедрения и дальнейшего обслуживания и прогнозируемой прибыли от внедрения;

При реализации можно "скатиться" в один из антипаттернов (например, излишнее дробление функционала на сервисы действительно микроразмера, что лавинообразно увеличивают сложность всей системы);

При частом обновлении, особенно в наиболее востребовательном функционале есть риск потери актуальности документации, когда имеющаяся по сервису информация соответствует не работающей, а устаревшей версии сервиса. Это чревато сбоями в других связанных сервисах, которые не учитывают внесенные изменения (особенно актуально, когда команды разработчиков разные).

Для внедрения микросервисной архитектуры без качественной проработки будущей архитектуры лучше не начинать. Однако, делить монолит на кусочки гораздо проще чем разрабатывать архитектуру с нуля - это можно делать постепенно, выделяя из монолита один функционал за другим. При этом на начальном этапе ещё можно малой кровью поменять протоколы связи между сервисами.
