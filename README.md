# Dil Konuşma Bozukluğu ve Kekemelik

Dil ve konuşma bozuklukları, her yaştan bireyde görülebilen
gelişimsel veya edinilmiş dil bozukluklarını, kekemelik ve
hızlı-bozuk konuşma gibi konuşmada görülen akıcılık
bozukluklarını, konuşma seslerinin doğru şekilde üretilememesi
şeklinde özetlenebilen konuşma sesi bozukluklarını, ses ve
yutma bozukluklarını ifade eder. Dil ve konuşma bozukluklarının
değerlendirme ve terapisinde Dil ve Konuşma Terapistleri görev
yapar.

Kekemelik, konuşma akıcılığını ve pürüzsüzlüğünü bozan
bir iletişim bozukluğu olmakla birlikte dil ve konuşma
bozukluklarının en yaygın görülen türleri arasındadır.
Sesleri, heceleri veya kelimeleri tekrar etme, uzatma veya
blok şekilde karakterize olabilir. Çoğunlukla gelişimsel
dönemde ortaya çıkar ve kronikleşebilir.

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


#install.packages("ggplot2")
#install.packages("dplyr")
library(dplyr)
library(ggplot2)

filtered_data <- TOPGIntakeData %>%
  mutate(LanguageCount = str_count(Languages, ",") + 1) %>%
  filter(LanguageCount >= 1 & LanguageCount <= 5, Difficulty_Level %in% c("1", "2", "3", "4", "5", "6", "7", "8", "9", "10"))

blue_palette <- colorRampPalette(c("#C7E9C0", "#1F75FE"))(10)

blue_palette[8:10] <- c("#1F75FE", "#0C47A1", "#07306B")

#nokta grafiğini oluşturalım
ggplot(filtered_data, aes(x = LanguageCount, y = as.numeric(Difficulty_Level), color = factor(Difficulty_Level))) +
  geom_point(position = position_jitter(width = 0.2, height = 0.2), size = 3, alpha = 0.7) +
  
  geom_density_2d(color = "gray", linetype = "dashed", size = 0.5, n = 100) +
  
    scale_color_manual(values = blue_palette, name = "Zorluk Seviyesi") +
  
  labs(
    title = "Konuşulan Dil Sayısı ve Kekemeliğin Zorluk Seviyesi Arasındaki İlişkisi",
    x = "Konuşulan Dil Sayısı",
    y = "Kekemeliğin Zorluk Seviyesi"
  ) +
  
  theme_minimal()




```

![KONUŞULAN DİL SAYISI](https://github.com/Yigitcanyardimci/Dil-Konu-ma-Bozuklu-u/assets/147248981/4492b789-ccb3-4f4e-a49d-96317510da25)









Görsel analizimize göre, özellikle iki dil konuşabilen bireylerde kekemeliğin daha sık görüldüğünü gözlemliyoruz. Bilinen dil sayısı ikiden daha fazla olduğunda, kekemeliğin görülme oranı belirgin bir şekilde azalmaktadır.




## Grafik-6 İş Kategorisine Göre Kekemeliğin Görülme Sıklığı


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




![iş Kat](https://github.com/Yigitcanyardimci/Dil-Konu-ma-Bozuklu-u/assets/147248981/4a4707bd-e907-4b65-b841-5d38b581c47e)



Grafik analizi, mühendisler arasında kekemelik yaşayanların, diğer meslek
gruplarına kıyasla konuşmada daha fazla zorluk yaşama eğiliminde olduklarına
dair bir eğilim ortaya koymaktadır.




# Sonuç 

Örneklem analizlerinin sonucuna bağlı olarak,

Kekemelik genellikle genç yaşlarda yoğun olarak görülse de, yaş ilerledikçe zorluklar artar. Cinsiyet analizi, erkeklerde
kadınlara göre daha sık rastlanan bir durumu ortaya koyar. Ancak yaşanan zorluklar arasında belirgin bir ilişki bulunmaz.
İki dil konuşabilen bireylerde kekemelik daha yaygındır, ancak dil sayısı arttıkça görülme oranı azalır. Ayrıca, teknik işlerle
uğraşan veya mühendislikle ilgilenen bireylerde kekemelik, diğer meslek gruplarına kıyasla daha sık gözlemlenir.

Zorluk seviyesi kekemeliğin zorluk düzeyini 1 ile 10 arasında derecelendiren faktördür.





