# Домашнее задание к занятию «`Уязвимости и атаки на информационные системы`» - `Игонин В.А.`


## Задание 1
Скачайте и установите виртуальную машину Metasploitable: https://sourceforge.net/projects/metasploitable/.

Это типовая ОС для экспериментов в области информационной безопасности, с которой следует начать при анализе уязвимостей.

Просканируйте эту виртуальную машину, используя nmap.

Попробуйте найти уязвимости, которым подвержена эта виртуальная машина.

Сами уязвимости можно поискать на сайте https://www.exploit-db.com/.

Для этого нужно в поиске ввести название сетевой службы, обнаруженной на атакуемой машине, и выбрать подходящие по версии уязвимости.

Ответьте на следующие вопросы:

Какие сетевые службы в ней разрешены?
Какие уязвимости были вами обнаружены? (список со ссылками: достаточно трёх уязвимостей)
Приведите ответ в свободной форме.

## Решение 1

`SSH` - протокол удаленного управления компьютером через зашифрованный туннель. В Metasploitable открыт порт **22** для SSH.

`FTP` - протокол передачи файлов, который позволяет пользователям копировать файлы между удаленными системами. В Metasploitable открыт порт **21** для FTP.

`Telnet` - протокол удаленного управления компьютером без шифрования трафика. В Metasploitable открыт порт **23** для Telnet.

`Apache` - веб-сервер, который обслуживает веб-страницы и другой контент. В Metasploitable открыты порты **80** для Apache.

`Samba` - набор программ, который позволяет обмениваться файлами и печатать на удаленных системах. В Metasploitable открыты порты **139** и **445** для Samba.

`PostgreSQL` - система управления реляционными базами данных. В Metasploitable открыт порт **5432** для PostgreSQL.

`MySQL` - другая система управления реляционными базами данных. В Metasploitable открыт порт **3306** для MySQL.

`Rlogin` - протокол удаленного управления компьютером без шифрования трафика. В Metasploitable открыт порт **513** для Rlogin.

`Portmap` - служба, которая помогает клиентам находить нужные RPC-сервисы. В Metasploitable открыт порт **111** для Portmap.

![alt text](https://github.com/Sayward-k8/sdb-hw-13-01/blob/main/img/1.1.1.png)
![alt text](https://github.com/Sayward-k8/sdb-hw-13-01/blob/main/img/1.1.png)
![alt text](https://github.com/Sayward-k8/sdb-hw-13-01/blob/main/img/1.3.png)
![alt text](https://github.com/Sayward-k8/sdb-hw-13-01/blob/main/img/1.4.png)
![alt text](https://github.com/Sayward-k8/sdb-hw-13-01/blob/main/img/1.4.1.png)

[ProFTPd IAC 1.3.x](https://www.exploit-db.com/exploits/15449)

[ProFTPD 1.3.1 - Telnet IAC Buffer Overflow (CVE-2010-4221)](https://www.exploit-db.com/exploits/16851)

[ISC BIND 9 - TKEY](https://www.exploit-db.com/exploits/37721)

[vsftpd 2.3.4](https://www.exploit-db.com/exploits/17491)



## Задание 2
Проведите сканирование Metasploitable в режимах SYN, FIN, Xmas, UDP.

Запишите сеансы сканирования в Wireshark.

Ответьте на следующие вопросы:

Чем отличаются эти режимы сканирования с точки зрения сетевого трафика?
Как отвечает сервер?
Приведите ответ в свободной форме.



## Решение 2

1. SYN-сканирование (-sS)

  Отправляются TCP-пакеты с флагом SYN. На открытые порты приходят ответы SYN/ACK, после чего сканер отправляет RST, не завершая соединение.
  
  Открытые порты - SYN/ACK, закрытые - RST/ACK.

![alt text](https://github.com/Sayward-k8/sdb-hw-13-01/blob/main/img/syn.png)

2. FIN-сканирование (-sF)

  Отправляются TCP-пакеты только с флагом FIN.
  
  Открытые порты игнорируют пакет (нет ответа), закрытые отвечают RST/ACK.

![alt text](https://github.com/Sayward-k8/sdb-hw-13-01/blob/main/img/fin.png)
![alt text](https://github.com/Sayward-k8/sdb-hw-13-01/blob/main/img/fin2.png)

3. Xmas-сканирование (-sX)

  Отправляются TCP-пакеты с флагами FIN, URG, PSH.

  Открытые порты молчат, закрытые отвечают RST/ACK.

![alt text](https://github.com/Sayward-k8/sdb-hw-13-01/blob/main/img/xmas.png)
![alt text](https://github.com/Sayward-k8/sdb-hw-13-01/blob/main/img/xmas2.png)

4. UDP-сканирование (-sU)

  Отправляются пустые UDP-пакеты.
  
  Открытые порты не отвечают или отвечают по протоколу, закрытые возвращают ICMP "Port Unreachable".

  ![alt text](https://github.com/Sayward-k8/sdb-hw-13-01/blob/main/img/udp.png)
