# Agent Skills

Yapay zekâ kodlama ajanlarıyla çalışırken kullanılabilecek, yeniden kullanılabilir beceri (skill) ve referans dokümanları koleksiyonu.

## Mevcut beceriler

### [Clean SaaS UI](skills/clean-saas-ui/SKILL.md)

React, shadcn/ui ve Tailwind CSS v4 ile sade ve tutarlı SaaS arayüzleri oluşturmak için bir tasarım rehberi. Görsel kurallar, arayüz kararları, bileşen örüntüleri ve kalite kontrol adımlarını içerir.

## Kullanım

1. Kullanmak istediğiniz becerinin klasörünü, içindeki referans dosyalarıyla birlikte ajanınızın erişebileceği bir konuma yerleştirin.
2. Ajanınızdan ilgili `SKILL.md` dosyasını okuyup görev sırasında uygulamasını isteyin.
3. Becerinin yönlendirdiği karar ve referans dokümanlarını kullanarak çalışmaya devam edin.

Örnek istek:

> `skills/clean-saas-ui/SKILL.md` dosyasını oku ve bu rehberi kullanarak bir SaaS yönetim paneli oluştur.

Clean SaaS UI, tasarım kararlarını üzerinde çalışılan projenin kökündeki `design-decisions.md` dosyasında kaydeder ve sonraki çalışmalarda bu kararları kullanır.

## Klasör yapısı

```text
skills/
└── clean-saas-ui/
    ├── SKILL.md      # Ana beceri rehberi
    ├── decisions/    # Karar kuralları ve kayıt şablonu
    ├── reference/    # Tasarım ve uygulama referansları
    └── qa.md         # Kalite kontrol listesi
```

## Katkıda bulunma

Yeni beceriler ekleyebilir, mevcut rehberleri geliştirebilir veya sorunlar için issue açabilirsiniz. Yeni bir beceriyi `skills/<beceri-adi>/` altında, açıklayıcı bir `SKILL.md` ve gerekli referanslarıyla birlikte ekleyin.

## Lisans

Bu depo [MIT Lisansı](LICENSE) ile sunulur. Kişisel ve ticari kullanım, kopyalama, değiştirme, dağıtma ve satış ücretsiz olarak serbesttir. Dağıtılan kopyalarda telif hakkı ve lisans bildiriminin korunması gerekir. İçerik herhangi bir garanti olmaksızın sunulur.
