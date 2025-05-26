# 🔄 ETF 데이터 자동 업데이트 도구

Streamlit을 사용한 ETF 데이터 실시간 업데이트 및 GitHub 자동 연동 도구입니다.

## ✨ 주요 기능

- 📊 **실시간 ETF 데이터 업데이트**: Yahoo Finance API를 통한 최신 데이터 수집
- 🚀 **GitHub 자동 업데이트**: 업데이트된 데이터를 자동으로 GitHub 레포지토리에 저장
- 📈 **상세 분석 지표**: 수익률, 변동성, MDD, Sharpe Ratio 등 계산
- 💾 **다양한 다운로드 형식**: Excel, CSV 형식으로 데이터 다운로드
- 🎨 **인터랙티브 UI**: 그룹별 필터링, 정렬 기능

## 🚀 빠른 시작

### 1. Streamlit Cloud 배포

1. 이 레포지토리를 Fork 또는 Clone
2. [Streamlit Cloud](https://share.streamlit.io)에서 앱 배포
3. 메인 파일: `update_etf_data.py`

### 2. GitHub 자동 업데이트 설정 (선택사항)

#### 2-1. GitHub Personal Access Token 생성

상세한 가이드: **[GitHub_Token_Setup_Guide.md](GitHub_Token_Setup_Guide.md)**

1. GitHub → Settings → Developer settings → Personal access tokens
2. "Generate new token (classic)" 클릭
3. 권한 설정: **repo** (전체 선택), **workflow**
4. 토큰 복사 및 안전하게 보관

#### 2-2. Streamlit Secrets 설정

상세한 가이드: **[Streamlit_Secrets_Setup_Guide.md](Streamlit_Secrets_Setup_Guide.md)**

Streamlit Cloud 앱 → Settings → Secrets에 다음 내용 추가:

```toml
[github]
token = "your_github_token_here"
repo_owner = "your_github_username"
repo_name = "your_repository_name"
```

## 📋 사용 방법

### 기본 사용법

1. **🔄 데이터 새로고침**: ETF 데이터 업데이트 (GitHub 자동 업데이트 포함)
2. **🚀 GitHub 업데이트**: 수동으로 GitHub에 업데이트
3. **📥 데이터 다운로드**: Excel/CSV 파일 다운로드

### GitHub 설정 확인

- 앱 상단의 **"🔧 GitHub 설정 상태"** 확장 메뉴 클릭
- **"🔍 GitHub 연결 테스트"** 버튼으로 설정 확인

## 📦 설치 및 의존성

### 필수 패키지 (`requirements.txt`)

```
streamlit>=1.28.0
pandas>=1.5.0
numpy>=1.24.0
yfinance>=0.2.28
openpyxl>=3.1.0
pytz>=2023.3
requests>=2.31.0
matplotlib>=3.7.0
```

### 로컬 실행

```bash
pip install -r requirements.txt
streamlit run update_etf_data.py
```

## 📊 데이터 구조

### 입력 데이터 (`etf_data.xlsx` 또는 `etf_data.csv`)

| 컬럼명 | 설명 |
|--------|------|
| ETF Ticker | ETF 티커 심볼 |
| ETF Name | ETF 이름 |
| Group | 그룹 분류 |

### 출력 데이터

| 컬럼명 | 설명 |
|--------|------|
| Close | 종가 |
| Daily Return (%) | 일간 수익률 |
| Weekly Return (%) | 주간 수익률 |
| Monthly Return (%) | 월간 수익률 |
| YTD Return (%) | 연초 대비 수익률 |
| 22/132/264 Days Return (%) | 기간별 수익률 |
| Ultra-Short/Short-term/Long-term Vol (%) | 기간별 변동성 |
| MDD (%) | 최대 낙폭 |
| 52W High Drawdown (%) | 52주 고점 대비 수익률 |
| Sharpe Ratio | 샤프 비율 |

## 🔧 고급 설정

### 1. Google Sheets 연동 (선택사항)

`google_sheets_integration.py` 참조

### 2. GitHub Actions 자동화 (선택사항)

정기적인 데이터 업데이트를 위한 GitHub Actions 설정 가능

### 3. 커스텀 분석 지표

코드 수정을 통해 추가 분석 지표 구현 가능

## 🛠️ 문제 해결

### 자주 발생하는 오류

| 오류 | 원인 | 해결방법 |
|------|------|----------|
| yfinance 오류 | 네트워크 또는 API 제한 | 잠시 후 재시도 |
| GitHub 401 오류 | 토큰 문제 | 새 토큰 생성 |
| GitHub 404 오류 | 레포지토리 이름 오류 | Secrets 설정 확인 |
| Secrets 오류 | 설정 누락 | Streamlit Secrets 재설정 |

### 로그 확인

Streamlit Cloud → 앱 → Logs에서 상세한 오류 메시지 확인

## 📁 파일 구조

```
ETF_Update_Tool/
├── update_etf_data.py              # 메인 애플리케이션
├── requirements.txt                # 패키지 의존성
├── etf_data.xlsx                   # 입력 데이터 (Excel)
├── etf_data.csv                    # 입력 데이터 (CSV)
├── README.md                       # 이 파일
├── GitHub_Token_Setup_Guide.md     # GitHub 토큰 설정 가이드
├── Streamlit_Secrets_Setup_Guide.md # Streamlit Secrets 설정 가이드
├── github_auto_update.py           # GitHub API 함수 (참조용)
└── google_sheets_integration.py    # Google Sheets 연동 (선택사항)
```

## 🔒 보안 고려사항

- ✅ GitHub 토큰은 Streamlit Secrets에만 저장
- ✅ 토큰을 코드에 하드코딩하지 않음
- ✅ 최소 권한 원칙 적용
- ✅ 정기적인 토큰 갱신 권장

## 📞 지원

- **이슈 리포트**: GitHub Issues 활용
- **기능 요청**: Pull Request 환영
- **문서 개선**: README 및 가이드 문서 기여 환영

## 📄 라이선스

MIT License - 자유롭게 사용, 수정, 배포 가능

---

**🎯 성공적인 설정을 위한 체크리스트:**

- [ ] Streamlit Cloud 앱 배포 완료
- [ ] `etf_data.xlsx` 또는 `etf_data.csv` 파일 업로드
- [ ] GitHub Personal Access Token 생성
- [ ] Streamlit Secrets 설정 완료
- [ ] GitHub 연결 테스트 성공
- [ ] 첫 번째 데이터 업데이트 테스트 