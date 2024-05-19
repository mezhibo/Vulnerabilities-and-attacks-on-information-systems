**Задание 1**

Скачайте и установите виртуальную машину Metasploitable: https://sourceforge.net/projects/metasploitable/.

Это типовая ОС для экспериментов в области информационной безопасности, с которой следует начать при анализе уязвимостей.

Просканируйте эту виртуальную машину, используя nmap.

Попробуйте найти уязвимости, которым подвержена эта виртуальная машина.

Сами уязвимости можно поискать на сайте https://www.exploit-db.com/.

Для этого нужно в поиске ввести название сетевой службы, обнаруженной на атакуемой машине, и выбрать подходящие по версии уязвимости.

Ответьте на следующие вопросы:

Какие сетевые службы в ней разрешены?
Какие уязвимости были вами обнаружены? (список со ссылками: достаточно трёх уязвимостей)



**Решение 1**

*Сканируем службы*

![alt text](https://github.com/mezhibo/Vulnerabilities-and-attacks-on-information-systems/blob/d15cfd51957c25ace85af9ff158a3a5bf97466fb/IMG/1.jpg)

*Теперь ищем уязвимости на сайте баз уязвимостей*

![alt text](https://github.com/mezhibo/Vulnerabilities-and-attacks-on-information-systems/blob/d15cfd51957c25ace85af9ff158a3a5bf97466fb/IMG/2.jpg)

![alt text](https://github.com/mezhibo/Vulnerabilities-and-attacks-on-information-systems/blob/d15cfd51957c25ace85af9ff158a3a5bf97466fb/IMG/3.jpg)

![alt text](https://github.com/mezhibo/Vulnerabilities-and-attacks-on-information-systems/blob/d15cfd51957c25ace85af9ff158a3a5bf97466fb/IMG/4.jpg)




**Задание 2**

Проведите сканирование Metasploitable в режимах SYN, FIN, Xmas, UDP.

Запишите сеансы сканирования в Wireshark.

Ответьте на следующие вопросы:

Чем отличаются эти режимы сканирования с точки зрения сетевого трафика?
Как отвечает сервер?



**Решение 2**

1. Режим сканирования SYN:
В режиме SYN (также известном как сканирование SYN), атакующий отправляет пакеты SYN на целевой хост. Если порт открыт, целевой хост отвечает пакетом SYN-ACK, указывая на готовность установить соединение. В случае закрытого порта целевой хост отвечает только пакетом RST. Таким образом, сканирование SYN позволяет определить открытые порты на целевом хосте без установления полного соединения.

https://github.com/mezhibo/Vulnerabilities-and-attacks-on-information-systems/blob/7c273f2ef7a23339241768b30ec7d56f62bd1a1f/FILES/SYN.pcapng


2. Режим сканирования FIN:
В режиме FIN атакующий отправляет пакеты с флагом FIN установленным в единицу. Это позволяет проверить, отвечает ли целевой хост на такие пакеты. Если порт открыт, целевой хост не возвращает никакого ответа. При закрытом порте целевой хост отправляет пакет RST. Часто такие пакеты игнорируются многими брандмауэрами и IDS/IPS, поэтому сканирование FIN не всегда дает точный результат.

https://github.com/mezhibo/Vulnerabilities-and-attacks-on-information-systems/blob/7c273f2ef7a23339241768b30ec7d56f62bd1a1f/FILES/FIN.pcapng


3. Режим сканирования Xmas:
Сканирование Xmas является вариацией сканирования FIN. В этом режиме атакующий отправляет пакеты с установленными флагами FIN, PSH и URG. По аналогии со сканированием FIN, при открытом порте целевой хост должен игнорировать такие пакеты, а при закрытом – отправить пакет RST. Однако такие пакеты могут вызвать аномальные реакции в некоторых системах и нарушить стандартные схемы работы.

https://github.com/mezhibo/Vulnerabilities-and-attacks-on-information-systems/blob/7c273f2ef7a23339241768b30ec7d56f62bd1a1f/FILES/Xmas.pcapng


4. Режим сканирования UDP:
В режиме UDP атакующий отправляет пакеты UDP на целевой хост. Если порт открыт, целевой хост должен отправить пакет ответа. В случае закрытого порта нестандартным поведением является ответ целевого хоста ICMP-пакетом с сообщением, что порт недоступен. Поэтому при сканировании UDP нужно учитывать особенности обработки UDP-пакетов на целевой системе. Процесс занимает намного больше времени по сравнению с предыдущими методами, так как проходит по каждому порту последовательно, и выдает ответ что порт недоступен, а так как всего портов 65536 времени уходит очень много на првоерку каждого порта.

![alt text](https://github.com/mezhibo/Vulnerabilities-and-attacks-on-information-systems/blob/a81661fc2231d88545bd915c64329920ad4607a6/IMG/5.jpg)

https://github.com/mezhibo/Vulnerabilities-and-attacks-on-information-systems/blob/be15a9af01383e55caaae88987f943fd30ca869e/FILES/UDP.pcapng
