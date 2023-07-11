

# **ToDo App**
#### 웹사이트 링크 : <https://gunw-todolist.netlify.app>
<br />

> ***프로젝트*** : 일과 생활을 관리해주는 Todo App
>
> ***프로젝트 분류*** : 개인 프로젝트
>
> ***팀규모*** : 프론트엔드(1)
>
> ***참여분야*** : 프로젝트|디자인 기획, 클라이언트 개발

<br />
<br />
<br />


# 👨‍🔧 **기술**

![Vue](https://img.shields.io/badge/Vue3-4FC08D?style=Vue.js&logo=Vue.js&logoColor=white)
![Vuex](https://img.shields.io/badge/Vuex-4FC08D?style=Vuex&logo=Vuex&logoColor=white)
![Sass](https://img.shields.io/badge/Sass-CC6699?style=Vuex&logo=Sass&logoColor=white)
![Webpack](https://img.shields.io/badge/Webpack-8DD6F9?style=Webpack&logo=Webpack&logoColor=white)
<br />
<!-- 
#### *왜 이 기술을 사용했는가?*  

<br />
<br />

<!-- # 👪 **협업** -->
<!-- ![Figma](https://img.shields.io/badge/figma-F24E1E?style=figma&logo=figma&logoColor=white)
![GitHub](https://img.shields.io/badge/github-181717?style=github&logo=github&logoColor=white) -->

<br />
<br />

# 👀 **기능**
<br />
<!-- 체크박스 -->

## **1. 체크박스**  
_src/pages/Brand:90_

<img width='80%' src='https://user-images.githubusercontent.com/74530907/250579327-611c017d-526a-4d60-934c-307e1e075921.gif' />

> 1차카테고리 : 브랜드  
> 2차카테고리 : 차급(Segment), 연료(FuleType)  
> 체크박스 형식의 카테고리를 설정하면 해당되는 차량만 필터링되어 보여줍니다.

<br />
<Hr />
<br />
<!-- 검색 -->

## **2. 검색**  
_src/components/SearchBar_

<img width='80%' src='https://user-images.githubusercontent.com/74530907/250912291-bd7c3785-1b01-4f46-8de1-9fb28ec54839.gif' />

> 차량에 이름을 검색이 가능하며 빠르게 상세페이지 링크를 제공합니다.

<br />
<Hr />
<br />
<!-- 상세페이지 -->

## **3. 상세페이지 Header**  
_src/pages/Detail:200_

<img width='80%' src='https://github.com/pgw6541/SEMOCAR/assets/74530907/98cdf9ef-f40e-4816-adea-aa205a5bfd60' />

> 스크롤하여 자동차이름, 이미지가 있는 단락이 화면에서 사라지면  
> 화면 최상단에 Fixed요소가 나옵니다.  

<br />
<Hr />
<br />

## **4. 스크롤 위치 이동**  
_src/pages/Detail:183_

<img width='80%' src='https://github.com/pgw6541/SEMOCAR/assets/74530907/04a484d6-d759-4a8f-a474-8b3c46291ed8' />

> 상세페이지 Navigation 버튼 클릭시 해당요소가 있는 스크롤위치로 이동합니다.  
> useRef로 DOM에 접근해 해당 요소 상단으로 이동하게끔 구현했습니다.

<br />
<Hr />
<br />


## **5. 등급및 제원**  
_src/pages/Detail:234_

<img width='80%' src='https://user-images.githubusercontent.com/74530907/250577293-015f760e-352c-4c17-b75d-bd470ab0de38.gif' />
> 1차 카테고리 : 차량의 등급(grades)  
> 2차 카테고리 : 차량의 트림(Trim)  
> 1차, 2차카테고리를 지정하면 해당 가격, 제원등을 아래단락에서 나타냅니다.

<br />
<Hr />
<br />

## **6. 캐러셀 슬라이드**
**배너** _src/pages/Main:79_  
**포토갤러리** _src/pages/Detail:549_

<img width='50%' src='https://user-images.githubusercontent.com/74530907/250577043-a3c03a91-be06-4ef0-afea-df31af017fc3.gif' /><img width='50%' src='https://user-images.githubusercontent.com/74530907/250576700-47e73051-bb43-46cf-885c-e96f9b400245.gif' />

> 메인페이지 배너, 최신 출시모델 상세페이지 차량외부, 내부에서 이미지 슬라이드를 구현하였습니다.

> Swiper 라이브러리를 사용하였습니다. <https://swiperjs.com/>

<br />
<Hr />
<br />

# 🗒️기획  

> 디자인과 기능을 다음자동차 웹사이트를 참고하였습니다.  

<br />

전체적인 웹사이트 목표  
차량 상세한 정보를 사용자에게 제공하는 것입니다.  
차량 검색, 차량 카테고리로 분류, 상세제원 제공, 추가로 비교기능을 기획하고있습니다.

대상 사용자 정의  
주요 사용자는 차량 구매를 고려하거나 관심이 있는 차량에 