# Üniversite Ders Kayıt Sistemi - Sözde Kod (pseudocode)

    FUNCTION course_registration_system():
        student_id := prompt("Öğrenci No giriniz:")
        password := prompt("Şifre giriniz:")
        
        IF NOT verify_student(student_id, password):
            display("Geçersiz giriş! Sistemden çıkılıyor.")
            return
    
        total_credits := 0
        enrolled_courses := []
    
        DO:
            display("Ders Listesi:")
            courses := get_all_courses()
            display_courses(courses)
            
            choice := prompt_number("Ders seçiniz (0 = Çıkış):")
            IF choice == 0:
                BREAK
            
            course := get_course_details(choice)
    
            # Koşul kontrolleri
            IF course_full(course):
                display("Kontenjan dolu. Başka ders seçiniz.")
            ELSE IF not_prerequisites_met(student_id, course):
                display("Ön koşul dersleri tamamlanmamış.")
            ELSE IF schedule_conflict(enrolled_courses, course):
                display("Zaman çakışması mevcut.")
            ELSE IF (total_credits + course.credits) > 35:
                display("Toplam kredi limiti aşımı.")
            ELSE IF student_gpa(student_id) < 2.5:
                approval := prompt("Danışman onayı gerekli, onay alındı mı? (E/H)")
                IF approval not in ["E", "e"]:
                    display("Danışman onayı alınmadı.")
                    CONTINUE
            
            # Ders ekleme
            add_course(student_id, course)
            enrolled_courses.append(course)
            total_credits := total_credits + course.credits
            display("Ders başarıyla eklendi.")
            
            another := prompt("Başka ders eklemek/çıkarmak ister misiniz? (E/H)")
        WHILE another in ["E", "e", "evet"]
    
        # Kayıt özeti ve onay
        display_registration_summary(student_id, enrolled_courses, total_credits)
        confirm := prompt("Kaydı onaylıyor musunuz? (E/H)")
        IF confirm in ["E", "e"]:
            finalize_registration(student_id, enrolled_courses)
            display("Kayıt başarıyla tamamlandı.")
        ELSE:
            display("Kayıt iptal edildi.")
