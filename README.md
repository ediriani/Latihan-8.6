import re
import random
import string

def generate_random_password(length=8):
    """Menghasilkan password acak dengan panjang tertentu."""
    characters = string.ascii_letters + string.digits
    password = ''.join(random.choice(characters) for _ in range(length))
    return password

def extract_usernames_and_generate_passwords(teks):
    """
    Mencari email dalam teks, mengekstrak username, dan menghasilkan password acak.

    Args:
        teks (str): Teks yang akan dianalisis.

    Returns:
        list: List berisi string hasil pemrosesan setiap email.
    """
    email_regex = r'[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}'
    emails_ditemukan = re.findall(email_regex, teks)
    hasil = []
    for email in emails_ditemukan:
        try:
            username = email.split('@')[0]
            password = generate_random_password()
            hasil.append(f"{email} username: {username} , password: {password}")
        except IndexError:
            hasil.append(f"Format email tidak valid: {email}")
    return hasil

# Contoh penggunaan
teks_input = "Berikut adalah daftar email dan nama pengguna dari mailing list: anton@mail.com dimiliki oleh antonius\nbudi@gmail.co.id dimiliki oleh budi anwari\nslamet@getnada.com dimiliki oleh slamet slumut\nmatahari@tokopedia.com dimiliki oleh toko matahari"
hasil_proses = extract_usernames_and_generate_passwords(teks_input)
for item in hasil_proses:
    print(item)

teks_lain = input("Masukkan teks yang mengandung alamat email: ")
hasil_proses_lain = extract_usernames_and_generate_passwords(teks_lain)
for item in hasil_proses_lain:
    print(item)
