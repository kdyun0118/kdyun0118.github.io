# kdyun0118.github.io

This website is based on a template by [Keunhong Park](https://github.com/keunhong/keunhong.github.io)


## 💻 로컬에서 실행하기 (Local Development)

GitHub에 푸시하기 전, 로컬 환경에서 사이트를 미리 볼 수 있습니다.

1.  **저장소 클론**
    ```bash
    git clone [https://github.com/](https://github.com/)[your-username]/[project-repo-name].git
    cd [project-repo-name]
    ```

2.  **Conda 환경 설정**
    이 프로젝트는 Ruby 및 관련 빌드 도구를 위해 Conda 환경을 사용하는 것을 권장합니다.
    ```bash
    # (처음 한 번만) jekyll-env라는 이름의 환경 생성
    conda create -n jekyll-env
    conda activate jekyll-env
    
    # 컴파일러 및 필수 라이브러리 설치
    conda install -c conda-forge gcc gxx make openssl pkg-config ruby
    ```

3.  **Ruby Gem 설치**
    Bundler를 사용해 Gemfile에 명시된 모든 종속성을 설치합니다.
    ```bash
    bundle install
    ```

4.  **Jekyll 서버 실행**
    ```bash
    bundle exec jekyll serve
    ```

5.  **브라우저에서 확인**
    웹 브라우저에서 `http://127.0.0.1:4000` (또는 `http://localhost:4000`) 주소로 접속합니다.

## 새로운 항목 추가하기

### 프로필 변경
`_config.yml` 파일을 편집하여 이름, 소속, 이메일, 소셜 미디어 링크 등을 수정합니다.
- **주의**: `_config.yml` 변경 후에는 Jekyll 서버를 재시작해야 합니다.

### 새로운 Author 추가
`_data/authors.yml`에 새로운 저자 정보를 추가합니다.
- `is_me: true`는 본인에게만 설정합니다.

### 새로운 Publication 추가

#### 1. Publication 항목 추가
`_data/publications.yml`에 새로운 항목을 추가합니다.

#### 2. 이미지/영상 파일 준비
이미지와 영상 파일을 `images/` 디렉토리에 추가합니다.


**권장 파일 형식:**
- **썸네일 이미지** (`image`):
  - 형식: JPG 또는 PNG
  - 해상도: 1280×720px (16:9 비율) 권장 = 영상과 동일하게
  - 파일 크기: 200KB 이하 권장

- **호버 영상** (`image_mouseover`):
  - 형식: MP4 (H.264 코덱)
  - 해상도: 360p (640×360) 권장
  - 프레임 레이트: 24fps 또는 30fps
  - 파일 크기: 2MB 이하 권장

#### 3. 영상 최적화 (ffmpeg 사용)

영상 정보 확인 
```bash
ffmpeg -i input.mp4
```

영상 파일 용량을 줄이고 웹에 최적화하려면 다음 명령어를 사용하세요:

e.g. (1280×720px) 영상 -> (640×360px) 영상

**기본 최적화 (해상도 고정):**
```bash
ffmpeg -i input.mp4 -vcodec libx264 -crf 28 -an -s 640x360 -pix_fmt yuv420p output.mp4
```

**권장 최적화 (가로 비율 유지):**
```bash
ffmpeg -i input.mp4 \
  -vcodec libx264 \
  -crf 28 \
  -an \
  -vf "scale=640:-1" \
  -pix_fmt yuv420p \
  -movflags +faststart \
  output.mp4
```

**옵션 설명:**
- `-vcodec libx264`: H.264 코덱 사용
- `-crf 28`: 압축률 (22-28 사이 권장, 숫자 높을수록 파일 작아짐)
- `-an`: 오디오 제거
- `-vf "scale=640:-1"`: 가로 640px, 세로는 비율 유지 ("scale=640:-2"`이면 비율을 유지하되 가장 가까운 짝수로)
- `-pix_fmt yuv420p`: 브라우저 호환성
- `-movflags +faststart`: 웹 스트리밍 최적화 