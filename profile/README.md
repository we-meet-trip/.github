# MAP

여행 일정을 추천하는 앱 MAP 의 공개 저장소 묶음이다. 사용자가 날짜·이동수단·취향을 고르면 장소와 동선, 시간표를 만들어 주고, 함께 가는 사람과 채팅하고, 카메라로 비춘 대상을 알려 준다.

교육·학습 목적으로 공개한 코드이며 운영 중인 서비스가 아니다.

## 저장소 지도

MAP 는 일곱 저장소로 이루어져 있다. 전체 구조와 한 번에 실행하는 방법은 [map-project-infra](https://github.com/we-meet-trip/map-project-infra) 에서 시작한다.

| 저장소 | 역할 |
|---|---|
| [map-project-infra](https://github.com/we-meet-trip/map-project-infra) | 전체 안내, 로컬 실행 구성(Docker Compose), DB 초기화 |
| [map-project-client](https://github.com/we-meet-trip/map-project-client) | 모바일 앱(Flutter, iOS·Android) |
| [map-project-user](https://github.com/we-meet-trip/map-project-user) | 사용자 BFF(Spring Boot): 인증·일정·채팅·동의, 다른 서비스 중계 |
| [map-project-agent](https://github.com/we-meet-trip/map-project-agent) | 추천 에이전트(FastAPI·LangGraph): 장소·경로·일정 생성 |
| [map-project-hub](https://github.com/we-meet-trip/map-project-hub) | 외부 데이터 게이트웨이(FastAPI·PostGIS): 관광·날씨·장소·경로 |
| [map-project-yolo](https://github.com/we-meet-trip/map-project-yolo) | 비전 서비스(WebSocket, 객체 탐지 + LLM 식별) |
| [map-project-admin](https://github.com/we-meet-trip/map-project-admin) | 운영 콘솔(FastAPI·React) |

## 한 번에 띄워 보기

외부 키·비용 없이 한 기계에서 띄울 수 있다. 모델은 합성 제공자, 외부 데이터는 스텁으로 답한다.

```sh
mkdir map && cd map
for r in infra user agent hub yolo admin client; do
  git clone https://github.com/we-meet-trip/map-project-$r
done
cd map-project-infra
./scripts/make-local-env.sh
docker compose --profile full up -d --build
```

자세한 순서·확인 방법·선택 기능은 [map-project-infra](https://github.com/we-meet-trip/map-project-infra) 의 README 에 있다.

## 기여·보안

- 기여 방법과 커밋 메시지 형식은 각 저장소의 `CONTRIBUTING.md`.
- 보안 문제는 공개 이슈 대신 각 저장소의 비공개 취약점 신고(Security → Report a vulnerability)로 알려 준다.

## 고지

- 이 저장소는 교육·학습 목적으로 공개한 코드다. 운영 중인 서비스가 아니며 지원을 약속하지 않는다.
- 이 프로젝트는 코드가 연동하는 외부 서비스·데이터 제공자(한국관광공사, 기상청, 공공데이터포털, 국토교통부, 서울특별시, 한국환경공단, 카카오, 네이버, Google, Apple, LangChain, ODsay, OpenStreetMap, Ultralytics, Wikimedia 등)와 관련이 없으며, 그들로부터 승인이나 후원을 받지 않았다. 언급한 상표와 서비스 이름은 각 소유자에게 있다.
- 저장소에는 제3자 데이터·이미지·본문을 넣지 않는다. 예외로, 이용조건을 원문으로 확인한 공공·개방 자료만 출처와 이용조건을 밝혀 담는다(`docs/data.md`). 그 밖의 외부 데이터는 각 제공자의 약관에 따라 직접 받아야 한다.
- MIT 라이선스는 이 저장소의 코드에만 적용된다. 저장소에 담은 공공·개방 자료와 외부 데이터, 모델 가중치, 폰트, 라이브러리는 각자의 이용조건·라이선스를 따른다.

## 라이선스

코드는 MIT 라이선스(각 저장소의 `LICENSE`)를 따른다. Copyright (c) The MAP Contributors. 만든 사람들은 각 저장소의 `AUTHORS.md` 에 있다.
