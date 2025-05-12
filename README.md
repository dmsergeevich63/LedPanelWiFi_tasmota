# LedPanelWiFi_tasmota
Управление часами LedPanelWiFi через Home Assistant и Matter.

Прошивка LedPanelWiFi очень большая,  вносить в неё изменения очень большая работа. Поэтому я решил эмулировать нажатие предусмотренной кнопки через ESP32-C3 Super Mini.
![image](https://github.com/user-attachments/assets/8d1660d1-6fbe-4c73-afb5-056218917b9e)

Установка: 
1. Прошиваем tasmota через https://tasmota.github.io/install/. Подключем устройство к WIFI.
2. Задаём пины.

   ![image](https://github.com/user-attachments/assets/2bc01814-6188-4ff3-9a3d-51c7ea32e404)
4. задаём в прошивке LedPanelWiFi пин для кнопки.
   ![image](https://github.com/user-attachments/assets/7dc4e148-771d-4343-ba7d-1af50e4aaad0)
6. Подключаем GPIO4(Power5) ESP32-C3 Super Mini r часам на прошивке LedPanelWiFi.
7. Преходим в консоль и вводим ниже приведённые правила. 
   Rule1 ON Power1#State=1 DO Backlog Power5 0; Delay 2; Power5 1;  Power5 0; Delay 1; Power5 1;  Delay 5; Power1 0   ENDON // двойное нажатие
   Rule2 ON Power2#State=1 DO Backlog Power5 0; Delay 2; Power5 1; Delay 5; Power2 0  ENDON // короткое удержание // выключает матрицу
   Rule3 ON Power3#State=1 DO Backlog Power5 0; Delay 2; Power5 1; Power5 0; Delay 5; Power5 1; Delay 5; Power3 0  ENDON //ночной режим
9. Они написаны смотря на описание действий. https://github.com/vvip-68/LedPanelWiFi/blob/258eb5e8a8434ced2d78e93a1d32cdb76f0bd9ca/README.md?plain=1#L172
![image](https://github.com/user-attachments/assets/ed28a510-e50d-48b7-8a06-852556a53fac)
11. Применяем правила.
      Rule1 1
      Rule2 1
      Rule3 1
      Rule4 1
12. Проверяем всё, радуемся.
13. Не знаю почему, но для корректной работы нужно чтобы перед запуском правил 1-4 необходимо сначало включить GPIO4(Power5).
14. 
![image](https://github.com/user-attachments/assets/67162830-c557-4b19-8025-fe47844571c8)


Правило, которое мне не понадобилось.
//Rule2 ON Power2#State=1 DO Backlog Power5 0; Delay 1; Power5 1;  Power5 0; Delay 1; Power5 1;  Power5 0; Delay 1; Power5 1;  Power5 0; Delay 1; Power5 1; Delay 5; Power2 0   ENDON // показ ip, нах не надо
