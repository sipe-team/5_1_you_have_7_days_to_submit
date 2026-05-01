# Swim Dots HK

## 한 줄 소개
> Apple Health 수영 기록을 **HealthKit**으로 직접 읽어 하프톤 도트 아트로 시각화하는 iOS 앱. swim-dots의 HealthKit 연동 버전.

## 문제 정의
swim-dots는 Apple Health 내보내기 XML 파일을 사용자가 직접 픽으로 골라야 했다. 640MB짜리 XML을 Health 앱에서 내보내고 → 에어드랍으로 폰에 옮기고 → 파일 선택까지 — "한 번 보고 싶다"의 비용이 너무 컸다.

이번엔 영민님 Apple Developer 유료 계정($99/년)을 빌려서 **HealthKit 직접 연동**이 가능해졌다. 기존 버전에서 HealthKit으로 데이터 소스만 바꾸는 게 목표였기 때문에 시각·렌더 코드는 의도적으로 손대지 않았고, 두 앱을 나란히 띄우면 같은 워크아웃의 도트가 거의 동일하게 그려지는 게 목표였다. 
