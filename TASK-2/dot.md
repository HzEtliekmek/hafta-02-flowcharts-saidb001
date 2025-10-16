    digraph Shopping {
      rankdir=TB;
      node [shape=rectangle, fontname="Helvetica"];
    
      start [label="Başla", shape=oval];
      login [label="Kullanıcı girişi"];
      login_check [label="Giriş doğru mu?", shape=diamond];
      exit1 [label="Hatalı giriş\nSistemden çık", shape=rectangle];
      
      categories [label="Ürün kategorilerini göster\n1-Giyim 2-Elektronik 3-Ev 4-Çıkış"];
      choose_cat [label="Kategori seç"];
      list_products [label="Ürünleri listele"];
      choose_prod [label="Ürün ID gir"];
      stock_check [label="Stokta var mı?", shape=diamond];
      out_of_stock [label="Stokta yok\nUyarı ver"];
      add_cart [label="Ürünü sepete ekle"];
      add_more [label="Başka ürün eklemek ister misiniz? (E/H)", shape=diamond];
      
      edit_cart [label="Sepeti görüntüle/düzenle", shape=rectangle];
      discount [label="İndirim kodu gir", shape=rectangle];
      discount_valid [label="İndirim geçerli mi?", shape=diamond];
      apply_disc [label="İndirimi uygula"];
      min_check [label="Tutar ≥ 50 TL mi?", shape=diamond];
      min_fail [label="Minimum 50 TL şartı sağlanmadı\nİşlem iptal", shape=rectangle];
      ship_check [label="Tutar ≥ 200 TL mi?", shape=diamond];
      ship_free [label="Kargo ücretsiz"];
      ship_add [label="Kargo 25 TL eklendi"];
      payment [label="Ödeme yöntemi seç"];
      payment_valid [label="Geçerli mi?", shape=diamond];
      invalid_pay [label="Geçersiz yöntem\nİşlem iptal", shape=rectangle];
      confirm [label="Sipariş onayı (E/H)", shape=diamond];
      order_done [label="Sipariş oluşturuldu"];
      order_cancel [label="Sipariş iptal edildi"];
      end [label="Bitiş", shape=oval];
    
      start -> login -> login_check;
      login_check -> categories [label="Evet"];
      login_check -> exit1 [label="Hayır"];
      exit1 -> end;
    
      categories -> choose_cat -> list_products -> choose_prod -> stock_check;
      stock_check -> out_of_stock [label="Hayır"];
      out_of_stock -> add_more;
      stock_check -> add_cart [label="Evet"];
      add_cart -> add_more;
      add_more -> categories [label="E"];
      add_more -> edit_cart [label="H"];
    
      edit_cart -> discount -> discount_valid;
      discount_valid -> apply_disc [label="Evet"];
      discount_valid -> min_check [label="Hayır"];
      apply_disc -> min_check;
    
      min_check -> min_fail [label="Hayır"];
      min_fail -> end;
      min_check -> ship_check [label="Evet"];
    
      ship_check -> ship_free [label="Evet"];
      ship_check -> ship_add [label="Hayır"];
      ship_free -> payment;
      ship_add -> payment;
    
      payment -> payment_valid;
      payment_valid -> invalid_pay [label="Hayır"];
      invalid_pay -> end;
      payment_valid -> confirm [label="Evet"];
    
      confirm -> order_done [label="E"];
      confirm -> order_cancel [label="H"];
      order_done -> end;
      order_cancel -> end;
    }
