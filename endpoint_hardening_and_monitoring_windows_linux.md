# GoIT Türkiye - Defensive Cyber Security Module
## Endpoint Hardening and Monitoring Lab Practice

[🇹🇷 Türkçe versiyonu için aşağıya kaydırın / Scroll down for Turkish version](#türkçe-versiyon-tr)

**Objective:** To implement fundamental system administration and security hardening protocols across Windows and Linux environments through Identity and Access Management (IAM), Access Control Lists (ACL), Audit Logging & Threat Detection, and Scheduled Task automation.

---

### 1. Identity and Access Management (IAM)
* **Action:** Created a standard user account named TestUser2 with limited privileges.
* **Target:** To mitigate the risk of full system compromise in the event of credential theft by enforcing the Principle of Least Privilege (PoLP), ensuring the user is not included in the local administrators or `sudo` group.

![IAM WIN-1: Windows Local Users and Groups configuration for TestUser2](images/iam-win-1.jpg)
*Figure 1: Windows IAM Configuration*

![IAM LIN-1: Creating TestUser2 via CLI](images/iam-lin-1.jpg)
*Figure 2: Kali Linux IAM Configuration*

---

### 2. Access Control Lists (ACL) and Data Integrity
* **Action:** Created a directory assigned to TestUser2 and restricted the account's permissions to read and execute only, explicitly denying write or modify access.
* **Target:** To ensure data integrity by preventing the encryption or deletion of files within the directory in the event that the restricted account is compromised by malicious software.

![ACL WIN-2: Restricting TestUser2 permissions in Windows Folder Security Properties](images/acl-win-2.jpg)
*Figure 3: Windows ACL Restriction*

![ACL LIN-2: Verifying directory permissions using the ls -ld command](images/acl-lin-2.jpg)
*Figure 4: Kali Linux Chmod Permission Restriction*

---

### 3. Audit Logging & Threat Detection
* **Action:** Enabled audit logging for failed logon events and successfully queried system logs following a simulated incorrect password entry.
* **Target:** To enhance SOC visibility by recording failed authentication attempts in system event viewers, enabling the ingestion of this data into a SIEM to detect potential brute-force attacks.

![ALTD WIN-3: Detecting failed logon attempt (Event ID 4625) in Event Viewer](images/altd-win-3.jpg)
*Figure 5: Windows Event Viewer - Event ID 4625 (Failed Logon)*

![ALTD LIN-3: Querying failed authentication logs via journalctl -t su](images/altd-lin-3.jpg)
*Figure 6: Kali Linux Journalctl - Failed Authentication Detection*

---

### 4. System Automation (Scheduled Task)
* **Action:** Configured an automated scheduled task (Task Scheduler on Windows, Cron Job on Linux) to execute a specific command prompt script at 1-hour intervals.
* **Target:** To establish a centralized coordination structure aligned with SOC monitoring methodologies, ensuring continuous, independent system tracking and the capability to trigger regular automated scans.

![SCHDT WIN-4: Verifying the trigger configuration in Task Scheduler](images/schdt-win-4.jpg)
*Figure 7: Windows Task Scheduler Configuration*

![SCHDT WIN-5: Verifying the automated command output (/c echo "SOCTest2: I SEE YOU...” & timeout /t 10)](images/schdt-win-5.jpg)
*Figure 8: Windows Automated Command Output*

![SCHDT LIN-4: Verifying the 0 * * * * wall "SOCTest2: I SEE YOU” cron job via crontab -l](images/schdt-lin-4.jpg)
*Figure 9: Kali Linux Cron Job Configuration*

---

<a name="türkçe-versiyon-tr"></a>

# GoIT Türkiye - Savunmacı/Defensive Siber Güvenlik Modülü
## Uç Nokta Sıkılaştırma (Endpoint-Hardening) ve İzleme (Monitoring) Laboratuvar Pratiği

**Amaç:** Kimlik Yönetimi (IAM), Erişim Kontrolü (ACL), Olay Kaydı & Tehdit Tespiti (Audit Logging & Threat Detection) ve Otomasyon (Scheduled Task) adımlarıyla temel sistem yönetimi ve güvenlik sıkılaştırma protokollerini Windows ve Linux ortamlarında uygulamak.

---

### 1. Kimlik ve Erişim Yönetimi (Identity and Access Management - IAM)
* **Eylem:** Sınırlı yetkilere sahip TestUser2 adlı kullanıcı hesabı oluşturulmuştur.
* **Hedef:** “En az ayrıcalık ilkesi” (PoLP) gereği kullanıcının, yöneticiler veya süper kullanıcı (sudo) grubuna dahil olmaması sağlanarak, kimlik hırsızlığı durumunda sistemin tamamen ele geçirilme riskinin azaltılması.

![IAM WIN-1: Windows Yerel Kullanıcılar ve Gruplar sekmesinde “TestUser2” profili oluşturma adımı](images/iam-win-1.jpg)
*Görsel 1: Windows IAM Konfigürasyonu*

![IAM LIN-1: Terminalde “TestUser2” kullanıcısı oluşturma adımı](images/iam-lin-1.jpg)
*Görsel 2: Kali Linux IAM Konfigürasyonu*

---

### 2. Erişim Kontrol Listeleri (ACL) ve Veri Bütünlüğü (Data Integrity)
* **Eylem:** TestUser2 adlı bir klasör oluşturulmuş ve TestUser2’nin bu klasörde yazma veya değiştirme erişimi engellenerek, salt okuma ve çalıştırma yetkisiyle sınırlandırılmıştır.
* **Hedef:** Veri bütünlüğünü güvenceye almak için kısıtlanmış hesabın zararlı yazılımlarca ele geçirilmesi halinde, ilgili dizindeki dosyaların şifrelenmesinin veya silinmesinin engellenmesi.

![ACL WIN-2: Windows Klasör Güvenlik Özelliklerinde TestUser2’yi kısıtlı yetkilendirme adımı](images/acl-win-2.jpg)
*Görsel 3: Windows ACL Kısıtlaması*

![ACL LIN-2: İzin denetleme çıktısı ls -ld komutunun denetimi](images/acl-lin-2.jpg)
*Görsel 4: Kali Linux Chmod Yetki Kısıtlaması*

---

### 3. Olay Kaydı ve Tehdit Tespiti (Audit Logging & Threat Detection)
* **Eylem:** Başarısız oturum açma girişimleri için denetim kaydı etkinleştirilmiş ve kasten yanlış şifre girildikten sonra sistem logları başarıyla sorgulanmıştır.
* **Hedef:** GHM/SOC görünürlüğünün (monitoring) artırılması için başarısız girişlerin olay görüntüleyicilerine yazılması ve verilerin SIEM'e aktarılarak kaba kuvvet (brute force) saldırılarının tespit edilmesi.

![ALTD WIN-3: Olay Görüntüleyicisi’nde başarısız giriş denetimi ve 4625 ID'li log tespiti](images/altd-win-3.jpg)
*Görsel 5: Windows Event Viewer 4625 Numaralı Hatalı Giriş Logu*

![ALTD LIN-3: Linux log denetleme çıktısı journalctl –t su komutunun denetimi](images/altd-lin-3.jpg)
*Görsel 6: Kali Linux Journalctl Başarısız Giriş Tespiti*

---

### 4. Sistem Otomasyonu (Scheduled Task)
* **Eylem:** Windows’ta Görev Zamanlayıcı (Task Scheduler), Linux’ta Cron Job üzerinde bir komutu 1 saatlik aralıklarla çalıştıracak bir zamanlanmış görev yapılandırılmıştır.
* **Hedef:** Bağımsız bir sürekli izlemenin sağlanmasıyla düzenli zafiyet taramalarının tetiklenmesi ve GHM/SOC anlayışıyla uyumlu bir merkezi eşgüdüm yapısının kurulması.

![SCHDT WIN-4: Görev Zamanlayıcısı’nda tetikleyici ayarının denetimi](images/schdt-win-4.jpg)
*Görsel 7: Windows Task Scheduler Yapılandırması*

![SCHDT WIN-5: Görev Zamanlayıcısı tetiklenmesinde gösterilecek /c echo "SOCTest2: I SEE YOU...” & timeout /t 10 komut çıktısının denetimi](images/schdt-win-5.jpg)
*Görsel 8: Windows Otomatik Komut Çıktısı*

![SCHDT LIN-4: Linux otomasyonu için cron -e komutuyla Cronjobs editörüne yazılan 0 * * * * wall "SOCTest2: I SEE YOU” komutunun crontab -l komutuyla denetimi](images/schdt-lin-4.jpg)
*Görsel 9: Kali Linux Cron Job Yapılandırması*
