# 🎙️ Ses Klonlama Projesi (Coqui TTS - VITS Modeli)

Bu proje, [Coqui TTS](https://github.com/coqui-ai/TTS) kütüphanesi kullanılarak **VITS** modeli ile ses klonlama sürecini göstermektedir.  
Google Colab üzerinde gerekli kurulumlar yapılmış, özel bir veri seti ile model eğitilmiş ve çıktı olarak klonlanan ses üretilmiştir.  
Ayrıca, eğitilen modeli kolayca test edebilmek için **Streamlit tabanlı bir kullanıcı arayüzü** geliştirilmiştir.

---

## 📌 1. Gerekli Kurulumlar (Google Colab)

Aşağıdaki komutlar Google Colab üzerinde adım adım çalıştırılmalıdır.

```python
# Coqui TTS 0.11.1 kurulumu
!pip install e .

# Eğitim için gerekli ek paketler
!pip install trainer
!pip install TTS phonemizer

# PyTorch ve Torchaudio'nun CUDA 11.8 uyumlu versiyonlarını yükleme
!pip uninstall -y torch torchaudio
!pip install torch==2.2.2+cu118 torchaudio==2.2.2+cu118 \
    --index-url https://download.pytorch.org/whl/cu118

# phonemizer için espeak-ng kurulumu
!apt-get update -y
!apt-get install -y espeak-ng
!pip install phonemizer[espeak]
```



📂 2. Veri Seti Yapılandırması
train_vits.py dosyası içinde veri seti yolu ve metadata dosyası aşağıdaki gibi ayarlanmalıdır:
```
dataset_config = BaseDatasetConfig(
    formatter="ljspeech",
    meta_file_train="metadata.csv/txt",
    path="your/dataset/path"
)
```

🚀 3. Modeli Eğitme
Eğitim sürecini başlatmak için:
```
 !python train_vits.py
```
<img width="1263" height="1030" alt="ime4" src="https://github.com/user-attachments/assets/cf5dbecd-a890-46ac-9692-cde7b8ec99d2" />


📊 4. TensorBoard ile Eğitimi Takip Etme
Eğitim devam ederken modelin kayıplarını (loss) ve metriklerini takip etmek için:
```
 %load_ext tensorboard
 %tensorboard --logdir /path/to/logdir
```

 🗣️ 5. Ses Üretme
Eğitim tamamlandıktan sonra, eğitilen model ile ses çıktısı almak için aşağıdaki komutu çalıştırın:
```
  !tts \
  --text "Merhaba." \
  --model_path "/content/drive/My Drive/Colab Notebooks/proje_ismi\
  vits_thorsten-voice-June-24-2025_08+00AM-0000000/best_model.pth" \
  --config_path "/content/drive/My Drive/Colab Notebooks/proje_ismi\
  /vits_thorsten-voice-June-24-2025_08+00AM-0000000/config.json" \
  --out_path "/content/drive/My Drive/Colab Notebooks/proje_ismi/vits_thorsten-voice-June-24-2025_08+00AM-0000000/output.wav" \
  --use_cuda true
```

🎧 6. Ses Çıktısını Dinleme
Oluşturulan sesi doğrudan Colab üzerinde dinlemek için:
```
  from IPython.display import Audio
  Audio("/content/drive/My Drive/Colab Notebooks/Voice_CloningProject/vits_thorsten-voice-June-24-2025_08+00AM-0000000/output.wav")
```

💻 7. Streamlit Arayüzü
Bu projeye, ses klonlama sürecini kolaylaştırmak için bir Streamlit tabanlı kullanıcı arayüzü eklendi.
Bu arayüz sayesinde:

📂 Eğitilen model dosyasını yükleyebilirsiniz (.pth uzantılı)

📑 Config dosyasını yükleyebilirsiniz (.json uzantılı)

📑 CSV/TXT metadata dosyasını yükleyebilirsiniz (metadata.csv vb.)

🎵 Test etmek istediğiniz ses dosyasını yükleyebilirsiniz (.wav uzantılı)

📌 7.1 Gerekli Kurulumlar
Streamlit’i yüklemek için:
```
 !pip install streamlit
 !pip install TTS
 !pip install phonemizer
 !pip install pyngrok
```

▶️ 7.3 Arayüzü Çalıştırma
Yerel ortamda çalıştırmak için:
```
 streamlit run app.py
```

Google Colab üzerinde çalıştırmak için:
```
 from pyngrok import ngrok
 !streamlit run app.py &>/dev/null&
 public_url = ngrok.connect(port="8501")
 public_url
```

<img width="2156" height="1186" alt="ime1" src="https://github.com/user-attachments/assets/a8ce2fe2-7b02-4783-b9e1-94f8d96900b6" />


<img width="2159" height="825" alt="ime2" src="https://github.com/user-attachments/assets/8e64aa84-7ca1-490d-99b6-4b207139bee5" />


📌 7.4 Kullanım Adımları

1-Eğitilen model (.pth) dosyasını yükleyin.

2-Config (.json) dosyasını yükleyin.

3-(İsteğe bağlı) Metadata CSV/TXT dosyasını yükleyin.

4-Test etmek istediğiniz ses dosyasını yükleyin (orijinal ses karşılaştırması için).

5-Metin kutusuna üretilecek cümleyi yazın.

6-Ses Üret butonuna basın.

7-Sonuç sesini doğrudan arayüzde dinleyebilirsiniz.


📌 Proje linki aşağıdadır:
https://drive.google.com/file/d/14BcMBd29Sf2wHXVphX4WhJll6AIOQIj5/view?usp=sharing

Mail: deeptech.nlp.2025@gmail.com
Sifre: deeptech.2025

 



