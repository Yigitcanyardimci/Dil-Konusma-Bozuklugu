# Dil Konuşma Bozukluğu ve Kekemelik

Dil konuşma bozukluğu, bireyin normalden farklı bir şekilde sesleri üretmesi veya kelimeleri düzgün bir şekilde kullanma yeteneğinin etkilendiği bir durumu ifade eder. Bu bozukluklar genellikle çocukluk döneminde başlar ve çeşitli nedenlere bağlı olarak ortaya çıkabilir. Kekemelik ise, konuşma akıcılığının bozulduğu ve konuşan kişinin bazı sesleri tekrarladığı, uzattığı veya bloke ettiği bir konuşma bozukluğudur. Genellikle stres, heyecan veya yorgunluk gibi faktörler kekemeliği artırabilir. Dil konuşma bozuklukları ve kekemelik, bireylerin günlük iletişim becerilerini etkileyebilir ve uygun terapötik yaklaşımlarla yönetilebilir.
Bu bilgiler ışığında bize verilen dil konuşma bozukluğu olan insanların verileri üzerinden çeşitli faktörleri ve etkenleri araştırdık. Bu araştırmama sırasında veri görselleştirme teknikleri kullanıldı. 

# Veri Seti 

Kekemelikle ilgili daha derin bir anlayış oluşturmayı teşvik etmek amacıyla, insanların yaş, cinsiyet ve eğitim seviyeleri ile kendi konuşma zorluklarına yönelik öz değerlendirmeleri arasındaki olası ilişkileri incelemek üzere çevrimiçi paylaşılan bir veri setidir. Veri setinin kısa bir özeti şu şekildedir:

Zaman Aralığı: Aralık 2020 - Haziran 2022
Toplam Gözlemler (Satırlar): 1135 (Başlık satırı dahil)
Değişkenler (Sütunlar): 8
Cinsiyet:

Erkek: 1051
Kadın: 79
Belirtmek İstemiyorum: 4
Bu bilgiler, kekemelikle ilgili genel istatistikler üzerinden toplumun bu konudaki algısını ve deneyimlerini daha iyi anlamayı amaçlamaktadır.
https://www.kaggle.com/datasets/sachinsrivastava/topgintakedataset

## Paketler








# Grafikler

## Grafik-1 Kekemelik ile Yaş Arasındaki İlişki


![YAŞ](https://github.com/Yigitcanyardimci/Dil-Konu-ma-Bozuklu-u/assets/147248981/453e8792-74c2-46a8-9ad1-410fcacac145)




Grafik, kekemelik vakalarının genç yaşlarda özellikle yoğunlaştığını gösterirken, yaşın ilerlemesiyle birlikte zorlukların arttığını açıkça ifade etmektedir. Aynı zamanda, kekemeliğin en yüksek zorluk seviyelerinde yaş ortalamasının belirgin bir şekilde yükseldiğini vurgulayarak yaşın kekemelik üzerinde etkili bir faktör olduğunu gösteriyor. Yapılan analiz, kekemelikle mücadelede yaşın kritik bir parametre olduğunu ortaya koyuyor ve bu nedenle yaşa özgü müdahale stratejilerinin geliştirilmesinin büyük bir önem taşıdığını vurguluyor.




## Grafik-2 Kekemelik ile Yaş Arasındaki İlişki


![YAŞ VE GGSTATSPLOT](https://github.com/Yigitcanyardimci/Dil-Konu-ma-Bozuklu-u/assets/147248981/21cc931c-8a20-4fe5-9808-a6a2029b5d9c)








Görsel verilerimiz, özellikle genç yaş grubunda (18-30) kekemeliğin daha yaygın bir şekilde görüldüğünü göstermektedir. Bu yaş aralığındaki bireyler arasında kekemelik zorluk seviyelerinin ortalama düzeyde olduğunu söyleyebiliriz. Bu durum, genç yaşlarda kekemelikle daha sık karşılaşılmasına rağmen, bu grup içinde genellikle orta düzeyde zorluklarla başa çıkıldığını göstermektedir.


## Grafik-3 Cinsiyete Göre Kekemelik Zorluk Seviyesi



![CİNSİYET](https://github.com/Yigitcanyardimci/Dil-Konu-ma-Bozuklu-u/assets/147248981/85f3d67e-854a-447f-9526-6db57716e0c2)






Görsel analize göre, kekemelik erkek bireylerde kadınlara göre daha sık ortaya çıkıyor ve zorluk seviyelerinde de erkeklerin dezavantajlı olduğu görülüyor. Bu bağlamda, erkeklerin kekemelikle mücadele sürecinde kadınlara kıyasla daha fazla zorluk yaşadığı gözlemlenmektedir.

## Grafik-4 Cinsiyete Göre Kekemelik Zorluk Seviyesi





![CİNSİYT VE GGSTATSPLOT](https://github.com/Yigitcanyardimci/Dil-Konu-ma-Bozuklu-u/assets/147248981/72ea8730-d359-492a-8ac9-2064c67caded)




Grafik analizinde cinsiyet ile kekemelik zorluğu arasında belirgin bir ilişki gözlemlenmemektedir. Bu durum, cinsiyet faktörünün kekemelik zorluğu üzerinde doğrudan bir etkisi olmadığını düşündürmektedir



## Grafik-5 Konuşulan Dil Sayısı ve Kekemeliğin Zorluk Seviyesi

```


 # install.packages(c("dplyr", "ggplot2"))

library(dplyr)
library(ggplot2)

# Kolon isimlerini düzenle
colnames(TOPGIntakeData) <- make.names(colnames(TOPGIntakeData))

# Veriyi filtrele
filtered_data <- TOPGIntakeData %>%
  filter(!is.na(Activity) & Activity != "")

# Aktivite gruplaması yap
filtered_data <- filtered_data %>%
  mutate(Activity_Grouped = case_when(
    grepl("Tech", Activity) ~ "Teknoloji/Mühendis",
    grepl("Developer", Activity) ~ "Geliştirici",
    grepl("Manager", Activity) ~ "Yönetici",
    grepl("Analyst", Activity) ~ "Analist",
    TRUE ~ NA_character_
  )) %>%
  na.omit() 

# Aktivite sıralaması
activity_order <- c("Teknoloji/Mühendis", "Geliştirici", "Yönetici", "Analist")
sorted_data <- filtered_data %>%
  group_by(Activity_Grouped) %>%
  mutate(Count = n()) %>%
  arrange(Count, .by_group = TRUE)

# Renk paleti
blue_palette <- colorRampPalette(c("#C7E9C0", "#1F75FE"))(10)
blue_palette[8:10] <- c("#1F75FE", "#0C47A1", "#07306B")

# Görselleştirme
ggplot(sorted_data, aes(x = Count, y = reorder(Activity_Grouped, Count), fill = as.factor(Difficulty_Level))) +
  geom_bar(stat = "identity", position = "dodge") +
  scale_fill_manual(values = blue_palette) +
  labs(
    title = "İş Kategorisine Göre Kekeme Zorluğu Tanımlamaları",
    y = "İş Kategorisi",
    x = "Gözlem Sayısı",
    fill = "Zorluk Seviyesi"
  ) +
  theme_minimal()


```



![iş Kat](https://github.com/Yigitcanyardimci/Dil-Konu-ma-Bozuklu-u/assets/147248981/4a4707bd-e907-4b65-b841-5d38b581c47e)






Görsel analizimize göre, özellikle iki dil konuşabilen bireylerde kekemeliğin daha sık görüldüğünü gözlemliyoruz. Bilinen dil sayısı ikiden daha fazla olduğunda, kekemeliğin görülme oranı belirgin bir şekilde azalmaktadır.




## Grafik-6 İş Kategorisine Göre Kekemeliğin Görülme Sıklığı


![KONUŞULAN DİL SAYISI](https://github.com/Yigitcanyardimci/Dil-Konu-ma-Bozuklu-u/assets/147248981/4492b789-ccb3-4f4e-a49d-96317510da25)




Grafik analizine göre, teknik işlerle uğraşan veya mühendis olan bireylerde kekemeliğin görülme oranının diğer meslek gruplarına göre daha yüksek olduğunu gözlemliyoruz. 


