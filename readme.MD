# Threemonths docker-compose repo
- Threemonths 프로젝트(http://threemonths.net/)의 docker-compose 관련 레포
- nginxproxy컨테이너와 certbot컨테이너를 활용해, 장고서버의 api에 https가 지원되도록 하였음

## 구성
    - proxy 컨테이너 : nginxproxy컨테이너
    - django 컨테이너 : 장고서버
    - certbot 컨테이너 : SSL 인증서 발급 등 https 지원을 위함

## 필요한 파일과 경로
    - .env파일을 docker-compose파일과 동일한 경로에 둘 것 : docker-compose에 적용할 환경변수를 위함
    - git_access_token_env.sh을 docker-compose파일과 동일한 경로에 둘 것 : build과정에서 dockerfile에 적용할 환경변수를 위함
    - secret_settings.py을 django폴더 내부에 저장

## 명령어
    - source git_access_token_env.sh : dockerfile을 위한 환경변수 등록
    - docker-compose build --build-arg GIT_ACCESS_TOKEN=$GIT_ACCESS_TOKEN && docker-compose up -d : 이미지 빌드 & 구동

# 

## 특이사항
### SSL인증서 첫발급
    - docker-compose certbot컨테이너의 command 부분에서 첫발급 부분 활성화(dry-run으로 꼭 테스트 해보고나서 실행할 것!!)
    - nginx/nginx.conf에서 ssl관련 server부분 비활성화 > 성공적으로 인증서를 발급받았을 경우 다시 활성화할 것!

### SSL인증서 발급 후 정상작동시
    - docker-compose certbot컨테이너의 command 부분에서 재발급 부분 활성화(역시 dry-run으로 꼭 테스트 해보고나서 실행할 것!!)
    - nginx/nginx.conf에서 ssl관련 server부분 다시 활성화
    - crontab에서 환경변수, 명령어 설정(https://www.notion.so/1-Docker-b382aa799a8c4e4ca8c4caf9ebfd7b2d#9963a197b0a0473c81720cd837e919a8)
        

### 도메인을 수정할 경우
    - .env파일의 Domain 환경변수를 수정
    - nginx/nginx.conf 파일에 있는 domain정보를 수정(총 6개를 수정해줘야 함)
