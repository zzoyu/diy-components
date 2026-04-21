# diy-components

CadQuery 기반 3D 프린팅 설계 컴포넌트 모음 Repository

## 디렉터리 구조

```
diy-components/
├── components/
│   ├── mechanical/       # 기본 부품
│   ├── electronics/      # HW 프로젝트 컴포넌트
│   ├── pegboard/         # 각종 타공판 악세사리
│   └── printing/         # 3D 프린팅 유틸리티 컴포넌트
├── projects/             # 프로젝트 폴더
│   └── <project_name>/   # 개별 프로젝트 폴더
├── exports/              # 생성된 STL / STEP 파일 (git 제외)
├── scripts/              # 유틸리티 스크립트
├── tests/                # 테스트 코드
└── environment.yml       # conda 환경 정의
```

## 환경 설정

```bash
conda env create -f environment.yml
conda activate diy-components
```

## 사용 방법

### 개별 컴포넌트 사용

```python
import cadquery as cq
from components.mechanical.bolt import make_bolt
from components.mechanical.nut import make_nut
from components.mechanical.gear import make_gear
from components.electronics.enclosure import make_enclosure
from components.pegboard.hook import make_hook
from components.printing.cable_clip import make_cable_clip

# M6×20 볼트
bolt = make_bolt(diameter=6, length=20)

# 인클로저 (본체 + 뚜껑)
body, lid = make_enclosure(width=100, depth=70, height=45, vent_holes=True)

# Skadis 훅
hook = make_hook(wire_length=60, style="single")

# 케이블 클립
clip = make_cable_clip(cable_diameter=5)
```

### 전체 내보내기

```bash
# STL + STEP 동시 내보내기 (기본)
python scripts/export_all.py

# STL만 내보내기
python scripts/export_all.py --format stl

# 특정 카테고리만
python scripts/export_all.py --category pegboard --format stl
```

### 테스트

```bash
pytest tests/ -v
```

## 컴포넌트 목록

### 기계 부품 (`components/mechanical/`)

| 모듈      | 함수          | 주요 파라미터                               |
| --------- | ------------- | ------------------------------------------- |
| `bolt.py` | `make_bolt()` | `diameter`, `length`, `head_style`          |
| `nut.py`  | `make_nut()`  | `diameter`, `thickness`                     |
| `gear.py` | `make_gear()` | `module`, `teeth`, `width`, `bore_diameter` |

### 전자 부품 케이스 (`components/electronics/`)

| 모듈           | 함수                     | 주요 파라미터                            |
| -------------- | ------------------------ | ---------------------------------------- |
| `pcb_mount.py` | `make_pcb_standoff()`    | `height`, `od`, `screw_diameter`         |
| `pcb_mount.py` | `make_pcb_mount_plate()` | `width`, `depth`, `standoff_height`      |
| `enclosure.py` | `make_enclosure()`       | `width`, `depth`, `height`, `vent_holes` |

### IKEA Skadis 페그보드 (`components/pegboard/`)

> 홀 간격 20 mm, 홀 직경 5 mm 기준으로 설계됨.

| 모듈            | 함수           | 주요 파라미터                                          |
| --------------- | -------------- | ------------------------------------------------------ |
| `hook.py`       | `make_hook()`  | `wire_length`, `style` (`single`/`double`), `peg_rows` |
| `shelf.py`      | `make_shelf()` | `width`, `depth`, `height`, `peg_columns`              |
| `bin_holder.py` | `make_bin()`   | `width`, `depth`, `height`, `drain_holes`              |

### 3D 프린팅 유틸 (`components/printing/`)

| 모듈            | 함수                | 주요 파라미터                                   |
| --------------- | ------------------- | ----------------------------------------------- |
| `base_plate.py` | `make_base_plate()` | `width`, `depth`, `hole_diameter`, `hole_pitch` |
| `cable_clip.py` | `make_cable_clip()` | `cable_diameter`, `opening_ratio`, `mount_hole` |

## 새 컴포넌트 추가 방법

1. 해당 카테고리 폴더에 `.py` 파일 생성
2. `make_<name>()` 함수를 정의하고 `cq.Workplane` 또는 `cq.Assembly` 반환
3. `tests/test_components.py`에 스모크 테스트 추가
4. `scripts/export_all.py`의 해당 섹션에 `export()` 호출 추가
