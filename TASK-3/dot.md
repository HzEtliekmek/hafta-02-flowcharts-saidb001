    digraph Hospital {
      rankdir=TB;
      node [shape=rectangle, fontname="Helvetica"];
    
      start [label="Başla", shape=oval];
      tc_input [label="TC Kimlik No gir"];
      tc_check [label="Geçerli mi?", shape=diamond];
      invalid_tc [label="Geçersiz TC\nTekrar iste"];
      
      menu [label="İşlem Seç:\n1-Randevu Al\n2-Tahlil Sonucu Gör\n3-Çıkış"];
      choice [label="Seçim", shape=rectangle];
      randevu [label="Poliklinik seç\nDoktor listesi\nUygun saatler"];
      confirm_r [label="Randevuyu onayla?", shape=diamond];
      sms [label="Randevu kaydı\nSMS gönder"];
      cancel_r [label="Randevu iptal"];
      
      tahlil_check [label="Tahlil kaydı var mı?", shape=diamond];
      no_tahlil [label="Tahlil kaydı yok"];
      result_ready [label="Sonuç hazır mı?", shape=diamond];
      not_ready [label="Henüz hazır değil"];
      show_result [label="Sonuçları görüntüle"];
      pdf_choice [label="PDF indirilsin mi?", shape=diamond];
      pdf_download [label="PDF indirildi"];
      
      again [label="Başka işlem ister misiniz?", shape=diamond];
      exit [label="Sistemden çık", shape=rectangle];
      end [label="Bitiş", shape=oval];
    
      start -> tc_input -> tc_check;
      tc_check -> invalid_tc [label="Hayır"];
      invalid_tc -> tc_input;
      tc_check -> menu [label="Evet"];
    
      menu -> choice;
      choice -> randevu [label="1"];
      choice -> tahlil_check [label="2"];
      choice -> exit [label="3"];
    
      randevu -> confirm_r;
      confirm_r -> sms [label="Evet"];
      confirm_r -> cancel_r [label="Hayır"];
      sms -> again;
      cancel_r -> again;
    
      tahlil_check -> no_tahlil [label="Hayır"];
      tahlil_check -> result_ready [label="Evet"];
      result_ready -> not_ready [label="Hayır"];
      result_ready -> show_result [label="Evet"];
      show_result -> pdf_choice;
      pdf_choice -> pdf_download [label="Evet"];
      pdf_choice -> again [label="Hayır"];
      pdf_download -> again;
    
      no_tahlil -> again;
      not_ready -> again;
      exit -> end;
      again -> menu [label="Evet"];
      again -> end [label="Hayır"];
    }
