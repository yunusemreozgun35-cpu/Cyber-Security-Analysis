# Vaka Analizi: Kişisel E-Posta Güvenliği ve CIA Üçgeni Değerlendirmesi

**Bağlam:** Savunmacı (Defensive) Siber Güvenliğe Giriş 
**Özne:** Kişisel Gmail Hesabı 
**Ölçüt:** CIA Üçgeni (Confidentiality, Integrity, Availability)
**Yöntem:** Şifre güvenliği paneli denetimi, e-posta üstbilgi (header) analizi ve platform mimarisinin incelenmesi

## Yönetici Özeti (Executive Summary)
Bu rapor, Google tabanlı kişisel e-posta hizmetinin (Gmail) temel güvenlik duruşunu CIA üçgeni çerçevesinde değerlendirmektedir. Yapılan analiz sonucunda; 21 karakterli karmaşık şifre ve donanım/yazılım destekli İki Aşamalı Doğrulama (2FA) sayesinde hesabın gizlilik (Confidentiality) açısından güçlü bir temele sahip olduğu tespit edilmiştir. Veri bütünlüğü (Integrity), Google'ın proaktif "sandbox" (izole ortam) taramaları ve e-posta kimlik doğrulama protokolleri (SPF, DKIM, DMARC) ile sağlanmaktadır. Sistemdeki birincil zafiyet, verilerin yalnızca bulut ekosistemine emanet edilmesidir; bu durumun yarattığı erişilebilirlik (Availability) riskini minimize etmek için maliyet-etkin bir çözüm olan periyodik donanımsal yedekleme (Google Takeout) stratejisi önerilmektedir. 

---

## 1. Gizlilik (Confidentiality)
Güvenlik mimarisinin ilk katmanı olan kimlik doğrulama süreçleri incelenmiştir. 
* Hesabı koruyan şifre 21 karakterden oluşmakta olup; rakam, sözcük, büyük/küçük harf ve noktalama işaretlerinin karmaşık bir kombinasyonunu barındırmaktadır.
* İki aşamalı doğrulama (2FA) mekanizması, SMS ve Duo Mobile authenticator alternatifleriyle aktiftir.
* İkincil e-posta ve kurtarma telefonu konfigürasyonları güncel tutularak kimlik doğrulama süreçleri desteklenmiştir.
* Parolanın başka bir dijital platformda kullanılmadığı teyit edilmiş olup, siber güvenlikte kritik bir kavram olan "tek nokta arızası" (single point of failure) riskinden başarılı bir şekilde kaçınılmıştır.

## 2. Bütünlük (Integrity)
Sistemin dışarıdan gelen tehditlere ve veri manipülasyonuna karşı dayanıklılığı değerlendirilmiştir.
* Ücretsiz Gmail sürümü, kullanıcıya ulaşan her bir e-posta ekini (attachment) izole bir ortamda (sandbox) tarayarak fidye yazılımı, solucan ve virüslere karşı proaktif bir koruma sağlamaktadır.
* Oltalama (phishing) ve spam saldırılarının engellenmesi için sunucu tabanlı kimlik doğrulama protokolleri olan Gönderici Politika Çerçevesi (SPF), Alan Anahtarları Tanımlanmış E-Posta (DKIM) ve DMARC aktiftir.
* Bir analist yaklaşımıyla e-postaların "Orijinalini Göster" (Header Analysis) menüsü üzerinden yapılan incelemelerde, bu protokollerin "Pass" (Başarılı) veya "Fail" (Başarısız) durumları net bir şekilde doğrulanabilmektedir.

## 3. Erişilebilirlik (Availability)
Kullanıcının verilerine ve iletişim kanallarına ihtiyaç duyduğu anda kesintisiz erişebilmesi ilkesi incelenmiştir.
* Google Hizmet Düzeyi Anlaşması (SLA) kapsamında, web arayüzü üzerinden e-posta hizmetine %99,9 oranında erişilebilirlik taahhüt edilmektedir.Bu durum, olası DDoS saldırılarına veya sunucu kesintilerine karşı kurumsal bir güvence sunar.
* Buna karşın, bulut tabanlı sistemlere tam bağımlılık bir zafiyet potansiyeli taşımaktadır. 

## Sonuç ve Aksiyon Planı
Kişisel Gmail hesabının mevcut güvenlik mimarisi, uygulanan temel ve güncel metotlar sayesinde görece makul düzeydedir. Gelişim alanlarına yönelik maliyet-etkin (cost-benefit) yaklaşımıyla şu sonuçlara varılmıştır:

1. **Maliyet-Etkinlik Optimizasyonu:** Protonmail gibi yüksek güvenlikli uçtan uca şifrelemeli alternatiflere geçiş, sıradan bir kullanıcının kullanılabilirlik (usability) deneyimini düşürüp maliyetleri artırabileceğinden, mevcut Gmail yapısında kalıp güvenlik farkındalığını artırmak daha gerçekçi bir çözümdür.
2. **Kritik Aksiyon - Çevrim Dışı Yedekleme:** Hesaba veya bulut altyapısına erişimin tamamen kaybedilmesi riskine (erişilebilirlik zafiyeti) karşı, Google Takeout aracı kullanılarak e-postaların belirli periyotlarla fiziksel donanımlara (hard disk) yedeklenmesi elzemdir.
3. **Sosyal Mühendislik Farkındalığı:** Teknik önlemler ne kadar güçlü olursa olsun, siber güvenlik okuryazarlığı sürekli geliştirilerek insan psikolojisini hedef alan saldırılara karşı tetikte olunmalıdır.
