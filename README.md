<h2 align="center">Finding_Shelter</h2>
  
<div align="center">
    <img width="554" alt="스크린샷" src="https://github.com/user-attachments/assets/e1fce1ed-cca7-4892-9b55-c4c64122a1a1" />
</div>

> 2023년 5월 31일 오전 06시 32분 서울특별시 2023년 북한 천리마-1 발사 사건에 대한 경계경보를 발령했으나 이후 오발령으로 밝혀진 사건을 계기로 대피소 찾기 서비스를 만들게 되었다. 

### 서비스 기능 
- 대피소 현황 데이터(공공 데이터)를 관리하고 있다 라고 가정하고, 대피소 현황 데이터는 위도 경도의 위치 정보 데이터를 가지고 있다.
- 해당 서비스로 주소 정보를 입력하여 요청하면 위치 기준에서 가까운 대피소 3 곳을 추출한다.
- 주소는 도로명 주소 또는 지번을 입력하여 요청받는다.
  - 정확한 주소를 입력받기 위해 [Kakao 우편번호 서비스](https://postcode.map.daum.net/guide) 사용   
- 주소는 정확한 상세 주소(동, 호수)를 제외한 주소 정보를 이용하여 추천한다.   
  - ex) 서울 성북구 종암로 10길
- 입력받은 주소를 위도, 경도로 변환하여 기존 대피소 데이터와 비교 및 가까운 대피소를 찾는다.   
  - 지구는 평면이 아니기 때문에, 구면에서 두 점 사이의 최단 거리 구하는 공식이 필요    
  - 두 위 경도 좌표 사이의 거리를 [haversine formula](https://en.wikipedia.org/wiki/Haversine_formula)로 계산  
  - 지구가 완전한 구형이 아니 므로 아주 조금의 오차가 있다.   
- 입력한 주소 정보에서 정해진 반경(10km) 내에 있는 대피소만 추천한다.   
- 추출한 대피소 데이터는 길안내 URL 및 로드뷰 URL로 제공한다.   
  - ex)    
  길안내 URL : https://map.kakao.com/link/map/우리회사,37.402056,127.108212    
  로드뷰 URL : https://map.kakao.com/link/roadview/37.402056,127.108212     

- 길 안내 URL은 고객에게 제공되기 때문에 가독성을 위해 shorten url로 제공한다.
- shorten url에 사용되는 key 값은 인코딩하여 제공한다.
  - base62를 통한 인코딩    
- shorten url의 유효 기간은 30일로 제한한다.   

</br>

### 사용 방법
대피소 메인 페이지
> “빠르게 대피소 찾기”를 클릭하면 Kakao 우편번호 서비스로 이동한다. 주소 입력 창에 현위치 정보를 입력하여 요청한다.
<img width="1373" alt="스크린샷 2024-12-27 오후 5 55 53" src="https://github.com/user-attachments/assets/0068d01d-0935-478d-8951-2313c980692a" />

주소는 도로명 주소 또는 지번을 입력하여 요청 받는다.

주소는 정확한 상세 주소(동, 호수)를 제외한 주소 정보를 이용하여 추천한다.

* ex) 서울 광운로 20

</br>

대피소 길 안내 페이지
> 입력한 주소 위치 기준에서 정해진 반경(10km) 내에 있는 대피소 3곳을 가까운 순서대로 추천해준다. 연결된 링크를 통해 카카오 맵으로 이동해 바로 길찾기를 할 수 있다.

대피소의 이름, 대피소 주소, 입력 주소와 대피소 사이의 거리 또한 알 수 있다.

<img width="1373" alt="스크린샷 2024-12-27 오후 5 56 04" src="https://github.com/user-attachments/assets/712b2ef2-6d65-4fa3-a4cb-c4f1c94e21aa" />

</br>

> 추출한 대피소 데이터의 “카카오 맵에서 길찾기”에서는 길안내를 제공한다.

KakaoMap으로 이동하여 길 찾기를 할 수 있도록 한다.

<img width="1373" alt="스크린샷 2024-12-27 오후 5 56 17" src="https://github.com/user-attachments/assets/a1a12733-7f11-4691-beb3-bf5d336af3e9" />

</br>

> “로드뷰 보기”를 클릭하면 대피소 주변을 확인하여 정확한 위치를 파악할 수 있도록 한다.

<img width="1373" alt="스크린샷 2024-12-27 오후 5 56 27" src="https://github.com/user-attachments/assets/f11992ae-767e-458b-a41a-ef518252d23f" />

</br>

</br>

대피 요령 안내 페이지
> 위급 상황 발생 시 긴급 대피 요령을 확인한다.

<img width="1373" alt="스크린샷 2024-12-27 오후 5 55 21" src="https://github.com/user-attachments/assets/a4d04520-2070-43cb-90c9-eefc32a1237c" />

</br>

### 개발 기능 
- Spring Data JPA를 이용한 CRUD 메서드 구현하기        
- 카카오 주소검색 API 연동하여 주소를 위도, 경도로 변환하기   
- 추천 결과를 카카오 지도 URL로 연동하여 제공하기   
- 공공 데이터를 활용하여 개발하기 (대피소 현황 데이터)    
- base62를 이용한 shorten url 개발하기 (길안내 URL)    

</br>

### 기술 스택   
- JDK 17
- Spring Boot 3.1.5
- Spring Data JPA
- Gradle
- Lombok
- Github
- MariaDB  

</br>

### 오픈 API 및 공공 데이터 
[외부 API(카카오 주소 검색 API](https://developers.kakao.com/docs/latest/ko/local/dev-guide))와 [공공 데이터(대피소 현황 정보)를 활용

추천된 대피소 길 안내는 [카카오 지도 및 로드뷰 바로가기 URL](https://apis.map.kakao.com/web/guide/#routeurl)로 
제공된다.     

[카카오 키워드 장소 검색 api](https://developers.kakao.com/docs/latest/ko/local/dev-guide#search-by-category)를 
이용하여 적용

</br>

### License
이 프로젝트는 MIT License를 따른다.

이 소프트웨어를 누구라도 무상으로 제한없이 취급해도 좋다. 단, 저작권 표시 및 이 허가 표시를 소프트웨어의 모든 복제물 또는 중요한 부분에 기재해야 한다.

저자 또는 저작권자는 소프트웨어에 관해서 아무런 책임을 지지 않는다.
