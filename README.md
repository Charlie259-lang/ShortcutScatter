<!DOCTYPE html>
<html>
<head>
  <title>Pisahkan Data Tiket</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #121212 url('https://media.linklist.bio/backgrounds/Zq7Qb762Xj6KaUWUSEPXCDpmKLCATryoNbbjK7Er.webp') no-repeat center center fixed;
      background-size: cover;
      color: #ffffff;
      padding: 30px;
      margin: 0;
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      position: relative;
    }

    /* Overlay untuk meningkatkan keterbacaan teks */
    body::before {
      content: '';
      position: fixed;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      background: rgba(18, 18, 18, 0.85);
      z-index: -1;
    }

    /* KOTAK MARGIN AREA HANYA DI TENGAH - SEKITAR KONTEN DENGAN GARIS BIRU */
    .main-container::before {
      content: '';
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      width: calc(100% + 100px); /* Lebih lebar dari konten */
      height: calc(100% + 100px); /* Lebih tinggi dari konten */
      background: rgba(0, 0, 0, 0.7); /* Hitam transparan */
      border-radius: 20px;
      z-index: -1;
      box-shadow: 
        0 0 50px rgba(0, 0, 0, 0.8),
        inset 0 0 30px rgba(0, 180, 216, 0.1);
      /* GARIS TEPI BIRU */
      border: 2px solid #00b4d8;
      box-shadow: 
        0 0 30px rgba(0, 180, 216, 0.3),
        0 0 50px rgba(0, 0, 0, 0.8),
        inset 0 0 30px rgba(0, 180, 216, 0.1);
    }

    .main-container {
      display: flex;
      gap: 30px;
      max-width: 1200px;
      width: 100%;
      justify-content: center;
      align-items: flex-start;
      position: relative;
      z-index: 1;
    }

    .center-section {
      display: flex;
      flex-direction: column;
      align-items: center;
      width: 500px;
    }

    .preview-section {
      width: 400px;
    }

    .input-container {
      width: 100%;
      display: flex;
      flex-direction: column;
      align-items: center;
    }

    /* JUDUL UTAMA DI TENGAH */
    .title-container {
      text-align: center;
      margin-bottom: 30px;
      width: 100%;
    }

    .main-title {
      color: #00b4d8;
      font-size: 28px;
      font-weight: bold;
      text-align: center;
      margin-bottom: 8px;
      text-transform: uppercase;
      letter-spacing: 1px;
    }

    .sub-title {
      color: #00b4d8;
      font-size: 20px;
      text-align: center;
      margin-bottom: 15px;
      font-weight: normal;
      position: relative;
      padding-bottom: 20px;
    }

    /* GARIS DI BAWAH SUBTITLE */
    .sub-title::after {
      content: '';
      position: absolute;
      bottom: 0;
      left: 50%;
      transform: translateX(-50%);
      width: 300px;
      height: 3px;
      background: linear-gradient(90deg, transparent, #00b4d8, #00b4d8, transparent);
      border-radius: 2px;
    }

    .section-title {
      color: #00b4d8;
      margin-bottom: 20px;
      font-size: 18px;
      font-weight: bold;
      text-align: center;
      width: 100%;
    }

    textarea {
      width: 100%;
      height: 120px;
      margin-bottom: 10px;
      background: rgba(30, 30, 30, 0.9);
      color: #ffffff;
      border: 1px solid #2e2e2e;
      padding: 10px;
      border-radius: 4px;
      box-sizing: border-box;
      backdrop-filter: blur(5px);
    }

    .clear-btn {
      background: none;
      border: 1px solid #007b9e;
      border-radius: 4px;
      color: #00b4d8;
      cursor: pointer;
      padding: 5px 12px;
      font-size: 14px;
      margin-bottom: 20px;
      backdrop-filter: blur(5px);
      background: rgba(30, 30, 30, 0.8);
      align-self: flex-start;
    }

    .clear-btn:hover {
      background-color: #007b9e;
      color: #ffffff;
    }

    .data-box {
      background: rgba(26, 26, 26, 0.9);
      border: 2px solid #007b9e;
      border-radius: 8px;
      padding: 12px 14px;
      margin-bottom: 12px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      backdrop-filter: blur(5px);
      width: 100%;
      box-sizing: border-box;
      min-height: 50px;
    }

    .label {
      font-weight: bold;
      color: #00b4d8;
      width: 100px;
      flex-shrink: 0;
      display: flex;
      align-items: center;
    }

    .value {
      flex-grow: 1;
      margin: 0 10px;
      word-break: break-word;
      color: #e0f7ff;
      display: flex;
      align-items: center;
      min-height: 20px;
      width: 300px;
      max-width: 300px;
      min-width: 300px;
    }

    .copy-btn {
      background: rgba(0, 180, 216, 0.2); /* Background biru transparan */
      border: 1px solid #00b4d8;
      border-radius: 6px;
      cursor: pointer;
      padding: 8px;
      display: flex;
      align-items: center;
      flex-shrink: 0;
      outline: none;
      transition: all 0.3s ease;
      min-width: 40px;
      min-height: 40px;
      justify-content: center;
    }

    .copy-btn:hover {
      background: rgba(0, 180, 216, 0.4);
      border-color: #00b4d8;
      transform: scale(1.05);
    }

    .copy-btn:focus {
      outline: 2px solid #00b4d8;
      outline-offset: 2px;
      background: rgba(0, 180, 216, 0.3);
    }

    .copy-btn:active {
      transform: scale(0.95);
      background: rgba(0, 180, 216, 0.5);
    }

    .copy-btn svg {
      fill: #00b4d8;
      transition: fill 0.2s ease;
    }

    .copy-btn:hover svg {
      fill: #ffffff;
    }

    /* Styling untuk preview gambar */
    .preview-section {
      background: rgba(26, 26, 26, 0.9);
      border: 2px solid #007b9e;
      border-radius: 8px;
      padding: 20px;
      backdrop-filter: blur(5px);
      height: fit-content;
    }

    .images-grid {
      display: grid;
      grid-template-columns: 1fr;
      gap: 15px;
    }

    .image-item {
      display: flex;
      flex-direction: column;
      align-items: center;
      background: rgba(30, 30, 30, 0.9);
      padding: 15px;
      border-radius: 8px;
      border: 1px solid #2e2e2e;
      backdrop-filter: blur(5px);
    }

    .image-title {
      color: #00b4d8;
      font-weight: bold;
      margin-bottom: 10px;
      font-size: 14px;
    }

    .image-preview {
      max-width: 100%;
      max-height: 200px;
      border-radius: 6px;
      border: 2px solid #007b9e;
      display: none;
      cursor: pointer;
      transition: transform 0.2s ease, border-color 0.2s ease;
    }

    .image-preview:hover {
      transform: scale(1.02);
      border-color: #00b4d8;
    }

    .image-placeholder {
      width: 200px;
      height: 150px;
      background: rgba(26, 26, 26, 0.9);
      border: 2px dashed #007b9e;
      border-radius: 8px;
      display: flex;
      align-items: center;
      justify-content: center;
      color: #00b4d8;
      font-size: 12px;
      text-align: center;
      cursor: default;
    }

    .image-error {
      color: #ff6b6b;
      font-size: 11px;
      margin-top: 5px;
      display: none;
    }

    .image-loading {
      display: none;
      color: #00b4d8;
      font-size: 11px;
      margin-top: 5px;
    }

    .no-preview {
      text-align: center;
      color: #666;
      font-style: italic;
      padding: 40px 20px;
    }

    /* Style untuk nilai kosong */
    .empty-value {
      color: #666;
      font-style: italic;
      display: flex;
      align-items: center;
      width: 100%;
    }

    /* Style untuk nilai dengan data */
    .value-content {
      display: flex;
      align-items: center;
      width: 100%;
    }

    /* Link container untuk multiple links */
    .links-container {
      display: flex;
      flex-direction: column;
      gap: 5px;
      width: 100%;
    }

    .link-item {
      display: flex;
      align-items: center;
      min-height: 20px;
    }

    .value a {
      color: #00b4d8;
      text-decoration: none;
      word-break: break-all;
      outline: none;
    }

    .value a:focus {
      outline: 2px solid #00b4d8;
      outline-offset: 2px;
      border-radius: 2px;
    }

    .value a:hover {
      color: #ffffff;
      text-decoration: underline;
    }

    /* Feedback untuk copy berhasil */
    .copy-success {
      color: #00ff88 !important;
    }
  </style>
</head>
<body>

<div class="main-container">
  <div class="center-section">
    <div class="input-container">
      <!-- JUDUL BARU DI TENGAH -->
      <div class="title-container">
        <div class="main-title">Scatter Mahjong Ways</div>
        <div class="sub-title">Event Scatter Mahjong Ways I & II</div>
      </div>

      <div class="section-title">INPUT DATA DARI DOCS SCATTER</div>

      <textarea id="inputData" placeholder="Tempel data di sini sormin jangan kau rusak..."></textarea>
      <button class="clear-btn" onclick="resetSemua()">🗑 Hapus</button>

      <div id="outputContainer">
        <div class="data-box">
          <span class="label">User ID :</span>
          <span class="value" id="userId">
            <span class="value-content">
              <span class="empty-value">-</span>
            </span>
          </span>
          <button class="copy-btn" onclick="copyUserId()" tabindex="1">
            <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24">
              <path d="M16 1H4c-1.1 0-2 .9-2 2v14h2V3h12V1zm3 4H8c-1.1 0-2 .9-2 2v14c0 1.1.9 2 
                       2 2h11c1.1 0 2-.9 2-2V7c0-1.1-.9-2-2-2zm0 16H8V7h11v14z"/>
            </svg>
          </button>
        </div>

        <div class="data-box">
          <span class="label">Kode Tiket :</span>
          <span class="value" id="kodeTiket">
            <span class="value-content">
              <span class="empty-value">-</span>
            </span>
          </span>
          <button class="copy-btn" onclick="copyKodeTiket()" tabindex="2">
            <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24">
              <path d="M16 1H4c-1.1 0-2 .9-2 2v14h2V3h12V1zm3 4H8c-1.1 0-2 .9-2 2v14c0 1.1.9 2 
                       2 2h11c1.1 0 2-.9 2-2V7c0-1.1-.9-2-2-2zm0 16H8V7h11v14z"/>
            </svg>
          </button>
        </div>

        <div class="data-box">
          <span class="label">Link Bukti :</span>
          <div class="value" id="linkBukti">
            <span class="value-content">
              <span class="empty-value">-</span>
            </span>
          </div>
          <button class="copy-btn" onclick="copyLinkBukti()" tabindex="3">
            <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24">
              <path d="M16 1H4c-1.1 0-2 .9-2 2v14h2V3h12V1zm3 4H8c-1.1 0-2 .9-2 2v14c0 1.1.9 2 
                       2 2h11c1.1 0 2-.9 2-2V7c0-1.1-.9-2-2-2zm0 16H8V7h11v14z"/>
            </svg>
          </button>
        </div>

        <div class="data-box">
          <span class="label">Bettingan :</span>
          <span class="value" id="bettingan">
            <span class="value-content">
              <span class="empty-value">-</span>
            </span>
          </span>
          <button class="copy-btn" onclick="copyBettingan()" tabindex="4">
            <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24">
              <path d="M16 1H4c-1.1 0-2 .9-2 2v14h2V3h12V1zm3 4H8c-1.1 0-2 .9-2 2v14c0 1.1.9 2 
                       2 2h11c1.1 0 2-.9 2-2V7c0-1.1-.9-2-2-2zm0 16H8V7h11v14z"/>
            </svg>
          </button>
        </div>
      </div>
    </div>
  </div>

  <!-- Preview gambar di samping kanan -->
  <div class="preview-section">
    <div class="section-title">PREVIEW GAMBAR BUKTI</div>
    <div id="imagesGrid" class="images-grid">
      <div class="no-preview">Belum ada data untuk ditampilkan</div>
    </div>
  </div>
</div>

<script>
const inputField = document.getElementById("inputData");
inputField.addEventListener("input", prosesData);

// Fungsi copy untuk masing-masing kolom
function copyUserId() {
  const element = document.getElementById('userId');
  copyTextFromElement(element);
}

function copyKodeTiket() {
  const element = document.getElementById('kodeTiket');
  copyTextFromElement(element);
}

function copyLinkBukti() {
  const element = document.getElementById('linkBukti');
  copyTextFromElement(element);
}

function copyBettingan() {
  const element = document.getElementById('bettingan');
  copyTextFromElement(element);
}

// Fungsi utama untuk copy teks
function copyTextFromElement(element) {
  let text = '';
  
  // Cek jika element memiliki value-content
  const valueContent = element.querySelector('.value-content');
  if (valueContent) {
    // Untuk link bukti yang memiliki multiple links
    if (element.id === 'linkBukti') {
      const links = valueContent.querySelectorAll('a');
      if (links.length > 0) {
        text = Array.from(links).map(link => link.textContent).join('\n');
      } else {
        text = valueContent.textContent || valueContent.innerText;
      }
    } else {
      // Untuk kolom lainnya
      text = valueContent.textContent || valueContent.innerText;
    }
  } else {
    // Fallback jika tidak ada value-content
    text = element.textContent || element.innerText;
  }
  
  // Bersihkan teks dan cek jika kosong
  text = text.trim();
  if (text === '-' || !text) {
    console.log("Tidak ada data untuk disalin");
    return;
  }
  
  // Copy ke clipboard
  navigator.clipboard.writeText(text).then(() => {
    console.log("Teks berhasil disalin:", text);
    showCopySuccess(element);
  }).catch(err => {
    console.error("Gagal menyalin teks:", err);
    // Fallback untuk browser yang tidak support clipboard API
    fallbackCopyTextToClipboard(text, element);
  });
}

// Fallback copy method
function fallbackCopyTextToClipboard(text, element) {
  const textArea = document.createElement("textarea");
  textArea.value = text;
  textArea.style.position = "fixed";
  textArea.style.left = "-999999px";
  textArea.style.top = "-999999px";
  document.body.appendChild(textArea);
  textArea.focus();
  textArea.select();
  
  try {
    const successful = document.execCommand('copy');
    if (successful) {
      console.log("Teks berhasil disalin (fallback):", text);
      showCopySuccess(element);
    } else {
      console.error("Gagal menyalin teks (fallback)");
    }
  } catch (err) {
    console.error("Gagal menyalin teks (fallback):", err);
  }
  
  document.body.removeChild(textArea);
}

// Tampilkan feedback copy berhasil
function showCopySuccess(element) {
  const button = element.closest('.data-box').querySelector('.copy-btn');
  if (button) {
    const originalSvg = button.innerHTML;
    const originalColor = button.querySelector('svg').style.fill;
    
    // Ganti dengan centang
    button.innerHTML = '<span style="color: #00ff88; font-size: 18px; font-weight: bold;">✓</span>';
    
    // Kembalikan setelah 1.5 detik
    setTimeout(() => {
      button.innerHTML = originalSvg;
    }, 1500);
  }
}

function prosesData() {
  const input = inputField.value.trim();
  const parts = input.split(/\s+/);

  let userId = parts[0] || "-";
  let kodeTiket = "-";
  let bettingan = "-";
  let links = [];

  for (let i = 1; i < parts.length; i++) {
    const part = parts[i];

    if (part.startsWith("http")) {
      links.push(part);
    } else if (/^\d{15,20}$/.test(part)) {
      kodeTiket = part;
    } else if (part.toUpperCase().includes("BET")) {
      const next = parts[i + 1] || "";
      bettingan = next.split("-")[0].replace(/[^\d,]/g, "") || "-";
    }
  }

  // Update semua kolom dengan ukuran yang konsisten
  updateValue('userId', userId);
  updateValue('kodeTiket', kodeTiket);
  updateValue('bettingan', bettingan);
  
  // Update link bukti
  if (links.length) {
    updateLinkBukti(links);
    showImagePreviews(links);
  } else {
    updateValue('linkBukti', '-');
    showImagePreviews([]);
  }
}

function updateValue(elementId, value) {
  const element = document.getElementById(elementId);
  const valueContent = element.querySelector('.value-content');
  
  if (value === '-' || !value) {
    valueContent.innerHTML = '<span class="empty-value">-</span>';
  } else {
    valueContent.innerHTML = value;
  }
}

function updateLinkBukti(links) {
  const element = document.getElementById("linkBukti");
  const valueContent = element.querySelector('.value-content');
  
  valueContent.innerHTML = `
    <div class="links-container">
      ${links.map(link => 
        `<div class="link-item"><a href="${link}" target="_blank" tabindex="-1">${link}</a></div>`
      ).join('')}
    </div>
  `;
}

function showImagePreviews(links) {
  const grid = document.getElementById("imagesGrid");
  
  if (links.length === 0) {
    grid.innerHTML = '<div class="no-preview">Belum ada data untuk ditampilkan</div>';
    return;
  }
  
  grid.innerHTML = '';
  
  // Buat preview untuk setiap link
  links.forEach((link, index) => {
    const imageItem = document.createElement('div');
    imageItem.className = 'image-item';
    imageItem.id = `imageItem-${index}`;
    
    // Judul gambar
    const title = document.createElement('div');
    title.className = 'image-title';
    title.textContent = `Gambar ${index + 1}`;
    
    // Container untuk preview gambar
    const imageContainer = document.createElement('div');
    imageContainer.className = 'image-preview-container';
    
    // Placeholder
    const placeholder = document.createElement('div');
    placeholder.className = 'image-placeholder';
    placeholder.textContent = 'Loading...';
    
    // Gambar preview yang bisa diklik
    const imagePreview = document.createElement('img');
    imagePreview.className = 'image-preview';
    imagePreview.id = `imagePreview-${index}`;
    imagePreview.onclick = function() {
      window.open(link, '_blank');
    };
    
    // Loading indicator
    const loading = document.createElement('div');
    loading.className = 'image-loading';
    loading.id = `imageLoading-${index}`;
    loading.textContent = 'Memuat gambar...';
    
    // Error message
    const error = document.createElement('div');
    error.className = 'image-error';
    error.id = `imageError-${index}`;
    error.textContent = 'Gagal memuat gambar';
    
    imageContainer.appendChild(placeholder);
    imageContainer.appendChild(imagePreview);
    imageContainer.appendChild(loading);
    imageContainer.appendChild(error);
    
    imageItem.appendChild(title);
    imageItem.appendChild(imageContainer);
    grid.appendChild(imageItem);
    
    // Muat gambar
    loadImagePreview(link, index);
  });
}

function loadImagePreview(url, index) {
  const imagePreview = document.getElementById(`imagePreview-${index}`);
  const imagePlaceholder = document.querySelector(`#imageItem-${index} .image-placeholder`);
  const imageLoading = document.getElementById(`imageLoading-${index}`);
  const imageError = document.getElementById(`imageError-${index}`);
  
  // Reset state
  imagePreview.style.display = "none";
  imagePlaceholder.style.display = "flex";
  imageLoading.style.display = "none";
  imageError.style.display = "none";
  
  // Coba muat gambar
  const img = new Image();
  img.onload = function() {
    imagePreview.src = url;
    imagePreview.style.display = "block";
    imageLoading.style.display = "none";
    imagePlaceholder.style.display = "none";
  };
  
  img.onerror = function() {
    imageLoading.style.display = "none";
    imageError.style.display = "block";
    imagePlaceholder.style.display = "flex";
    imagePlaceholder.textContent = 'Gagal memuat';
    imagePlaceholder.style.color = '#ff6b6b';
  };
  
  img.src = url;
}

function resetSemua() {
  inputField.value = "";
  updateValue('userId', '-');
  updateValue('kodeTiket', '-');
  updateValue('linkBukti', '-');
  updateValue('bettingan', '-');
  showImagePreviews([]);
}
</script>

</body>
</html>
