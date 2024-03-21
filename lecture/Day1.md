# SSH 접속

```
# SSH 키생성
ssh-keygen -t rsa -f ~/.ssh/first-s
sh-key -C ubuntu -b 2048

# 경로 이동
cd ~/.ssh

# pubulic key 확인 및 복사
cat first-ssh-key.pub


```
복사한 public key를 GCP-메타데이터-SSH 키에 저장
![](2024-03-20-10-39-56.png)


ssh 접속
~~~
ssh -i ~/.ssh/first-ssh-key ubuntu@34.47.88.72 #외부IP
~~~

# Miniconda 설치
링크 주소 복사
![](2024-03-20-11-57-54.png)


```
# 서버에 설치(wget)
get https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh

# sh파일 실행
bash ./Miniconda3-latest-Linux-x86_64.sh 

# 가상환경 활성화 후, poetry 설치
pip install poetry

# pyproject.toml 파일을 저장할 디렉토리 생성 및 이동
mkdir (디렉토리 명)
cd (디렉토리 명)

# project init (현재 디렉토리에 pyproject.toml을 생성)
poetry init

# 패키지 추가
poetry add (package) # e.g. pandas
```
**pyproject.toml 내용**
![](2024-03-20-12-00-31.png)