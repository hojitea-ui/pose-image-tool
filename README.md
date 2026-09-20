# 원하는 포즈로 이미지 만드는 도구 (ControlNet OpenPose)

## 도구 설명
ControlNet과 OpenPose를 활용하여 참조 인물 사진에서 관절 포즈(Skeleton)를 추출하고, 설정한 프롬프트를 통해 **지정한 포즈를 그대로 따라 하는 새로운 이미지를 생성하는 튜토리얼 도구**입니다.

## 사용법
1. **Colab 실행 환경 설정**
   - Google Colab에서 `pose_tool.ipynb` 노트를 엽니다.
   - 상단 메뉴 [런타임] - [런타임 유형 변경]에서 `T4 GPU`를 선택합니다.
2. **셀 순서대로 실행**
   - **[셀 1]**: 필수 라이브러리(`controlnet-aux`, `diffusers` 등) 설치 및 ControlNet OpenPose 모델 로드
   - **[셀 2]**: 참조 이미지(`samples/pose_01.png` 또는 `samples/pose_02.png`) 업로드 및 관절(Pose) 추출
   - **[셀 3]**: 프롬프트 입력 및 ControlNet 파이프라인으로 조건부 이미지 생성
   - **[셀 4]**: 최종 생성 결과를 `samples/output_01.png` 또는 `samples/output_02.png`로 저장
3. **결과 확인**
   - 생성된 이미지 파일은 `/content/samples/` 디렉토리에 저장이 완료됩니다.

## 테스트 결과

| 구분 | 포즈 1 (네온 사이버 수트) | 포즈 2 (피겨 스케이터) |
| :--- | :--- | :--- |
| **참조 포즈** | `samples/pose_01.png` | `samples/pose_02.png` |
| **결과 이미지** | `samples/output_01.png` | `samples/output_02.png` |
| **프롬프트** | `a cyberpunk warrior with neon lights...` | `a figure skater on ice rink, snowing background...` |
| **결과 평가** | **[성공]** 원본의 상체 기울임과 양팔을 벌린 동적인 포즈가 네온 수트를 입은 SF 캐릭터에 정확히 적용됨. | **[성공]** 한쪽 다리를 뒤로 접어 올린 발랄한 동작이 피겨 스케이팅 연주 포즈와 자연스럽게 결합됨. |

## 한계 및 관찰 소감
- **장점:** 참조 사진의 원래 의상이나 배경에 구애받지 않고 오직 '인물의 신체 관절 위치'만 조건으로 활용하므로, 전혀 다른 컨셉(SF, 피겨 스케이팅)의 프롬프트와 결합해도 포즈가 안정적으로 유지됨.
- **한계:** SD v1.5 기반 파이프라인 특성상 손가락 세부 마디나 정교한 이목구비 형태는 일부 뭉개지거나 손가락 개수 왜곡이 나타나는 경우가 있음.