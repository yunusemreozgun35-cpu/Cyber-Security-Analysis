# SOC Concept Design for a Local Branch of a Global Hotel Chain
*GoIT Türkiye - Defensive Cyber Security Module / Assignment 2*

[🇹🇷 Türkçe versiyonu için aşağıya kaydırın / Scroll down for Turkish version](#türkçe-versiyon-tr)

## 1. Security Needs and Threat Modeling
* **Shadow IT & Visibility Gaps:** Right now, the SOC only receives logs from a small fraction of the devices on the network. When staff or guests connect unmonitored personal devices to the isolated Wi-Fi, it creates massive blind spots. This lack of visibility doesn't just disrupt pattern analysis; it opens the door for Man-in-the-Middle attacks against other guests and risks getting the corporate IP globally blacklisted due to spam traffic.
* **Single Point of Failure (Understaffed IT):** The local branch lacks the IT manpower to handle rapid, large-scale incidents. If a ransomware infection starts moving laterally across the operational network, manual triage and quarantine procedures simply won't be fast enough to stop it.
* **Hybrid Threats (Physical-Cyber Convergence):** Our OT (Operational Technology) systems—like pool controls or sauna power units—are air-gapped from the main network. However, because the SOC doesn't have integrated CCTV monitoring, these systems are highly vulnerable to physical sabotage. An attacker could easily walk in and plug a malicious USB (like a Rubber Ducky) directly into a terminal.

## 2. Main SOC Objectives
* **Zero Trust via SOAR Automation:** We need to compensate for the small IT team by automating our defenses. By setting up SOAR playbooks, EDR tools will isolate compromised endpoints automatically without waiting for human approval.
* **Strict Network Segmentation:** Enforcing hard firewall rules to keep the guest Wi-Fi completely separated from operational servers. We will also enable client isolation so devices on the guest network cannot communicate with each other.
* **Situational Awareness:** Bringing IT logs and physical security alerts (like unauthorized server room access) onto a single, unified SOC dashboard to get a real picture of the hotel's security posture.

## 3. Action Plan and Architecture
* **NDR & NAC for Access Control:** Network Detection and Response tools will monitor traffic patterns continuously. If an unregistered device (BYOD) connects to the network, Network Access Control (NAC) will immediately block it from reaching core servers.
* **Endpoint Security (EDR & DLP):** EDR solutions will run behavioral analysis to catch suspicious PowerShell or CMD executions in seconds. At the same time, we'll block malicious file transfers by constantly checking file hashes against known IOCs (Indicators of Compromise). If a machine is infected, it gets isolated instantly.
* **Vulnerability Management:** We won't wait for an attack. The team will run regular scans using tools like Nessus or OpenVAS to patch missing updates and known CVEs across the infrastructure.

## 4. Roles and Responsibilities
* **Tier 1 - Triage Analyst:**
  * *Role:* The first line of defense. Watches the SIEM dashboard 24/7 to catch incoming alerts.
  * *Skills:* Log analysis, weeding out false positives, and understanding basic correlation rules.
* **Tier 2 - Incident Responder:**
  * *Role:* Steps in when an attack is real. They isolate infected machines and coordinate the recovery effort with national authorities (USOM) or the central CERT team.
  * *Skills:* Malware analysis, active incident response, and crisis communication.
* **Tier 3 - Threat Hunter:**
  * *Role:* Proactively searches the network for hidden threats that bypassed Tier 1 and 2. They run penetration tests and look for architectural flaws.
  * *Skills:* Pentesting, advanced vulnerability scanning, and CVE research.
* **Tier 4 - SOC Manager:**
  * *Role:* Runs the entire operation. They build the SOAR playbooks and translate technical incidents into clear executive summaries for upper management.
  * *Skills:* Team leadership, strategic planning, and executive reporting.

---

<a name="türkçe-versiyon-tr"></a>
# Küresel Bir Otel Zincirinin Yerel Şubesi İçin SOC Konsept Tasarımı 🇹🇷
*GoIT Türkiye - Savunmacı Siber Güvenlik Modülü / 2. Ödev*

## 1. Güvenlik İhtiyaçları ve Tehdit Modellemesi
* **Shadow IT ve Görünürlük Sorunu:** Şu anda SOC, oteldeki yüzlerce cihazın sadece çok küçük bir kısmından log alabiliyor. Personel veya misafirler izole ağa denetimsiz şahsi cihazlarıyla bağlandığında ciddi kör noktalar oluşuyor. Bu durum sadece anomali analizini bozmakla kalmıyor; diğer misafirlere yönelik veri hırsızlığına zemin hazırlıyor ve spam trafiği nedeniyle kurumsal IP'nin küresel karalistelere (blacklist) girmesi riskini doğuruyor.
* **Müdahale Kapasitesi (Tek Nokta Arızası):** Yerel şubenin BT kadrosu, büyük çaplı krizleri manuel olarak yönetecek sayıya sahip değil. Operasyonel cihazları hedef alan bir fidye yazılımı (ransomware) ağda yatay olarak ilerlemeye başlarsa, insan gücüne dayalı karantina ve triyaj adımları çok geç kalacaktır.
* **Hibrit Tehditler (Fiziksel ve Siber Sabotaj):** Havuz veya sauna kumanda panelleri gibi Operasyonel Teknoloji (OT) sistemleri ana ağdan yalıtılmış (air-gapped) durumda. Ancak SOC ekibi kameraları (CCTV) anlık izleyemediği için, bu cihazlar fiziksel sabotaja tamamen açık. Dışarıdan biri rahatça gelip bu sistemlere zararlı bir USB (Rubber Ducky) takabilir.

## 2. SOC'un Ana Hedefleri
* **SOAR Otomasyonu ile Sıfır Güven (Zero Trust):** Yetersiz personel sayısını otomasyonla telafi etmeliyiz. SOAR platformlarında yazılacak senaryolar (playbooks) sayesinde, uç nokta koruma (EDR) sistemleri bir insan onayı beklemeden zararlı cihazları ağdan anında izole edecek.
* **Katı Ağ Bölümlendirmesi:** Misafir ağı ile operasyon sunucularını birbirinden tamamen ayırmak için katı güvenlik duvarı kuralları uygulayacağız. Ayrıca misafir ağındaki cihazların birbirini görmesini engelleyen "istemci izolasyonunu" (client isolation) aktif edeceğiz.
* **Durumsal Farkındalık:** BT cihazlarından gelen loglar ile fiziksel güvenlik alarmlarını (yetkisiz sunucu odası girişleri vb.) tek bir SOC ekranında birleştirerek otelin gerçek güvenlik tablosunu ortaya çıkaracağız.

## 3. Eylem Planı ve Teknik Mimari
* **NDR ve NAC ile Erişim Kontrolü:** Ağa bağlanan cihazların trafik desenleri NDR ile sürekli izlenecek. Envanter dışı (BYOD) bir cihaz ağa girdiğinde, Ağ Erişim Kontrolü (NAC) bu cihazın ana sunuculara ulaşmasını otomatik olarak engelleyecek.
* **Uç Nokta Güvenliği (EDR ve DLP):** EDR araçları, şüpheli CMD veya PowerShell komutlarını saniyeler içinde yakalamak için davranış analizi yapacak. Aynı zamanda dışarıdan gelen dosyaların hash değerleri bilinen tehdit göstergeleriyle (IOC) karşılaştırılarak zararlı aktarımlar durdurulacak. Enfekte olan makine anında ağdan koparılacak.
* **Zafiyet Yönetimi:** Saldırı olmasını beklemeyeceğiz. Ekip, Nessus veya OpenVAS gibi araçlarla düzenli taramalar yaparak altyapıdaki yama eksikliklerini ve güncel CVE açıklarını tespit edecek.

## 4. Roller ve Sorumluluklar
* **1. Kademe (Tier 1) - Triyaj Analisti:**
  * *Rolü:* İlk savunma hattı. Gelen alarmları yakalamak için SIEM ekranını 7/24 izler.
  * *Beceriler:* Log okuma, hatalı pozitifleri (false positive) ayıklama ve temel korelasyon mantığı.
* **2. Kademe (Tier 2) - Olay Müdahale Uzmanı:**
  * *Rolü:* Tehdit doğrulandığında devreye girer. Virüslü cihazları ağdan izole eder ve USOM veya merkezi SOME (CERT) ekipleriyle kurtarma sürecini koordine eder.
  * *Beceriler:* Zararlı yazılım analizi, aktif olay müdahalesi ve kriz iletişimi.
* **3. Kademe (Tier 3) - Tehdit Avcısı:**
  * *Rolü:* İlk iki kademeyi atlatmış olabilecek gizli tehditleri ağda proaktif olarak arar. Sızma testleri yapar ve mimari hataları bulur.
  * *Beceriler:* Pentest, ileri düzey zafiyet tarama ve CVE araştırması.
* **4. Kademe (Tier 4) - SOC Yöneticisi:**
  * *Rolü:* Tüm operasyonu yönetir. SOAR senaryolarını yazar ve yaşanan teknik olayları üst yönetimin anlayacağı stratejik raporlara dönüştürür.
  * *Beceriler:* Ekip liderliği, stratejik planlama ve üst düzey raporlama.

## References / Çevrim İçi Kaynaklar
1. GoIT Türkiye Siber Güvenlik Analistliği Kursu Öğrenim Materyalleri
2. IBM X-Force Threat Intelligence Index - Hospitality Sector Trends
3. CISA - IT/OT Convergence Strategies
4. NIST SP 800-48 - Wireless Network and Receiver Isolation
5. Gartner - The Risks of Shadow IT & BYOD
6. ASIS International - Physical Security and Cyber Convergence
