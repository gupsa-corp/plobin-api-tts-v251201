# Plobin TTS API Service

TTS (Text-to-Speech) API 서비스입니다. 한국어 음성 합성을 지원합니다.

## 📋 필수 다운로드 항목

### 1. Python 가상환경 설정
```bash
cd plobin-api-tts/
python3 -m venv korean_tts_env
source korean_tts_env/bin/activate
pip install -r requirements.txt
```

### 2. 필수 라이브러리들 (자동 설치됨)
- PyTorch + CUDA 지원
- Transformers
- FastAPI/Uvicorn
- 한국어 TTS 관련 패키지들
- UniDic Lite 사전 (자동 다운로드, ~100MB)

### 3. 대용량 라이브러리 파일들
다음 파일들은 pip install 시 자동으로 다운로드됩니다:
- PyTorch CUDA 라이브러리들 (~2-3GB)
- NVIDIA CUDA/cuDNN 라이브러리들 (~1-2GB)
- 한국어 형태소 분석 사전 파일들

## 🚀 실행 방법

### 가상환경 활성화 후 서비스 시작
```bash
cd plobin-api-tts/
source korean_tts_env/bin/activate
python main.py
# 또는
uvicorn main:app --host 0.0.0.0 --port 40003
```

## 📁 디렉토리 구조

```
.
├── plobin-api-tts/         # 메인 TTS API 코드
│   ├── korean_tts_env/     # 가상환경 (gitignore됨)
│   ├── main.py             # FastAPI 메인 서버
│   ├── requirements.txt    # 파이썬 패키지 목록
│   └── static/             # 정적 파일들
└── README.md
```

## ⚠️ 주의사항

- `korean_tts_env/` 가상환경은 로컬에서 직접 생성해야 합니다
- PyTorch, CUDA 라이브러리들은 `pip install` 시 자동으로 다운로드됩니다 (~5GB)
- UniDic 사전 파일은 첫 실행 시 자동으로 다운로드됩니다
- 생성된 오디오 파일들(`.wav`)은 Git에 포함되지 않습니다

## 🌐 접근 URL

- HTTP: http://192.168.1.245:40003
- 도메인: http://api.tts.plobin.com:40003
- HTTPS: https://api.tts.plobin.com/ (리버스 프록시 설정 필요)

## 📖 API 문서

- Swagger UI: http://api.tts.plobin.com:40003/docs
- ReDoc: http://api.tts.plobin.com:40003/redoc
- 모델 상태: http://api.tts.plobin.com:40003/api/models/status

## 🎵 사용 예시

### 웹 인터페이스
브라우저에서 http://api.tts.plobin.com:40003/ 접속하여 직접 테스트 가능

### API 호출
```bash
curl -X POST "http://api.tts.plobin.com:40003/api/tts" \
     -H "Content-Type: application/json" \
     -d '{"text": "안녕하세요!", "language": "KR", "speed": 2.0}'
```