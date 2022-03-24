Linux cmd
------
- ls - 현재 위치의 파일 목록 조회

>
> ls -l : 파일의 상세정보  
>ls -a : 숨김 파일 표시  
>ls -t : 파일들을 생성시간순(제일 최신 것부터)으로 표시  
>ls -rt : 파일들을 생성시간순(제일 오래된 것부터)으로 표시  
>ls -f : 파일 표시 시 마지막 유형에 나타내는 파일명을 끝에 표시
('/' : 디렉터리, '*' : 실행파일, '@' : 링크 등등,,,)

- cd - 디렉터리 이동

>
>cd [디렉터리 경로]  
>cd ~ : 홈 디렉터리로 이동  
>cd / : 최상위 디렉터리로 이동   
>cd . : 현재 디렉터리    
>cd .. : 상위 디렉터리로 이동   
>cd - : 이전 경로로 이동   

- touch - 0바이트 파일 생성, 파일의 날짜와 시간을 수정
- mkdir - 디렉터리 생성
- cp - 파일 복사
- mv - 파일 이동
- rm - 파일 삭제
- cat - 파일의 내용을 화면에 출력, 리다이렉션 기호('>')를 사용하여 새로운 파일 생성
- redirection - 화면의 출력 결과를 파일로 저장
- alias - 자주 사용하는 명령어들을 별명으로 정의하여 쉽게 사용할 수 있도록 설정
    
### vi
[Ref](https://blockdmask.tistory.com/25)
![](https://media.vlpt.us/images/zeesoo/post/2204c682-ccc7-497a-ab16-ccf7c5830fb4/image.png)
> 파일 열기   

- vi [파일명]  
  
> 명령모드 (esc 눌렀을때, vi 처음 들어갔을때)

- 파일의 끝으로 이동할때는 - G
- 한줄 잘라내기 - dd
- 세줄 잘라내기 - 3dd
- 붙여넣기 - p
- 한글자 삭제 - x
- 단어 삭제 - dw
- 실행취소! - u
- 줄의 맨 앞 - o
- 줄의 맨 뒤 - $

> 마지막행 모드 (esc -> : 눌렀을때)

(명령어 뒤에 !를 붙이면 강제로 수행)
- 저장만 : w
- 종료만 : q
- 저장 후 종료 : wq
- 라인 번호 : set nu
- 커서 위치 뒤로 문자열좀 찾자 : ?문자열
- 커서 위치 앞으로 문자열좀 찾자 : /문자열


nano
---
- nano 파일명
- 도움말 표시 : ctrl+g (F1) 
- nano 종료 (혹은 현재의 file buffer를 닫음) : ctrl+x (F2)  
- 현재 편집 중인 파일 저장 : ctrl+o (F3)  
- 문단 행의 끝을 나란히 : ctrl+j (F4) 
- 현재 file에 다른 file의 내용을 추가 : ctrl+r (F5) 
- text 검색 : ctrl+w (F6) 
- 현재의 cursor 위치 표시하기 : ctrl+c (F11) 
- spell check 시작 ctrl+\ search and replace :  ctrl+t (F12) 
- 현재의 line 혹은 선택된 text 삭제(그리고 저장(copy)) : ctrl+k (F9) 
- 붙여넣기 : ctrl+u (F10) 