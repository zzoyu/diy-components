# 3D Printing DIY Components

CadQuery, Build123d 기반 3D 프린팅 설계 컴포넌트 모음 Repository
둘 다 조금 깔짝거려보다가 마음에 드는 라이브러리로 정착 예정

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

# FYI

- [CadQuery Documentation](https://cadquery.readthedocs.io/en/latest/index.html)
- [Build123d Documentation](https://build123d.readthedocs.io/en/latest/index.html)
