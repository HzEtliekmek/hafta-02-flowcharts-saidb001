    digraph CourseRegistration {
      rankdir=TB;
      node [shape=rectangle, fontname="Helvetica"];
    
      start [label="Başla", shape=oval];
      login [label="Öğrenci girişi"];
      login_check [label="Giriş geçerli mi?", shape=diamond];
      exit1 [label="Geçersiz giriş\nSistemden çık", shape=rectangle];
    
      show_courses [label="Ders listesini göster"];
      choose_course [label="Ders seç"];
      course_full [label="Kontenjan dolu?", shape=diamond];
      prereq_check [label="Ön koşullar tamam mı?", shape=diamond];
      schedule_check [label="Zaman çakışması?", shape=diamond];
      credit_check [label="Kredi limiti aşımı?", shape=diamond];
      gpa_check [label="GPA < 2.5?", shape=diamond];
      advisor_approval [label="Danışman onayı alındı mı?", shape=diamond];
      add_course [label="Dersi ekle"];
      another_course [label="Başka ders ekle/çıkar?", shape=diamond];
    
      summary [label="Kayıt özeti göster"];
      confirm [label="Kayıt onayla?", shape=diamond];
      finalize [label="Kayıt tamamlandı"];
      cancel [label="Kayıt iptal edildi"];
      end [label="Bitiş", shape=oval];
    
      start -> login -> login_check;
      login_check -> show_courses [label="Evet"];
      login_check -> exit1 [label="Hayır"];
      exit1 -> end;
    
      show_courses -> choose_course;
      choose_course -> course_full;
      course_full -> show_courses [label="Evet"];
      course_full -> prereq_check [label="Hayır"];
      prereq_check -> show_courses [label="Hayır"];
      prereq_check -> schedule_check [label="Evet"];
      schedule_check -> show_courses [label="Evet"];
      schedule_check -> credit_check [label="Hayır"];
      credit_check -> show_courses [label="Evet"];
      credit_check -> gpa_check [label="Hayır"];
      gpa_check -> advisor_approval [label="Evet"];
      gpa_check -> add_course [label="Hayır"];
      advisor_approval -> show_courses [label="Hayır"];
      advisor_approval -> add_course [label="Evet"];
      add_course -> another_course;
      another_course -> show_courses [label="Evet"];
      another_course -> summary [label="Hayır"];
      summary -> confirm;
      confirm -> finalize [label="Evet"];
      confirm -> cancel [label="Hayır"];
      finalize -> end;
      cancel -> end;
    }
