    digraph ATM {
      rankdir=TB;
      node [shape=rectangle, fontname="Helvetica"];
      start [label="Başla\n(Kart takınız)", shape=oval];
    
      card_check [label="Kart takıldı mı?"];
      ask_pin [label="PIN sor\n(PIN gir)"];
      pin_decision [label="PIN doğru mu?", shape=diamond];
      pin_fail [label="PIN hatası sayacı++\n3 hatada kart bloke", shape=rectangle];
      block_card [label="Kart bloke et\nİşlem sonlandır", shape=rectangle];
      main_menu [label="Ana Menü\n1-Bakiye  2-Çekme  3-Çıkış", shape=rectangle];
      balance_proc [label="Bakiye göster"];
      withdraw_start [label="Çekilecek miktarı al"];
      check_multiple [label="20 TL'nin katı mı?", shape=diamond];
      insufficient_unit [label="20 TL'nin katı olmalı\nHata göster", shape=rectangle];
      check_balance [label="Bakiye yeterli mi?", shape=diamond];
      insufficient_balance [label="Yetersiz bakiye\nHata göster", shape=rectangle];
      check_daily [label="Günlük limit aşımı?", shape=diamond];
      limit_exceed [label="Günlük limit aşıldı\nHata göster", shape=rectangle];
      dispense [label="Para ver\nFiş yazdır"];
      ask_another [label="Başka işlem ister misiniz?\n(E/H)", shape=diamond];
      eject_card [label="Kartı geri ver\nOturumu kapat", shape=rectangle];
      end [label="Bitiş", shape=oval];
    
      start -> card_check;
      card_check -> ask_pin [label="Evet"];
      card_check -> end [label="Hayır"];
    
      ask_pin -> pin_decision;
      pin_decision -> main_menu [label="Evet"];
      pin_decision -> pin_fail [label="Hayır"];
    
      pin_fail -> pin_decision [label="Deneme < 3"];
      pin_fail -> block_card [label="Deneme = 3"];
      block_card -> end;
    
      main_menu -> balance_proc [label="1"];
      main_menu -> withdraw_start [label="2"];
      main_menu -> eject_card [label="3"];
    
      balance_proc -> ask_another;
      withdraw_start -> check_multiple;
      check_multiple -> insufficient_unit [label="Hayır"];
      insufficient_unit -> ask_another;
    
      check_multiple -> check_balance [label="Evet"];
      check_balance -> insufficient_balance [label="Hayır"];
      insufficient_balance -> ask_another;
    
      check_balance -> check_daily [label="Evet"];
      check_daily -> limit_exceed [label="Evet"];
      limit_exceed -> ask_another;
    
      check_daily -> dispense [label="Hayır"];
      dispense -> ask_another;
      ask_another -> main_menu [label="E"];
      ask_another -> eject_card [label="H"];
    
      eject_card -> end;
    }
