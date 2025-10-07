# Make-To-Do-List
Company person's Task List
# TO-DO-LİST UYGULAMASI


#Listeleme Fonsiyonu
def gorev_listele(gorevler):
  if not gorevler:
    print("Görev mevcut değil.")
  else:
    print("\n --- GÖREVLERİ LİSTELE---")
    for i, gorev in enumerate(gorevler,1):
      print(f"{i}.{gorev}")

#Ekleme Fonksiyonu
def gorev_ekle(gorevler):
  gorev = input("Yeni görev:")
  gorevler.append(gorev)
  print("Yeni görev eklendi.")


#Düzenleme Fonksiyonu
def gorev_duzenle(gorevler):

  try:
    numara = int(input("Düzenlenecek görev numarası:"))
    if 0 < numara <= len(gorevler):
      yeni_gorev = input("Yeni göreviniz:")
      gorevler[numara-1] = yeni_gorev
      print("Göreviniz yeniden düzenlendi.")
    else:
      print("Lütfen geçerli bir görev numarası giriniz.")
  except ValueError:
    print("Lütfen geçerli bir sayı giriniz.")




#SİLME FONKSİYONU
def gorev_silme(gorevler):

  try:
    numara = int(input("Silinecek görev numarası:"))
    if 0 < numara <= len(gorevler):
      gorev_sil = gorevler.pop(numara-1)
      print(f"'{gorev_sil}' numaralı görev silindi.")
    else:
      print("Lütfen geçerli bir görev numarası giriniz.")
  except ValueError:
    print("Lütfen geçerli bir sayı giriniz.")

#DOSYA YAZDIRMA FONKSİYONU
def dosyaya_yaz(gorevler):
  with open("gorevler.txt", "w") as dosya:
    for gorev in gorevler:
      dosya.write(gorev + "\n")

#DOSYA OKUMA FONKSİYONU
def dosyadan_oku():
  gorevler = []
  try:
    with open("gorevler.txt", "r") as dosya:
      for satir in dosya:
        gorevler.append(satir.strip())
  except FileNotFoundError:
    pass # Dosya yoksa boş liste döndür
  return gorevler


#MENÜ EKRANI
def menu(gorevler):
  while True:
    print("To-Do List Uygulamasına hoşgeldiniz")
    print("Lütfen 1'den 6'ya kadar olan sayılardan seçim yapınız.")
    print("1. Görevleri Listele")
    print("2. Görev Ekle")
    print("3. Görev Düzenle")
    print("4. Görev Sil")
    print("5. gorevler.txt dosyasını görüntüle.")
    print("6. Çıkış")

    #Seçim
    secim = input("Seçiminiz:")

    if secim == '1':
      gorev_listele(gorevler)
    elif secim == '2':
      gorev_ekle(gorevler)
    elif secim == '3':
      gorev_duzenle(gorevler)
    elif secim == '4':
      gorev_silme(gorevler)
    elif secim == '5':
      gorevler = dosyadan_oku()
      gorev_listele(gorevler)
    elif secim == '6':
      print("Çıkış yapıldı.")
      exit()
    else:
      print("Lütfen geçerli bir seçim yapınız.")

    # Save changes to file after each operation
    dosyaya_yaz(gorevler)


# Görev listesini çağır
gorevler = dosyadan_oku()

# Menü fonksiyonunu çağır
menu(gorevler)
