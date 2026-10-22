# 노트북 디스크 이미지 포렌식 분석

| | |
|---|---|
| 기간 | 2026.09.28 ~ 2026.10.12 (약 2주) |
| 인원 | 4명 |
| 내 역할 | Windows 아티팩트 분석 (UserAssist, ShellBag, Jump List, Prefetch) |
| 대상 | Windows 11 ARM64 노트북 디스크 이미지 1개 (E01, 약 85 GiB) |
| 시나리오 | NIST CFReDS "TechHive Scenario" (Mark Spencer, Arsenal Recon) |

## 시나리오

IT 회사 계약직이 사용한 노트북에서 회사 자료의 취급, 파일 이동, 외부 연락, 기록 정리 과정을 시간순으로 밝힌다.

## 분담

| 영역 | 대상 |
|---|---|
| Windows 아티팩트 (본인) | UserAssist, ShellBag, Jump List, Prefetch |
| 웹, 클라우드 | 브라우저 기록, 다운로드, WebCache |
| 외부장치, 파일시스템 | USBSTOR, $MFT, $UsnJrnl, 휴지통 |
| 계정, 인증 | SAM, SYSTEM, 자격증명 |

## 내 분석 결과

- Dropbox 실행: UserAssist와 Prefetch가 1월 22일 13:38:46으로 일치한다.
- 1월 30일 Dropbox 실행: UserAssist에 기록이 없고, USB 연결 0.75~0.85초 뒤 AutoPlay로 실행된 것으로 판단해 업로드 근거에서 제외했다.
- USB: ShellBag에 E:\TechHive 폴더를 탐색기로 연 기록이 있다. 그 아래 개별 파일 경로는 ShellBag, LNK, Jump List, Prefetch 어디에도 없다.
- 삭제 도구: Eraser, CCleaner, BleachBit, sdelete는 설치 목록, Prefetch, ShimCache, BAM에 없다. FORMAT.COM, DISKPART.EXE 실행 기록도 없다.
- E: 볼륨: LNK와 Jump List의 항목은 모두 포맷 후 볼륨 시리얼이고, 포맷 전 시리얼을 가리키는 항목은 없다.

## 팀 결론

- 회사 코드 6개 파일: Dropbox 업로드(1/20) → 데스크톱 복사(1/22) → TechHive 폴더 이동 → 휴지통 이동(1/23). 직접 확인됨.
- USB: 1/22, 1/23, 1/30 세 차례 연결, 1/30 exFAT에서 NTFS로 재포맷.
- 외부 전달: 직접 증거 없음. 6개 파일의 USB 복사 기록도 없다. 정황(Zoom 회의 ID 일치, 발송되지 않은 메시지 초안, USB 연결 시점)만 있다.
- 확정하려면 USB 원본, Dropbox 서버 기록, Discord 서버 기록이 필요하다.

## 도구

Autopsy: 디스크 이미지를 열어 분석 대상 파일 확인

## 문서

- [_](docs/조)
- [털](docs/지)
- [털](docs/지)
