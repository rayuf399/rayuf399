from telethon.sync import TelegramClient

# Telegram API məlumatları
api_id = '22070794'         # my.telegram.org saytından API ID
api_hash = '5b20302854f0f6ac270f98d3f014f799'     # my.telegram.org saytından API Hash
phone = '+994553996899'    # Sizin telefon nömrəniz (+994... formatında)

# Telegram müştərisini yaradın
client = TelegramClient(phone, api_id, api_hash)

async def main():
    # Kontaktları yükləyin
    contacts = await client.get_contacts()

    # Kontaktları fayla yazın
    with open('contacts.txt', 'w') as file:
        for contact in contacts:
            if contact.phone:
                file.write(f"{contact.first_name} {contact.last_name or ''}: {contact.phone}\n")

    print("Kontaktlar 'contacts.txt' faylına yükləndi.")

# Skripti işə salın
with client:
    client.loop.run_until_complete(main())
