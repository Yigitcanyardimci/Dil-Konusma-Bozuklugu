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

```
#install.packages(c("dplyr", "ggplot2"))
library(dplyr)
library(ggplot2)

# Sütun adlarını güncelleyelim
colnames(TOPGIntakeData) <- c("Timestamp", "Your_Age", "Your_Gender", "Languages", "City", "Qualification", "Activity", "Difficulty_Level")


age_mean <- mean(TOPGIntakeData$Your_Age, na.rm = TRUE)


blue_palette <- colorRampPalette(c("#C7E9C0", "#1F75FE"))(length(levels(TOPGIntakeData$Difficulty_Level)))

blue_palette[8:10] <- c("#1F75FE", "#0C47A1", "#07306B")

# Yeni renk paletini kullanarak violin plot oluşturalım
ggplot(TOPGIntakeData, aes(x = Difficulty_Level, y = Your_Age, fill = Difficulty_Level)) +
  geom_violin(trim = FALSE) +
  geom_boxplot(width = 0.2, fill = "white", color = "black") +
  scale_fill_manual(values = blue_palette) +
  
  # Yaş ortalamasını gösteren düz çizgi ekleyelim
  geom_hline(yintercept = age_mean, linetype = "solid", color = "red", size = 0.5) +
  
  labs(
    title = "Yaşa Göre Kekemelik Zorluk Seviyesi",
    x = "Zorluk Seviyesi",
    y = "Yaş",
    fill = "Zorluk Seviyesi"
  ) +
  
  theme_minimal()


```






![YAŞ](https://github.com/Yigitcanyardimci/Dil-Konu-ma-Bozuklu-u/assets/147248981/453e8792-74c2-46a8-9ad1-410fcacac145)




Grafik, kekemelik vakalarının genç yaşlarda özellikle yoğunlaştığını gösterirken, yaşın ilerlemesiyle birlikte zorlukların arttığını açıkça ifade etmektedir. Aynı zamanda, kekemeliğin en yüksek zorluk seviyelerinde yaş ortalamasının belirgin bir şekilde yükseldiğini vurgulayarak yaşın kekemelik üzerinde etkili bir faktör olduğunu gösteriyor. Yapılan analiz, kekemelikle mücadelede yaşın kritik bir parametre olduğunu ortaya koyuyor ve bu nedenle yaşa özgü müdahale stratejilerinin geliştirilmesinin büyük bir önem taşıdığını vurguluyor.




## Grafik-2 Kekemelik ile Yaş Arasındaki İlişki


```

# install.packages(c("ggstatsplot", "dplyr"))

# Kütüphaneleri yükleyin
library(ggstatsplot)
library(dplyr)

# Veri çerçevesindeki cinsiyet değişkenini faktöre çevirin
TOPGIntakeData$`Your gender?` <- factor(TOPGIntakeData$`Your gender?`)

# ggstatsplot ile scatter plot oluşturun ve cinsiyete göre renklendirin
ggstatsplot_output <- ggstatsplot::ggscatterstats(
  data = TOPGIntakeData,
  x = `Your Age`,
  y = `How will you describe your difficulties with stammering?`,  # Doğru değişkeni kullanalım
  title = "Yaş ve Kekemelik Zorluk Seviyesi",
  xlab = "Yaş",
  ylab = "Kekemelik Zorluk Seviyesi",
  messages = FALSE,
  cor.coef = TRUE,           # Korelasyon katsayısını göster
  cor.method.args = list("spearman"),  # Korelasyon yöntemini belirt
  ggtheme = ggplot2::theme_minimal() + ggplot2::theme(legend.position = "none"),  # Tema özelleştirmeleri
  ggstatsplot.layer = FALSE,  # İstatistiksel katmanı kaldır
  conf.level = 0.95,          # Güven aralığı
  conf.method.args = list("t"),  # Güven aralığı hesaplama yöntemi
  alpha = 0.7,               # Nokta saydamlığı
  dot.size = 3,              # Nokta boyutu
  add.reg.line = TRUE,       # Regresyon çizgisi ekle
  reg.line.color = "red",    # Regresyon çizgisi rengi
  reg.line.linetype = 2,     # Regresyon çizgisi tipi
  by = `Your gender?`,       # Cinsiyete göre renklendir
  pairwise.comparisons = TRUE,  # Gruplar arası karşılaştırmaları göster
  geom.params = list(bins = 20)  # Histogram için bins parametresini belirle
)

# ggstatsplot çıktısını yazdır
print(ggstatsplot_output)


```



![YAŞ VE GGSTATSPLOT](https://github.com/Yigitcanyardimci/Dil-Konu-ma-Bozuklu-u/assets/147248981/21cc931c-8a20-4fe5-9808-a6a2029b5d9c)








Görsel verilerimiz, özellikle genç yaş grubunda (18-30) kekemeliğin daha yaygın bir şekilde görüldüğünü göstermektedir. Bu yaş aralığındaki bireyler arasında kekemelik zorluk seviyelerinin ortalama düzeyde olduğunu söyleyebiliriz. Bu durum, genç yaşlarda kekemelikle daha sık karşılaşılmasına rağmen, bu grup içinde genellikle orta düzeyde zorluklarla başa çıkıldığını göstermektedir.


## Grafik-3 Cinsiyete Göre Kekemelik Zorluk Seviyesi

```
# install.packages("dplyr")
# install.packages("ggplot2")
library(dplyr)
library(ggplot2)

#sütun adlarını güncelleyelim
colnames(TOPGIntakeData) <- c("Timestamp", "Your_Age", "Your_Gender", "Languages", "City", "Qualification", "Activity", "Difficulty_Level")

#Veri çerçevesi, Your_Gender ve Difficulty_Level sütunları için boş olmayan değerlere sahip gözlemleri filtreleyelim
filtered_data <- TOPGIntakeData %>%
  filter(!is.na(Your_Gender) & Your_Gender != "" & !is.na(Difficulty_Level) & Difficulty_Level != "")

blue_palette <- colorRampPalette(c("#C7E9C0", "#4A90E2"))(length(levels(filtered_data$Difficulty_Level)))

blue_palette[8:10] <- c("#1F75FE", "#0C47A1", "#07306B")

#çubuk grafiği
ggplot(filtered_data, aes(x = reorder(Your_Gender, table(Your_Gender)[Your_Gender]), fill = Difficulty_Level)) +
  geom_bar(position = "dodge", stat = "count", width = 0.7, color = "white") +
  scale_fill_manual(values = blue_palette) +
  labs(
    title = "              Cinsiyete Göre Kekemeliğin Zorluk Seviyesi ve Gözlem Sayısı",
    x = "Cinsiyet",
    y = "Gözlem Sayısı",
    fill = "Zorluk Seviyesi"
  ) +
  theme_minimal() +
  theme(
    plot.title = element_text(size = 16, hjust = 0.5, face = "bold"),
    axis.title = element_text(size = 14, face = "bold"),
    axis.text = element_text(size = 12),
    legend.title = element_text(size = 14, face = "bold"),
    legend.text = element_text(size = 12)
  )



```


![CİNSİYET](https://github.com/Yigitcanyardimci/Dil-Konu-ma-Bozuklu-u/assets/147248981/85f3d67e-854a-447f-9526-6db57716e0c2)






Görsel analize göre, kekemelik erkek bireylerde kadınlara göre daha sık ortaya çıkıyor ve zorluk seviyelerinde de erkeklerin dezavantajlı olduğu görülüyor. Bu bağlamda, erkeklerin kekemelikle mücadele sürecinde kadınlara kıyasla daha fazla zorluk yaşadığı gözlemlenmektedir.

## Grafik-4 Cinsiyete Göre Kekemelik Zorluk Seviyesi


```
# install.packages(c("ggstatsplot", "dplyr"))

library(ggstatsplot)
library(dplyr)

if ("Your_Gender" %in% names(TOPGIntakeData)) {
  # Cinsiyet değişkenini faktöre çevirin ve Türkçe etiketleri tanımlayın
  TOPGIntakeData$Your_Gender <- factor(TOPGIntakeData$Your_Gender, levels = c("Male", "Female", "Prefer not to say"), labels = c("Erkek", "Kadın", "Belirtmek İstemeyenler"))

  ggbetweenstats_output <- ggbetweenstats(
    data = TOPGIntakeData,
    x = Your_Gender,
    y = Difficulty_Level,
    title = "Cinsiyet ve Kekemelik Zorluk Seviyesi",
    type = "np",
    messages = FALSE,
    ylab = "Kekemelik Zorluk Seviyesi",  # Y eksenini Türkçe ayarla
    xlab = "Cinsiyet"  # X eksenini Türkçe ayarla
  )

  print(ggbetweenstats_output)
} else {
  cat("Hata: 'Your_Gender' adında bir sütun bulunamadı.")
}

```



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


