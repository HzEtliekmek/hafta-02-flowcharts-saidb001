# Online Alışveriş Sepeti Sistemi - Sözde Kod (pseudocode)

    FUNCTION start_shopping_system():
        display("Lütfen giriş yapınız.")
        username := prompt("Kullanıcı adı:")
        password := prompt("Şifre:")
        
        IF NOT verify_user(username, password):
            display("Hatalı giriş! Sistemden çıkılıyor.")
            return
        
        cart := []
        total_price := 0
    
        DO:
            display("Kategoriler: 1-Giyim  2-Elektronik  3-Ev  4-Çıkış")
            category := prompt_number("Kategori seçiniz:")
            
            IF category == 4:
                BREAK
            
            products := list_products_by_category(category)
            display_products(products)
            choice := prompt_number("Ürün ID'si giriniz (0 = Ana menü):")
            
            IF choice == 0:
                CONTINUE
    
            IF NOT is_in_stock(choice):
                display("Seçilen ürün stokta yok!")
            ELSE:
                quantity := prompt_number("Kaç adet eklemek istiyorsunuz?")
                add_to_cart(cart, choice, quantity)
                display("Ürün sepete eklendi.")
            
            another := prompt("Başka ürün eklemek ister misiniz? (E/H)")
        WHILE another in ["E", "e", "evet"]
    
        # Sepeti düzenleme döngüsü
        DO:
            display_cart(cart)
            edit := prompt("Sepeti düzenlemek ister misiniz? (E/H)")
            IF edit in ["E", "e"]:
                update_cart(cart)
            ELSE:
                BREAK
        WHILE TRUE
    
        total_price := calculate_cart_total(cart)
        discount_code := prompt("İndirim kodunuz varsa giriniz (yoksa boş bırakın):")
        
        IF validate_discount_code(discount_code):
            total_price := apply_discount(total_price)
            display("İndirim uygulandı. Yeni tutar: " + format_currency(total_price))
    
        IF total_price < 50:
            display("Minimum sipariş tutarı 50 TL olmalıdır.")
            return
    
        IF total_price >= 200:
            shipping_cost := 0
            display("Kargo ücretsiz.")
        ELSE:
            shipping_cost := 25
            total_price := total_price + shipping_cost
            display("Kargo ücreti 25 TL eklendi.")
    
        display("Toplam ödenecek tutar: " + format_currency(total_price))
        payment := prompt("Ödeme yöntemi seçiniz (1-Kredi Kartı / 2-Havale / 3-Kapıda Ödeme):")
        
        IF payment not in [1,2,3]:
            display("Geçersiz ödeme yöntemi!")
            return
    
        confirm := prompt("Siparişi onaylıyor musunuz? (E/H)")
        IF confirm in ["E", "e"]:
            process_order(username, cart, total_price)
            display("Sipariş başarıyla oluşturuldu!")
        ELSE:
            display("Sipariş iptal edildi.")
    
        display("Teşekkürler, iyi alışverişler!")
