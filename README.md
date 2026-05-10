# Face Recognition Service — 1:1 Verification

## Prasyarat

- Python 3.13.3
- Docker (untuk Milvus)
- **Windows:** [Microsoft C++ Build Tools](https://visualstudio.microsoft.com/downloads/) → pilih "Desktop development with C++"
- **macOS:** `xcode-select --install`

---

## Setup

### 1. Jalankan Milvus
> Buka **Docker Desktop**, pastikan sudah running. Lalu jalankan di **Terminal**:

```bash
docker compose -f docker-compose.milvus.yml up -d
```

### 2. Buat Virtual Environment
> Jalankan di **Terminal**:

```bash
# Windows
python -m venv .venv
.venv\Scripts\activate

# macOS / Linux
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install Dependencies
> Jalankan di **Terminal** (pastikan virtual environment sudah aktif):

```bash
# Windows + GPU NVIDIA
pip install -r requirements.txt

# macOS / Linux / tanpa GPU
pip install -r requirements.cpu.txt
```

### 4. Setup `.env`
> Jalankan di **Terminal**:

```bash
cp .env.example .env
```

Lalu buka file `.env` dan isi:
```env
MILVUS_HOST=localhost
MILVUS_PORT=19530
SIMILARITY_THRESHOLD=0.55
```

### 5. Jalankan Service
> Jalankan di **Terminal**:

```bash
uvicorn main:app --host 0.0.0.0 --port 8000 --reload
```

Pertama kali jalan, model InsightFace (~300MB) akan otomatis terdownload.

Cek health:
```
GET http://localhost:8000/health
```
