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

