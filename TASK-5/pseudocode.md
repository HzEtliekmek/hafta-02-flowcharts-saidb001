# Akıllı Ev Güvenlik Sistemi - Sözde Kod (pseudocode)

    FUNCTION smart_home_security_system():
        IF NOT system_active():
            display("Sistem kapalı. Aktivasyon bekleniyor.")
            return
    
        DO:
            sensor_data := read_sensors()
    
            IF motion_detected(sensor_data):
                display("Hareket algılandı!")
                IF NOT resident_home():
                    alarm_level := determine_alarm_level(sensor_data)
                    display("Alarm seviyesi: " + str(alarm_level))
                    activate_cameras()
                    send_notifications(alarm_level)
    
            IF door_window_open(sensor_data):
                display("Kapı/Pencere açık!")
                IF NOT resident_home():
                    alarm_level := determine_alarm_level(sensor_data)
                    display("Alarm seviyesi: " + str(alarm_level))
                    activate_cameras()
                    send_notifications(alarm_level)
    
            wrong_alarm := check_false_alarm()
            IF wrong_alarm:
                display("Ev sahibi evde, alarm iptal edildi.")
                reset_alarm()
            ELSE:
                continue_alarm := prompt("Alarm devam etsin mi? (E/H)")
                IF continue_alarm not in ["E", "e"]:
                    reset_alarm()
            
            wait(interval)
        WHILE TRUE
