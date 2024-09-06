"# library-system" 
class Kitap:
    def __init__(self, baslik, yazar, yayin_evi, yayin_yili):
        self.baslik = baslik
        self.yazar = yazar
        self.yayin_evi = yayin_evi
        self.yayin_yili = yayin_yili
        
    def bilgileri_goster(self):
        print("\n Kitap Bilgileri: ")
        print(f"Başlık: {self.baslik}\nYazar: {self.yazar}\nYayın Evi: {self.yayin_evi}\nYayın Yılı: {self.yayin_yili}")
        
    
class Uye:
    def __init__(self, ad, soyad, uye_numarasi):
        self.ad = ad
        self.soyad = soyad
        self.uye_numarasi = uye_numarasi
        
    def bilgileri_goster(self):
        print("\n Üye Bilgileri: ")
        print(f"Ad: {self.ad}\nSoyad: {self.soyad}\nÜye Numarası: {self.uye_numarasi}")
        
class Kutuphane:
    def __init__(self):
        self.kitaplar = []
        self.uyeler = []
        self.odunc_alinmis_kitaplar = {}
        
    def kitap_ekle(self, kitap):
        self.kitaplar.append(kitap)
        print(f"{kitap.baslik} kütüphanenize başarılı bir şekilde eklendi.")
        
    def kitap_sil(self, baslık):
        for kitap in self.kitaplar:
            if kitap.baslik == baslik:
                self.kitaplar.remove(kitap)
                print(f"{kitap.baslik} kütüphanenizden başarılı bir şekilde silindi.")
                return
        print(f"{baslik} başlıklı kitap bulunamadı")
        
    def uye_ekle(self, uye):
        self.uyeler.append(uye)
        print(f"{uye.ad} {uye.soyad} kütüphanenizin üyeleri arasına başarılı bir şekilde eklendi.")
        
    def uye_sil(self, uye_numarasi):
        for uye in self.uyeler:
            if uye.uye_numarasi == uye_numarasi:
                self.uyeler.remove(uye)
                print(f"{uye.uye_numarasi} kütüphanenizden başarılı bir şekilde silindi.")
                return
        print(f"{uye_numarasi} numaraya sahip üye bulunamadı")
        
    def odunc_almak(self, kitap, uye):
        if kitap in self.kitaplar and uye in self.uyeler:
            if kitap not in self.odunc_alinmis_kitaplar:
                self.odunc_alinmis_kitaplar[kitap] = uye
                print(f"{kitap.baslik} adlı kitap {uye.ad} {uye.soyad} kişisi tarafından başarılı bir şekilde ödünç alındı.")
            else:
                print(f"{kitap.baslik} daha önce başka birisi tarafından ödünç alınmıştır.")
    
    def geri_vermek(self, kitap):
        if kitap in self.odunc_alinmis_kitaplar:
            uye = self.odunc_alinmis_kitaplar.pop(kitap)
            print(f"{kitap.baslik} adlı kitap {uye.ad} {uye.soyad} kişisi tarafından geri verildi.")
        else:
            print(f"{kitap.baslik} adlı kitap şuan ödünçte değil.")
    
    def kitaplari_goster(self):
        if len(self.kitaplar) == 0:
            print("Henüz kütüphanenize eklenmiş bir kitap yoktur.")
        else:
            print("\nKitaplar: ")
            for kitap in self.kitaplar:
                kitap.bilgileri_goster()
            
    def uyeleri_goster(self):
        if len(self.uyeler) == 0:
            print("Henüz kütüphanenize eklenmiş bir üye yoktur.")                                                      
        else:
            print("\nÜyeler: ")
            for uye in self.uyeler:
                uye.bilgileri_goster()
            

kutuphane = Kutuphane()
while True:
    print(20*"*", "Kütüphane Yönetim Sistemi Menüsü", 20*"*")
    print("""
            1. Kitap Ekle
            2. Kitap Sil
            3. Üye Ekle
            4. Üye Sil
            5. Kitap Ödünç Al
            6. Kitap Geri Ver
            7. Kitapları Göster
            8. Üyeleri Göster
            9. Çıkış (q)
    """)
    islem = input("Yapacağınız işlemin numarasını giriniz: ")
    if islem == "1":
        baslik = input("Kitap başlığı: ")
        yazar = input("Yazar: ")
        yayin_evi = input("Yayın evi: ")
        yayin_yili = input("Yayın yılı: ")
        kitap = Kitap(baslik, yazar, yayin_evi, yayin_yili)
        kutuphane.kitap_ekle(kitap)
    elif islem == "2":
        baslik = input("Silmek istediğiniz kitabın adınız giirniz: ")
        kutuphane.kitap_sil(baslik)
    elif islem == "3":
        ad = input("Üye adı: ")
        soyad = input("Üye soyadı: ")
        uye_numarasi = input("Üye numarası: ")
        uye = Uye(ad, soyad, uye_numarasi)
        kutuphane.uye_ekle(uye)
    elif islem == "4":
        uye_numarasi = input("Silmek istediğiniz üyenin, üye numarasını giriniz: ")
        kutuphane.uye_sil(uye_numarasi)
    elif islem == "5":
        baslik = input("Kitabın adını giriniz: ")
        uye_numarasi = input("Üye numarasını giriniz: ")
        kitap = next((k for k in kutuphane.kitaplar if k.baslik == baslik), None)
        uye = next((u for u in kutuphane.uyeler if u.uye_numarasi == uye_numarasi), None)
        if kitap and uye:
            kutuphane.odunc_almak(kitap, uye)
        else:
            print("Yanlış bir kitap veya üye girişi yaptınız.")
            
    elif islem == "6":
        baslik = input("Kitabın adını giriniz: ")
        kitap = next((k for k in kutuphane.kitaplar if k.baslik == baslik), None)
        if kitap:
            kutuphane.geri_vermek(kitap)
        else:
            print("Yanlış bir kitap girişi yaptınız.")
            
    elif islem == "7":
        kutuphane.kitaplari_goster()
    elif islem == "8":
        kutuphane.uyeleri_goster()
    elif islem == "9" or islem == "q" or islem == "Q":
        print("Uygulamadan çıkış yaptınız.")
        break
    else:
        print("Yanlış bir işlem seçimi yaptınız. Lütfen yapmak istediğiniz işlemin sadece numarasını yazınız.")
        
                
            
