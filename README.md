# LedPanelWiFi_tasmota
Управление часами LedPanelWiFi через Home Assistant и Matter.

Прошивка LedPanelWiFi очень большая, изменение вносить в неё изменения очень большая работа. Поэтому я решил эмулировать нажатие предусмотренной кнопки через ESP32-C3 Super Mini.

Установка: 
1. Прошиваем tasmota через https://tasmota.github.io/install/. Подключем устройство к WIFI.
2. Задаём пины.
   ![image](https://github.com/user-attachments/assets/2bc01814-6188-4ff3-9a3d-51c7ea32e404)
4. задаём в прошивке LedPanelWiFi пин ддля кнопки.
   ![image](https://github.com/user-attachments/assets/7dc4e148-771d-4343-ba7d-1af50e4aaad0)
6. Подключаем GPIO4(Power5) часы на прошивке LedPanelWiFi.
7. Преходим в консоль и ниже приведённые правала.
   Rule1 ON Power1#State=1 DO Backlog Power5 0; Delay 2; Power5 1;  Power5 0; Delay 1; Power5 1;  Delay 5; Power1 0   ENDON // двойное нажатие
   Rule2 ON Power2#State=1 DO Backlog Power5 0; Delay 2; Power5 1; Delay 5; Power2 0  ENDON // короткое удержание // выключает матрицу
   Rule3 ON Power3#State=1 DO Backlog Power5 0; Delay 2; Power5 1; Power5 0; Delay 5; Power5 1; Delay 5; Power3 0  ENDON //ночной режим
8. Применяем правила.
      Rule1 1
      Rule2 1
      Rule3 1
      Rule4 1
9. Проверяем всё, радуемся.
//Rule2 ON Power2#State=1 DO Backlog Power5 0; Delay 1; Power5 1;  Power5 0; Delay 1; Power5 1;  Power5 0; Delay 1; Power5 1;  Power5 0; Delay 1; Power5 1; Delay 5; Power2 0   ENDON // показ ip, нах не надо
