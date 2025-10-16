# ATM Para Çekme Sistemi - Sözde Kod (pseudocode)

CONSTANT DAILY_LIMIT := 5000          # günlük çekim limiti (örnek)
CONSTANT BILL_UNIT := 20              # banknot birimi
CONSTANT MAX_PIN_ATTEMPTS := 3

FUNCTION start_atm():
    display("Kartınızı takınız.")
    card := wait_for_card()
    if card == null:
        display("Kart takılmadı. İşlem iptal.")
        return

    pin_attempts := 0
    authenticated := FALSE

    WHILE pin_attempts < MAX_PIN_ATTEMPTS AND NOT authenticated:
        entered_pin := prompt("PIN giriniz:")
        if verify_pin(card, entered_pin):
            authenticated := TRUE
        else:
            pin_attempts := pin_attempts + 1
            remaining := MAX_PIN_ATTEMPTS - pin_attempts
            display("Hatalı PIN. Kalan deneme: " + to_string(remaining))

    IF NOT authenticated:
        block_card(card)
        display("Kart bloke edildi. Bankayla iletişime geçiniz.")
        return

    # Kullanıcı doğrulandı, ana menü döngüsü
    DO:
        selection := show_menu_and_get_choice(["Bakiye Sorgulama", "Para Çekme", "Çıkış"])
        IF selection == "Bakiye Sorgulama":
            balance := get_account_balance(card)
            display("Mevcut bakiye: " + format_currency(balance))
        ELSE IF selection == "Para Çekme":
            balance := get_account_balance(card)
            daily_withdrawn := get_daily_withdrawn_amount(card)
            display("Günlük kalan limit: " + format_currency(DAILY_LIMIT - daily_withdrawn))
            amount := prompt_number("Çekmek istediğiniz tutarı giriniz:")
            
            # Koşul kontrolleri
            IF amount <= 0:
                display("Geçersiz tutar.")
            ELSE IF amount % BILL_UNIT != 0:
                display("Lütfen " + BILL_UNIT + " TL'nin katları şeklinde giriniz.")
            ELSE IF amount > balance:
                display("Yetersiz bakiye.")
            ELSE IF (daily_withdrawn + amount) > DAILY_LIMIT:
                display("Günlük limit aşımı. Kalan limit: " + format_currency(DAILY_LIMIT - daily_withdrawn))
            ELSE:
                dispense_cash(amount)
                print_receipt(card, amount, get_account_balance(card) - amount)
                update_account_after_withdrawal(card, amount)
                display("Lütfen paranızı ve fişinizi alınız.")
        ELSE IF selection == "Çıkış":
            display("Oturum kapatılıyor. Kartınızı alınız.")
            eject_card(card)
            return
        END IF

        another := prompt("Başka işlem yapmak ister misiniz? (E/H)")
    WHILE another in ["E", "e", "evet"]

    display("İşleminiz sonlandırıldı. Kartınızı alınız.")
    eject_card(card)
    return
