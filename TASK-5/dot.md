    digraph SmartHome {
      rankdir=TB;
      node [shape=rectangle, fontname="Helvetica"];
    
      start [label="Başla", shape=oval];
      active_check [label="Sistem aktif mi?", shape=diamond];
      exit1 [label="Sistem kapalı\nBekleme", shape=rectangle];
    
      sensor_loop [label="Sensörleri oku", shape=rectangle];
      motion_check [label="Hareket sensörü?", shape=diamond];
      door_window_check [label="Kapı/Pencere sensörü?", shape=diamond];
      resident_check [label="Ev sahibi evde mi?", shape=diamond];
      alarm_level [label="Alarm seviyesi belirle", shape=rectangle];
      activate_cam [label="Kamera aktivasyonu"];
      send_notify [label="Bildirim gönder"];
      false_alarm [label="Yanlış alarm kontrolü", shape=diamond];
      reset_alarm [label="Alarm sıfırla", shape=rectangle];
      continue_alarm [label="Alarm devam etsin mi?", shape=diamond];
      wait_loop [label="Bekle ve tekrar kontrol et", shape=rectangle];
      end [label="Bitiş", shape=oval];
    
      start -> active_check;
      active_check -> sensor_loop [label="Evet"];
      active_check -> exit1 [label="Hayır"];
      exit1 -> start;
    
      sensor_loop -> motion_check;
      motion_check -> resident_check [label="Evet"];
      motion_check -> door_window_check [label="Hayır"];
      door_window_check -> resident_check [label="Evet"];
      door_window_check -> alarm_level [label="Hayır"];
      resident_check -> reset_alarm [label="Evet"];
      resident_check -> alarm_level [label="Hayır"];
      alarm_level -> activate_cam -> send_notify -> false_alarm;
      false_alarm -> reset_alarm [label="Yanlış alarm"];
      false_alarm -> continue_alarm [label="Alarm doğru"];
      continue_alarm -> reset_alarm [label="Hayır"];
      continue_alarm -> wait_loop [label="Evet"];
      wait_loop -> sensor_loop;
    }
