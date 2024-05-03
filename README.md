# Test_script_Jmeter

Пример скрипта для нагрузочного тестирования сайта webtours.load-test.ru (WebTours45.jmx)

Скрипт, выполняет следующие действия:

1. Открытие главной страницы "root" по http://webtours.load-test.ru:1080/webtours (в запросе root/cgi-bin/nav.pl-5 вытаскиваем userSession с помощью Regular Expression Extractor)
2. Вход в систему "login" под заранее созданными пользователями с помощью CSV Data Set Config (вход в систему (запрос login/cgi-bin/login.pl-6) можно проводить либо с помощью тестового логина/пароля из файла и переменной userSession из предыдущего запроса, либо поставить заглушку на запрос и получать всегда один ответ "Autorized!", заглушка развёрнута на локалхосте с помощью WireMock, http://localhost:8080/__admin/mappings или создать с помощью Spring boot и Java)
3. Переход на страницу "Flights", выбор случайного города отправления и прибытия (вытаскиваем список городов из запроса flights/cgi-bin/reservations.pl-11  и перебираем их с помощью Regular Expression Extractor)
4. В половине случаев скрипт должен покупать билеты "туда", а в половине случаев "туда-обратно" (распределяем пропорции с помощью Counter, If Controller и Regular Expression Extractor )
5. Покупка билета (подставляем все необходимые переменные в параметры запроса payment/cgi-bin/reservations.pl-17)
6. Переход на корневую страницу
