# 실습 과제 2: Agibot Toy2Box 모방학습 성공률 향상 연구

Agibot 오른팔로 장난감을 상자에 넣는(Toy2Box) 작업의 모방학습 데이터셋입니다.

- 환경: `Isaac-Place-Toy2Box-Agibot-Right-Arm-RmpFlow-v0`
- Mimic 환경: `Isaac-Place-Toy2Box-Agibot-Right-Arm-RmpFlow-Rel-Mimic-v0`
- 코스 저장소: IsaacLab_RS

## 데이터셋

| 파일 | 크기 | 데모 수 | 총 스텝 수 |
|---|---|---|---|
| [toy2box_human_all.hdf5](https://github.com/brownporkcutlet/Agibot-Toy2Box-Imitation-Learning/releases/download/v1.0-datasets/toy2box_human_all.hdf5) | 42 MB (44,027,842 B) | 100 | 61,134 |
| [toy2box_mimic_500_final.hdf5](https://github.com/brownporkcutlet/Agibot-Toy2Box-Imitation-Learning/releases/download/v1.0-datasets/toy2box_mimic_500_final.hdf5) | 240 MB (251,061,084 B) | 500 | 310,889 |

- **toy2box_human_all.hdf5**: 키보드 원격조작으로 수집한 사람 시연 100개입니다. 20개씩 5세트를 합쳤고, 각 데모의 `source_file` / `source_demo` 속성에 원본 파일과 데모 번호가 남아 있습니다.
- **toy2box_mimic_500_final.hdf5**: 사람 시연에 서브태스크 주석을 단 파일로 Isaac Lab Mimic을 돌려 만든 성공 데모 500개입니다. datagen seed 1에서 378개, seed 2에서 122개를 얻었습니다(첫 실행이 메모리 부족으로 중단되어 seed 2로 이어서 생성). 보간 15스텝, 행동 노이즈 0.01을 적용했습니다.

파일 용량 때문에 데이터셋은 git이 아니라 [Release v1.0-datasets](https://github.com/brownporkcutlet/Agibot-Toy2Box-Imitation-Learning/releases/tag/v1.0-datasets)에 첨부되어 있습니다.

## 다운로드

```bash
mkdir -p ~/IsaacLab_RS/datasets && cd ~/IsaacLab_RS/datasets
wget https://github.com/brownporkcutlet/Agibot-Toy2Box-Imitation-Learning/releases/download/v1.0-datasets/toy2box_human_all.hdf5
wget https://github.com/brownporkcutlet/Agibot-Toy2Box-Imitation-Learning/releases/download/v1.0-datasets/toy2box_mimic_500_final.hdf5
```

## 사용법

파일을 `~/IsaacLab_RS/datasets/`에 두고 IsaacLab_RS 루트에서 robomimic BC 학습을 실행합니다.

```bash
./isaaclab.sh -p scripts/imitation_learning/robomimic/train.py --task Isaac-Place-Toy2Box-Agibot-Right-Arm-RmpFlow-v0 --algo bc --dataset ./datasets/toy2box_mimic_500_final.hdf5
```
