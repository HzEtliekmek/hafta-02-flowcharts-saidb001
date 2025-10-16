# Hastane Randevu Sistemi - Sözde Kod (pseudocode)

    FUNCTION hospital_system():
        DO:
            tc_no := prompt("Lütfen TC Kimlik Numaranızı giriniz:")
            IF NOT verify_tc(tc_no):
                display("Geçersiz TC Kimlik Numarası!")
            ELSE:
                BREAK
        WHILE TRUE
    
        DO:
            display("1- Randevu Al\n2- Tahlil Sonucu Gör\n3- Çıkış")
            choice := prompt_number("İşlem seçiniz:")
    
            IF choice == 1:
                display("Poliklinikler: Dahiliye, Kardiyoloji, Cildiye...")
                poly := prompt("Poliklinik seçiniz:")
                doctors := list_doctors(poly)
    
                DO:
                    display("Doktorlar:")
                    display_list(doctors)
                    doc := prompt("Doktor seçiniz:")
                    available_times := get_available_times(doc)
                    display("Uygun saatler:")
                    display_list(available_times)
                    time := prompt("Saat seçiniz:")
                    confirm := prompt("Randevuyu onaylıyor musunuz? (E/H)")
                    IF confirm in ["E", "e"]:
                        save_appointment(tc_no, doc, time)
                        send_sms_confirmation(tc_no)
                        display("Randevunuz onaylandı ve SMS gönderildi.")
                        BREAK
                    ELSE:
                        display("Randevu iptal edildi.")
                        BREAK
                WHILE TRUE
    
            ELSE IF choice == 2:
                IF NOT has_lab_results(tc_no):
                    display("Tahlil kaydınız bulunmamaktadır.")
                ELSE:
                    IF NOT is_result_ready(tc_no):
                        display("Sonuçlar henüz hazır değil. Lütfen daha sonra tekrar deneyin.")
                    ELSE:
                        display_lab_results(tc_no)
                        download := prompt("Sonuçları PDF olarak indirmek ister misiniz? (E/H)")
                        IF download in ["E", "e"]:
                            download_pdf(tc_no)
                            display("PDF başarıyla indirildi.")
    
            ELSE IF choice == 3:
                display("Sistemden çıkılıyor...")
                BREAK
    
            another := prompt("Başka işlem yapmak ister misiniz? (E/H)")
        WHILE another in ["E", "e", "evet"]
    
        display("İyi günler dileriz.")
