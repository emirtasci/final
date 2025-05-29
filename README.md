Proje Çalıştırma Kılavuzu: Yorum Benzerlik Analizi
Amaç:
Bu rehber, otomobil kullanıcı yorumları üzerinde benzerlik analizi yapılan projenin adım adım nasıl çalıştırılacağını açıklar.

1. 🔧 GEREKSİNİMLER
Projeyi çalıştırmak için aşağıdaki Python kütüphanelerine ihtiyaç vardır:

bash
Kopyala
Düzenle
pip install pandas scikit-learn numpy
Not: SBERT veya Word2Vec ile çalışmak istenirse ek kütüphaneler gerekir:

bash
Kopyala
Düzenle
pip install sentence-transformers gensim
2. 📁 VERİ DOSYASI
Veri dosyasının adı: otomobil_yorum_analizi.csv
Dosyada, araçlarla ilgili kullanıcı yorumları bulunmaktadır. Yorumların işlendiği sütun: "yorum" (ya da dosyadaki ilgili sütun ismi).

Dosyayı aynı klasöre koyman yeterlidir.

3. 🧠 KULLANILAN MODEL
Bu projede ilk aşamada TF-IDF + Cosine Similarity yöntemi kullanılmıştır. Her yorum metni vektöre dönüştürülüp, birbirine olan benzerlikleri hesaplanmıştır.

4. ▶️ KODU ÇALIŞTIRMA
Python dosyasını terminalden veya Jupyter Notebook üzerinden çalıştırabilirsin. Örnek komut:

bash
Kopyala
Düzenle
python benzerlik_analizi.py
Kod akışı şu şekildedir:

Veriler okunur

TF-IDF matrisine dönüştürülür

Kosinüs benzerlik matrisi oluşturulur

Her yorum için en benzer 5 yorum ekrana yazdırılır

5. 📈 ÇIKTI ÖRNEĞİ
nginx
Kopyala
Düzenle
Yorum 0: "Araba çok hızlı ve konforlu."
En benzer yorumlar:
  - "Performansı çok iyi, hız konusunda çok memnunum." (Benzerlik: 0.83)
  - ...
6. 🚀 İLERİ SEVİYE: SBERT ile Denemek İstersen
SBERT kullanmak için aşağıdaki gibi bir yapı kurabilirsin:

python
Kopyala
Düzenle
from sentence_transformers import SentenceTransformer, util

model = SentenceTransformer('paraphrase-MiniLM-L6-v2')
embeddings = model.encode(yorum_listesi, convert_to_tensor=True)
cos_sim = util.pytorch_cos_sim(embeddings, embeddings)
7. 📌 NOTLAR
Kodun doğru çalışması için CSV dosyasındaki yorum sütununun doğru şekilde belirtilmiş olması gerekir.

Büyük veri setlerinde işlem süresi uzayabilir.

Çıktılar üzerinde filtreleme ya da eşik belirleme yapılabilir (örn. 0.75 üzeri benzerlikleri göster).

📝 Özet
Bu proje, kullanıcı yorumları arasında otomatik olarak benzerlik bulmaya yönelik bir çalışmadır. İlk aşamada TF-IDF ile başlanmış, dilersen SBERT gibi daha güçlü modellerle analiz genişletilebilir.
