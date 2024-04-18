### Story US-302

**Başlık**: Kullanıcı Profil Sayfasında E-posta Güncelleme Özelliği Ekleme

**Proje**: Kullanıcı Yönetim Sistemi

**Açıklama**:
Kullanıcılar, web uygulamasının "Profil" sayfası üzerinden kayıtlı e-posta adreslerini güncelleyebilmelidir. Bu özellik, kullanıcıların mevcut e-posta adreslerini yeni, geçerli bir e-posta adresiyle değiştirmelerini sağlar.

**Kabul Kriterleri**:
1. **Erişim Kontrolü**: Yalnızca kayıtlı ve oturum açmış kullanıcılar e-posta adreslerini güncelleyebilmelidir.
2. **E-posta Doğrulama**: Kullanıcı, yeni e-posta adresini iki kez girmeli ve girişler birbiriyle eşleşmelidir.
3. **Format Doğrulama**: Sistem, girilen e-posta adresinin geçerli bir e-posta formatında olduğunu doğrulamalıdır.
4. **Onay E-postası**: E-posta adresi güncellendikten sonra, kullanıcının yeni e-posta adresine bir doğrulama bağlantısı içeren bir onay e-postası gönderilmelidir. Kullanıcı bu bağlantıya tıkladığında, e-posta adresi güncellemesi tamamlanmış olmalıdır.
5. **Hata Mesajları**: Geçersiz girişlerde kullanıcıya açık ve anlaşılır hata mesajları gösterilmelidir.
6. **UI Güncellemeleri**: E-posta başarıyla güncellendiğinde, kullanıcıya bir başarı mesajı gösterilmelidir ve profil sayfasındaki e-posta adresi otomatik olarak güncellenmelidir.

**Etkilediği Dış Sistemler**:
(yok)

**Performans Beklentileri**:
(yok)

**Bağımlılıklar**:
- E-posta servisi API dokümantasyonunun tamamlanması.

**Görevler**:
- [ ] Backend API'sinde e-posta güncelleme endpoint'ini geliştir.
- [ ] Frontend'de e-posta güncelleme formunu oluştur.
- [ ] E-posta doğrulama işlevselliğini implemente et.
- [ ] Doğrulama e-postası gönderimi için e-posta servisini entegre et.
- [ ] UI Snapshot testleri yaz.
- [ ] API davranış testleri yaz.

**Referans Bağlantılar**:
- [Figma bağlantısı](.)
- [Veritabanı şeması](.)
- [Mimari plan](.)

**Story Point**: 34

**Geliştirme Sorumlusu**: xxx

**QA Kriterlerini Gözden Geçiren**: yyy
