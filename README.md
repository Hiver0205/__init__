<div align="center">

# 🛡️ 페이신 Faccine

### 보정할 때 함께 지켜지는 딥페이크 방지 카메라

평소처럼 사진을 보정하기만 하면,<br/>
사진 속 **모든 얼굴**에 눈에 띄지 않는 보호 신호가 함께 들어갑니다.

<br/>

![PWA](https://img.shields.io/badge/PWA-설치형_웹앱-5A0FC8?style=for-the-badge&logo=pwa&logoColor=white)
![TensorFlow.js](https://img.shields.io/badge/TensorFlow.js-FF6F00?style=for-the-badge&logo=tensorflow&logoColor=white)
![Vite](https://img.shields.io/badge/Vite-646CFF?style=for-the-badge&logo=vite&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)

**2026 창업아이디어 경진대회 · 팀 이닛 `__init__`**

</div>

<br/>

## 💡 왜 페이신인가요?

> SNS에 올린 사진 한 장이면 누구나 내 얼굴로 딥페이크를 만들 수 있습니다.
> 딥페이크 성범죄 피해자의 **92.6%가 10~20대**이고, 사진을 올리기 전에 따로 보호 도구를 쓰는 사람은 거의 없습니다.

페이신은 **보호를 따로 하는 일이 아니라, 보정할 때 함께 되는 일**로 만듭니다.

<br/>

## ✨ 주요 기능

| | 기능 | 설명 |
|:---:|---|---|
| 👥 | **모든 얼굴 자동 보호** | 단체 사진 속 얼굴까지 모두 찾아서 보호 |
| 🎨 | **보정 필터** | 피부 보정 · 화사하게 · 색온도 |
| 🛡️ | **보호 방식 2가지** | **그대로**: 눈에 띄지 않는 미세 신호만<br/>**메이크업**: 신원 인식을 피하는 메이크업을 자동으로 골라 입힘 (내추럴 · 코랄 · 로즈 · 클린) |
| 📊 | **보호 리포트** | 보호 전후 신원 유사도, SNS 압축 후에도 유지되는지 바로 확인 |
| 📱 | **앱으로 설치** | 홈 화면에 설치, 첫 실행 후에는 인터넷 없이도 동작 |
| 🔒 | **사진은 내 폰 밖으로 안 나감** | 모든 처리가 기기 안에서 이루어짐 |

<br/>

## 🔄 작동 방식

```
📷 촬영 / 갤러리  →  👤 얼굴 검출  →  🎨 보정 필터  →  🛡️ 보호 신호 삽입  →  📤 SNS 공유
```

보호 신호는 **두 얼굴 인식 모델을 동시에 속이도록** 만든 적대적 섭동입니다.
그래서 얼굴 스왑 도구가 쓰는 ArcFace 계열 신원 인식이 보호된 사진에서 원래 사람을 찾지 못합니다.

<br/>

## 📈 검증 결과

> **LFW 데이터셋 100명** · SNS 업로드를 흉내 낸 **JPEG 85% 압축 후** 보호 성공률

| 보호 방식 | ArcFace R50 | Glint360K R100 |
|---|:---:|:---:|
| 🛡️ 그대로 (기본값) | **91%** | **88%** |
| 💄 메이크업 | **95%** | **93%** |
| ❌ *참고: 일반 보정 앱* | *0%* | *0%* |

<details>
<summary><b>검증 방법 자세히 보기</b></summary>
<br/>

- **시나리오**: 공격자가 보호된 사진 A를 가져가서, 다른 곳에서 구한 같은 사람의 사진 B와 대조
- **평가 모델**: 보호 신호를 만들 때 **쓰지 않은** 모델 2개
  - ArcFace R50: 얼굴 스왑 도구(inswapper 등)의 신원 인코더
  - Glint360K R100: 학습 데이터가 다른 모델
- **판정 기준**: 다른 사람 쌍 9,900개 중 1%만 같은 사람으로 잘못 통과하도록 데이터로 정함
- **강인성**: JPEG 70% 압축, 75% 축소 후에도 측정
- 전체 비교표: [Data/results/comparison.md](Data/results/comparison.md)

</details>

<br/>

## 🛠️ 기술 스택

| 분야 | 사용 기술 |
|---|---|
| **앱** | Vanilla JS · Vite · PWA (Service Worker) |
| **얼굴 검출 · 인식** | TensorFlow.js · [face-api](https://github.com/vladmandic/face-api) · InsightFace ArcFace |
| **보호 신호** | 앙상블 적대적 공격 (MI-FGSM + EOT) · 미분 가능한 얼굴 정렬 · 자체 ONNX → TF.js 로더 |
| **검증** | Puppeteer · onnxruntime-node · LFW 데이터셋 |

<br/>

## 🚀 시작하기

```bash
cd Code
npm install
npm run dev      # 첫 실행 시 모델(약 26MB) 자동 다운로드
npm run build    # dist/ 생성 → HTTPS 호스팅에 올리면 휴대폰에 앱으로 설치 가능
```

`main` 브랜치에 push하면 GitHub Actions가 자동으로 GitHub Pages에 배포합니다.

<br/>

## 📁 폴더 구성

```
📦 __init__
 ┣ 📂 Code          웹앱 (PWA)
 ┣ 📂 Evaluate      LFW 기반 보호 효과 검증
 ┗ 📂 Data/results  검증 리포트
```

<br/>

## ⚠️ 한계와 주의

- 보호 강도를 높이면 작은 얼굴에서 **잔무늬**가 보일 수 있고, 메이크업 방식은 **화장이 진해질 수** 있습니다.
- 검증 범위는 ArcFace 계열 인식 모델이며, 다른 계열 모델과 확산 모델 기반 편집은 확인하지 않았습니다.
- 처리 속도는 PC GPU 기준으로 측정했고, 휴대폰에서는 더 느릴 수 있습니다.
- InsightFace 모델은 **비상업 · 연구용** 라이선스입니다. 저장소에는 넣지 않고 빌드할 때 내려받습니다.

<br/>

<div align="center">

**🛡️ 평소처럼 보정만 하면, 끝.**

Made with 💙 by Team 이닛 `__init__`

</div>
