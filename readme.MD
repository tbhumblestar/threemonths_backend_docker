# Threemonths docker-compose repo
- Threemonths 프로젝트(https://threemonths.net/)의 docker-compose 관련 레포

<br/>

### 구성
- proxy 컨테이너 : nginxproxy컨테이너
- django 컨테이너 : 장고서버
- certbot 컨테이너 : https 프로토콜을 위한 인증서 발급

<br/>

### 필요한 파일
- 공통
    - restart.sh : Git Access token 환경변수 등록 + 기존 컨테이너 / 이미지 / 볼륨 삭제 + 이미지 빌드 후 서버 재시작
    - .env : docker-compose에 전달할 환경변수

</br>

- Django 컨테이너
    - Dockerfile
    - secret_settings.py

</br>

- Nginx
    - nginx/templates/nginx.conf.template : envburst를 통해 환경변수를 전달하기 위함
    - nginx/nginx.conf : nginx의 설정파일


<br/>

### 특이사항
- LetsEncrypt의 인증서는 90일마다 만료되므로, crontab기능을 활용해 80일마다 lets'encrypt컨테이너가 재실행되도록 설정

<br/>

---

<br/>

## 상황별 주의사항

### SSL인증서 첫발급
- docker-compose certbot컨테이너의 command 부분에서 첫발급 부분 활성화(dry-run으로 꼭 테스트 해보고나서 실행할 것!!)
- nginx/nginx.conf에서 ssl관련 server부분 비활성화 > 성공적으로 인증서를 발급받았을 경우 다시 활성화할 것!

</br>

### SSL인증서 발급 후 정상작동시
- docker-compose certbot컨테이너의 command 부분에서 재발급 부분 활성화(역시 dry-run으로 꼭 테스트 해보고나서 실행할 것!!)
- nginx/nginx.conf에서 ssl관련 server부분 다시 활성화
- crontab에서 환경변수, 명령어 설정(https://www.notion.so/1-Docker-b382aa799a8c4e4ca8c4caf9ebfd7b2d#9963a197b0a0473c81720cd837e919a8)
        
</br>

### 도메인변경
- .env파일의 domain 환경변수를 수정하면, docker-compose를 통해 Nginx컨테이너에 전달됨

</br>

### 서버 환경 설정
- .env파일의 server_environment 환경변수를 수정하면 자동으로 docker-compose를 통해 Django서버에 전달됨

</br>



