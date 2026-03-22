import streamlit as st
import google.generativeai as genai

# --- 1. BEYİN BAĞLANTISI (GEMINI API) ---
# Kendi API anahtarını aşağıdaki tırnak işaretlerinin arasına yapıştır
  genai.configure(api_key="AIzaSyA-G0lgtnNtHga9_DHhLTcdn3Q2_VzcbLs)
model = genai.GenerativeModel('gemini-1.5-flash')

# --- 2. SAYFA AYARLARI ---
st.set_page_config(page_title="Asistan Prime v26.0", page_icon="🦉", layout="centered")

# Havalı Başlık ve Alt Başlık
st.markdown("<h1 style='text-align: center;'>🦉 Asistan Prime v26.0</h1>", unsafe_allow_html=True)
st.markdown("<p style='text-align: center; color: #00ffcc; font-weight: bold;'>Kuantum Bilgi Motoru Aktif</p>", unsafe_allow_html=True)
st.markdown("<p style='text-align: center; font-size: 0.8em;'>Tarih • Bilim • Genel Kültür • Yazılım</p>", unsafe_allow_html=True)

# --- 3. HAFIZA SİSTEMİ (Mesaj Geçmişi) ---
if "messages" not in st.session_state:
    st.session_state.messages = [
        {"role": "assistant", "content": "Selam! Ben Asistan Prime v26.0. 9 yaşındaki bir başmühendis tarafından geliştirildim. Bana dünyadaki her şeyi sorabilirsin!"}
    ]

# Eski mesajları ekranda göster
for message in st.session_state.messages:
    with st.chat_message(message["role"]):
        st.markdown(message["content"])

# --- 4. SOHBET GİRİŞİ ---
prompt = st.chat_input("Bir soru sor veya bir denklem yaz...")

if prompt:
    # Kullanıcı mesajını hafızaya ekle ve ekrana yaz
    st.session_state.messages.append({"role": "user", "content": prompt})
    with st.chat_message("user"):
        st.markdown(prompt)

    # Yapay Zekanın Cevabı
    with st.chat_message("assistant"):
        with st.spinner("Bilgi havuzunda aranıyor..."):
            try:
                # Asistanın kişiliğini belirliyoruz
                system_instruction = "Sen zeki, yardımsever ve 9 yaşındaki bir maker tarafından kodlanmış bir asistansın. Her konuda derin bilgin var."
                full_prompt = f"{system_instruction} Soru: {prompt}"
                
                # Gemini'den cevap al
                response = model.generate_content(full_prompt)
                full_response = response.text
                
                st.markdown(full_response)
                
                # Cevabı hafızaya kaydet
                st.session_state.messages.append({"role": "assistant", "content": full_response})
            except Exception as e:
                st.error(f"Bir hata oluştu: {e}. Lütfen API anahtarını kontrol et!")

# --- 5. YAN MENÜ (EK ÖZELLİKLER) ---
with st.sidebar:
    st.title("🛠️ Kontrol Paneli")
    st.info("v26.0 En Büyük Güncelleme")
    if st.button("Sohbeti Temizle"):
        st.session_state.messages = []
        st.rerun()
