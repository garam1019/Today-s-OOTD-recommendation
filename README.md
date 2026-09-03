<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>오늘의 OOTD</title>
<style>
  :root{
    --cream: #FFF8E7;
    --cream-deep: #FFF1CE;
    --yellow: #FFD452;
    --yellow-deep: #F4A825;
    --sky: #8FCBE8;
    --sky-deep: #4F9FC7;
    --brown: #6B4A2B;
    --brown-dark: #4A3218;
    --white: #FFFFFF;
    --coral: #FF9770;
    --shadow: rgba(107, 74, 43, 0.18);
  }

  *{ box-sizing: border-box; }

  body{
    margin: 0;
    min-height: 100vh;
    background: radial-gradient(circle at 20% 0%, var(--cream-deep), var(--cream) 60%);
    font-family: "Apple SD Gothic Neo", "Malgun Gothic", "Segoe UI", -apple-system, BlinkMacSystemFont, sans-serif;
    color: var(--brown-dark);
    display: flex;
    justify-content: center;
    padding: 32px 16px 64px;
  }

  .wrap{ width: 100%; max-width: 560px; }

  header{ text-align: center; margin-bottom: 24px; }

  header .badge{
    display: inline-block;
    background: var(--sky);
    color: var(--brown-dark);
    font-weight: 800;
    font-size: 15px;
    padding: 6px 16px;
    border-radius: 999px;
    margin-bottom: 14px;
  }

  h1{ font-size: 32px; margin: 0 0 10px; font-weight: 900; }

  header p{ font-size: 16px; color: var(--brown); margin: 0; line-height: 1.5; }

  .panel{
    background: var(--white);
    border-radius: 28px;
    padding: 30px 26px;
    box-shadow: 0 14px 32px var(--shadow);
    text-align: center;
  }

  .screen{ display: none; }
  .screen.active{ display: block; animation: fadeIn 0.35s ease; }

  @keyframes fadeIn{
    from{ opacity: 0; transform: translateY(8px); }
    to{ opacity: 1; transform: translateY(0); }
  }

  .big-emoji{ font-size: 70px; margin-bottom: 8px; }

  .desc-text{ font-size: 17px; color: var(--brown); line-height: 1.6; margin: 10px 0 26px; }

  .primary-btn{
    background: var(--yellow-deep);
    color: var(--brown-dark);
    border: none;
    border-radius: 16px;
    padding: 16px 20px;
    font-size: 18px;
    font-weight: 800;
    cursor: pointer;
    font-family: inherit;
    width: 100%;
    transition: transform 0.15s ease, background 0.15s ease;
  }
  .primary-btn:hover{ background: var(--yellow); transform: translateY(-2px); }

  .secondary-btn{
    background: var(--cream);
    color: var(--brown-dark);
    border: 2px solid var(--yellow-deep);
    border-radius: 16px;
    padding: 14px 20px;
    font-size: 16px;
    font-weight: 700;
    cursor: pointer;
    font-family: inherit;
    width: 100%;
    margin-top: 10px;
    transition: transform 0.15s ease, background 0.15s ease;
  }
  .secondary-btn:hover{ background: var(--yellow); transform: translateY(-2px); }

  .status-text{ font-size: 15px; color: var(--brown); margin-top: 14px; min-height: 20px; }

  .error-box{
    background: #FFF0E9;
    border: 2px solid var(--coral);
    border-radius: 14px;
    padding: 14px 16px;
    font-size: 15px;
    color: #B84B25;
    margin-top: 16px;
    text-align: left;
    display: none;
  }

  /* 위치 확인 화면 */
  .location-card{
    background: linear-gradient(160deg, var(--sky), var(--sky-deep));
    color: var(--white);
    border-radius: 20px;
    padding: 24px 18px;
    margin-bottom: 22px;
  }
  .location-card .loc-name{ font-size: 24px; font-weight: 900; margin: 4px 0; }
  .location-card .loc-sub{ font-size: 15px; opacity: 0.95; }

  .yes-no-row{ display: flex; gap: 10px; }
  .yes-no-row button{ flex: 1; }
  .no-btn{
    background: var(--white);
    color: var(--brown-dark);
    border: 2px solid #D8C7A8;
  }
  .no-btn:hover{ background: var(--cream); }

  /* 검색 화면 */
  .search-row{ display: flex; gap: 8px; margin-bottom: 16px; }
  .search-row input{
    flex: 1;
    padding: 14px 16px;
    border-radius: 14px;
    border: 2px solid var(--yellow-deep);
    font-size: 16px;
    font-family: inherit;
    background: var(--cream);
    color: var(--brown-dark);
  }
  .search-row input:focus{ outline: none; border-color: var(--coral); }
  .search-row button{ width: auto; padding: 14px 20px; }

  .search-result-item{
    background: var(--cream);
    border-radius: 14px;
    padding: 14px 16px;
    margin-bottom: 10px;
    text-align: left;
    cursor: pointer;
    font-size: 16px;
    font-weight: 700;
    border: 2px solid transparent;
    transition: border 0.15s ease, background 0.15s ease;
  }
  .search-result-item:hover{ border-color: var(--yellow-deep); background: var(--yellow); }
  .search-result-item span{
    display: block;
    font-size: 13px;
    font-weight: 500;
    color: var(--brown);
    margin-top: 2px;
  }

  /* 결과 화면 */
  .weather-summary{
    background: linear-gradient(160deg, var(--yellow), var(--yellow-deep));
    border-radius: 22px;
    padding: 26px 18px;
    margin-bottom: 22px;
  }
  .weather-summary .w-emoji{ font-size: 64px; }
  .weather-summary .w-temp{ font-size: 40px; font-weight: 900; margin: 4px 0; color: var(--brown-dark); }
  .weather-summary .w-label{ font-size: 17px; font-weight: 700; color: var(--brown-dark); }
  .weather-summary .w-sub{ font-size: 14px; color: var(--brown); margin-top: 6px; }

  .outfit-grid{
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 12px;
    margin-bottom: 16px;
    text-align: left;
  }

  .outfit-card{
    background: var(--cream);
    border-radius: 16px;
    padding: 16px;
  }
  .outfit-card .oc-label{
    font-size: 13px;
    font-weight: 800;
    color: var(--sky-deep);
    margin-bottom: 6px;
  }
  .outfit-card .oc-value{ font-size: 15px; font-weight: 700; line-height: 1.4; color: var(--brown-dark); }

  .umbrella-box{
    border-radius: 16px;
    padding: 16px;
    margin-bottom: 16px;
    text-align: left;
    font-size: 15px;
    font-weight: 700;
  }
  .umbrella-yes{ background: #E6F3FA; color: var(--sky-deep); border: 2px dashed var(--sky-deep); }
  .umbrella-no{ background: var(--cream); color: var(--brown); border: 2px dashed #D8C7A8; }

  .tip-box{
    background: #FFF3E0;
    border-radius: 16px;
    padding: 14px 16px;
    font-size: 14px;
    color: var(--brown);
    line-height: 1.5;
    margin-bottom: 22px;
    text-align: left;
  }

  @media (max-width: 420px){
    h1{ font-size: 26px; }
    .outfit-grid{ grid-template-columns: 1fr; }
  }
</style>
</head>
<body>
<div class="wrap">

  <header>
    <span class="badge">오늘의 날씨 코디</span>
    <h1>👕 날씨 기반 OOTD</h1>
    <p>지금 날씨에 딱 맞는 옷차림과 신발, 우산까지 한 번에 추천해드려요.</p>
  </header>

  <div class="panel">

    <!-- 화면 1: 시작 -->
    <div class="screen active" id="screen-start">
      <div class="big-emoji">📍</div>
      <p class="desc-text">내 위치의 실시간 날씨를 불러와서<br>오늘 입을 옷을 추천해드릴게요.</p>
      <button class="primary-btn" id="btn-start">내 위치로 날씨 확인하기</button>
      <div class="status-text" id="start-status"></div>
      <div class="error-box" id="start-error"></div>
    </div>

    <!-- 화면 2: 위치 확인 -->
    <div class="screen" id="screen-confirm">
      <div class="location-card">
        <div style="font-size:14px; opacity:0.9;">현재 감지된 위치</div>
        <div class="loc-name" id="confirm-loc-name">-</div>
        <div class="loc-sub" id="confirm-loc-sub">-</div>
      </div>
      <p class="desc-text">이 위치가 맞나요?</p>
      <div class="yes-no-row">
        <button class="primary-btn" id="btn-yes">예, 맞아요</button>
        <button class="secondary-btn no-btn" id="btn-no">아니요</button>
      </div>
    </div>

    <!-- 화면 3: 직접 검색 -->
    <div class="screen" id="screen-search">
      <div class="big-emoji">🔍</div>
      <p class="desc-text">지역 이름을 직접 검색해주세요.<br>예: 서울, 부산 해운대, 대전</p>
      <div class="search-row">
        <input type="text" id="search-input" placeholder="지역 이름 입력">
        <button class="primary-btn" id="btn-search" style="width:auto;">검색</button>
      </div>
      <div id="search-results"></div>
      <div class="status-text" id="search-status"></div>
    </div>

    <!-- 화면 4: 결과 -->
    <div class="screen" id="screen-result">
      <div class="weather-summary">
        <div class="w-emoji" id="result-emoji">☀️</div>
        <div class="w-temp" id="result-temp">-℃</div>
        <div class="w-label" id="result-label">-</div>
        <div class="w-sub" id="result-sub">-</div>
      </div>

      <div class="outfit-grid">
        <div class="outfit-card">
          <div class="oc-label">👚 상의</div>
          <div class="oc-value" id="oc-top">-</div>
        </div>
        <div class="outfit-card">
          <div class="oc-label">👖 하의</div>
          <div class="oc-value" id="oc-bottom">-</div>
        </div>
        <div class="outfit-card">
          <div class="oc-label">🧥 아우터</div>
          <div class="oc-value" id="oc-outer">-</div>
        </div>
        <div class="outfit-card">
          <div class="oc-label">👟 신발</div>
          <div class="oc-value" id="oc-shoes">-</div>
        </div>
      </div>

      <div class="umbrella-box" id="umbrella-box">
        <span id="umbrella-text">-</span>
      </div>

      <div class="tip-box">
        💡 <span id="result-tip">-</span>
      </div>

      <button class="secondary-btn" id="btn-reset">🔄 지역 다시 선택하기</button>
    </div>

  </div>
</div>

<script>
  // =====================================================
  // 화면 전환 관련 요소
  // =====================================================
  const screens = {
    start: document.getElementById('screen-start'),
    confirm: document.getElementById('screen-confirm'),
    search: document.getElementById('screen-search'),
    result: document.getElementById('screen-result'),
  };

  function showScreen(name){
    Object.values(screens).forEach(s => s.classList.remove('active'));
    screens[name].classList.add('active');
    window.scrollTo({ top: 0, behavior: 'smooth' });
  }

  // 현재 선택된 위치 정보를 담아둘 변수
  let currentLocation = null; // { name, sub, latitude, longitude }

  // =====================================================
  // 날씨 코드 → 한국어 라벨 / 이모지 매핑 (WMO 날씨코드 기준)
  // =====================================================
  const WEATHER_INFO = {
    0:  { label: '맑음', emoji: '☀️' },
    1:  { label: '대체로 맑음', emoji: '🌤️' },
    2:  { label: '구름 조금', emoji: '⛅' },
    3:  { label: '흐림', emoji: '☁️' },
    45: { label: '안개', emoji: '🌫️' },
    48: { label: '짙은 안개', emoji: '🌫️' },
    51: { label: '약한 이슬비', emoji: '🌦️' },
    53: { label: '이슬비', emoji: '🌦️' },
    55: { label: '강한 이슬비', emoji: '🌧️' },
    56: { label: '어는 이슬비', emoji: '🌧️' },
    57: { label: '강한 어는 이슬비', emoji: '🌧️' },
    61: { label: '약한 비', emoji: '🌧️' },
    63: { label: '비', emoji: '🌧️' },
    65: { label: '강한 비', emoji: '🌧️' },
    66: { label: '어는 비', emoji: '🌧️' },
    67: { label: '강한 어는 비', emoji: '🌧️' },
    71: { label: '약한 눈', emoji: '🌨️' },
    73: { label: '눈', emoji: '🌨️' },
    75: { label: '강한 눈', emoji: '❄️' },
    77: { label: '싸락눈', emoji: '🌨️' },
    80: { label: '약한 소나기', emoji: '🌦️' },
    81: { label: '소나기', emoji: '🌧️' },
    82: { label: '강한 소나기', emoji: '⛈️' },
    85: { label: '약한 눈 소나기', emoji: '🌨️' },
    86: { label: '강한 눈 소나기', emoji: '❄️' },
    95: { label: '뇌우', emoji: '⛈️' },
    96: { label: '우박 동반 뇌우', emoji: '⛈️' },
    99: { label: '강한 우박 동반 뇌우', emoji: '⛈️' },
  };

  function getWeatherInfo(code){
    return WEATHER_INFO[code] || { label: '알 수 없음', emoji: '🌡️' };
  }

  // =====================================================
  // 날씨 코드로 비/눈/뇌우/안개 여부 판단하는 함수들
  // =====================================================
  const RAIN_CODES = [51,53,55,56,57,61,63,65,66,67,80,81,82,95,96,99];
  const SNOW_CODES = [71,73,75,77,85,86];
  const FOG_CODES = [45,48];
  const THUNDER_CODES = [95,96,99];
  const CLEAR_CODES = [0,1];

  // =====================================================
  // 날씨 + 기온 + 바람에 따라 오늘의 코디를 만들어주는 함수
  // =====================================================
  function buildOutfit(tempC, code, windKmh){
    const isRain = RAIN_CODES.includes(code);
    const isSnow = SNOW_CODES.includes(code);
    const isFog = FOG_CODES.includes(code);
    const isThunder = THUNDER_CODES.includes(code);
    const isClear = CLEAR_CODES.includes(code);
    const strongWind = windKmh >= 40;   // 바람이 거센 날
    const typhoonLevel = windKmh >= 60; // 태풍급 강풍

    let top, bottom, outer, shoes;
    let umbrella = false;
    let umbrellaText = '오늘은 우산이 필요 없어요. 가볍게 나가도 좋아요!';
    let tips = [];

    // ---- 1단계: 기온에 따른 기본 코디 ----
    if (tempC >= 28){
      top = '민소매나 반팔 티셔츠';
      bottom = '반바지나 얇은 린넨 팬츠';
      outer = '아우터 없이 가볍게';
    } else if (tempC >= 23){
      top = '반팔 티셔츠나 얇은 셔츠';
      bottom = '면바지나 슬랙스';
      outer = '더울 수 있으니 얇은 셔츠 하나만 겹쳐 입기';
    } else if (tempC >= 17){
      // 화창하고 선선한 날씨의 기준 구간
      top = '얇은 긴팔 티셔츠나 반팔 위에 가벼운 셔츠';
      bottom = '면바지나 청바지';
      outer = '바람막이나 얇은 가디건 (덥지 않게 살짝만!)';
    } else if (tempC >= 9){
      top = '맨투맨이나 얇은 니트';
      bottom = '청바지나 두께감 있는 팬츠';
      outer = '자켓이나 후드집업';
    } else if (tempC >= 0){
      top = '기모 후드나 두꺼운 니트';
      bottom = '기모 바지나 두꺼운 청바지';
      outer = '코트나 가벼운 패딩';
    } else {
      top = '기모 이너 위에 두꺼운 니트';
      bottom = '기모 안감이 있는 두꺼운 바지';
      outer = '두꺼운 패딩이나 롱코트';
    }

    shoes = '캐주얼 운동화'; // 기본 신발

    // ---- 2단계: 날씨 상황별 보정 ----
    if (isRain && !isThunder){
      umbrella = true;
      umbrellaText = '비 소식이 있어요! 우산을 꼭 챙기세요.';
      outer += ' 위에 방수 자켓이나 우비를 겹치면 든든해요';
      shoes = '방수 운동화나 레인부츠 (천 소재 운동화는 젖기 쉬워요)';
      tips.push('비 오는 날엔 밝은 색보다 어두운 색 옷이 얼룩이 덜 티나요.');
    }

    if (isThunder){
      umbrella = true;
      umbrellaText = '천둥 번개를 동반한 비예요! 튼튼한 우산과 여벌 옷을 챙기면 안심이에요.';
      outer += ' 위에 방수 자켓은 필수예요';
      shoes = '방수 신발 (미끄러운 길 주의)';
      tips.push('갑자기 바람이 세질 수 있으니 장우산을 추천해요.');
    }

    if (isSnow){
      umbrella = true;
      umbrellaText = '눈이 내려요! 우산이나 방수 모자를 챙기면 좋아요.';
      outer = '방수 기능이 있는 두꺼운 패딩이나 코트';
      shoes = '방수·미끄럼 방지 부츠';
      tips.push('눈길은 미끄러우니 밑창이 두꺼운 신발을 신어주세요.');
    }

    if (strongWind){
      outer += ' (바람에 잘 안 날리는 핏으로 선택하세요)';
      tips.push('바람이 강해서 모자보다는 머리끈이나 후드가 더 편할 수 있어요.');
      if (typhoonLevel){
        tips.push('태풍급 바람이 예상돼요. 외출은 최소화하고, 우산 대신 우비를 추천해요!');
        umbrella = false;
        umbrellaText = '바람이 너무 강해서 우산이 뒤집힐 수 있어요. 우산 대신 우비를 챙기세요!';
      }
    }

    if (isFog){
      tips.push('안개로 시야가 낮아요. 밝은 색 옷이나 액세서리로 눈에 잘 띄게 입어보세요.');
    }

    if (isClear && tempC >= 17 && tempC <= 24 && !strongWind){
      tips.push('화창하고 선선한 날씨엔 얇은 아우터 하나로 산뜻하게 연출해보세요!');
    }

    if (tips.length === 0){
      tips.push('오늘 하루도 상쾌하고 좋은 하루 보내세요!');
    }

    return {
      top, bottom, outer, shoes,
      umbrella, umbrellaText,
      tip: tips.join(' '),
    };
  }

  // =====================================================
  // 화면 1: "내 위치로 날씨 확인하기" 버튼
  // =====================================================
  const btnStart = document.getElementById('btn-start');
  const startStatus = document.getElementById('start-status');
  const startError = document.getElementById('start-error');

  btnStart.addEventListener('click', () => {
    startError.style.display = 'none';
    startStatus.textContent = '📍 위치 정보를 확인하는 중이에요...';

    if (!navigator.geolocation){
      startError.style.display = 'block';
      startError.textContent = '이 브라우저는 위치 정보 기능을 지원하지 않아요. 아래에서 지역을 직접 검색해주세요.';
      startStatus.textContent = '';
      showScreen('search');
      return;
    }

    navigator.geolocation.getCurrentPosition(
      async (position) => {
        const lat = position.coords.latitude;
        const lon = position.coords.longitude;
        startStatus.textContent = '🗺️ 지역 이름을 확인하는 중이에요...';

        try {
          const locName = await reverseGeocode(lat, lon);
          currentLocation = {
            name: locName.main,
            sub: locName.sub,
            latitude: lat,
            longitude: lon,
          };
          document.getElementById('confirm-loc-name').textContent = currentLocation.name;
          document.getElementById('confirm-loc-sub').textContent = currentLocation.sub;
          startStatus.textContent = '';
          showScreen('confirm');
        } catch (err){
          startError.style.display = 'block';
          startError.textContent = '지역 이름을 불러오지 못했어요. 아래에서 지역을 직접 검색해주세요.';
          startStatus.textContent = '';
          showScreen('search');
        }
      },
      (error) => {
        startStatus.textContent = '';
        startError.style.display = 'block';
        startError.textContent = '위치 권한이 거부되었거나 오류가 발생했어요. 아래에서 지역을 직접 검색해주세요.';
        showScreen('search');
      },
      { timeout: 10000 }
    );
  });

  // 위도/경도를 지역 이름으로 바꿔주는 함수 (BigDataCloud 무료 API, 키 필요 없음)
  async function reverseGeocode(lat, lon){
    const url = `https://api.bigdatacloud.net/data/reverse-geocode-client?latitude=${lat}&longitude=${lon}&localityLanguage=ko`;
    const res = await fetch(url);
    if (!res.ok) throw new Error('reverse geocode failed');
    const data = await res.json();
    const main = data.city || data.locality || data.principalSubdivision || '알 수 없는 지역';
    const sub = [data.principalSubdivision, data.countryName].filter(Boolean).join(' · ');
    return { main, sub: sub || '위치 확인됨' };
  }

  // =====================================================
  // 화면 2: 위치 확인 (예 / 아니요)
  // =====================================================
  document.getElementById('btn-yes').addEventListener('click', () => {
    loadWeatherAndShowResult();
  });

  document.getElementById('btn-no').addEventListener('click', () => {
    showScreen('search');
  });

  // =====================================================
  // 화면 3: 지역 직접 검색
  // =====================================================
  const searchInput = document.getElementById('search-input');
  const searchResults = document.getElementById('search-results');
  const searchStatus = document.getElementById('search-status');
  const btnSearch = document.getElementById('btn-search');

  btnSearch.addEventListener('click', doSearch);
  searchInput.addEventListener('keydown', (e) => {
    if (e.key === 'Enter') doSearch();
  });

  async function doSearch(){
    const query = searchInput.value.trim();
    if (!query){
      searchStatus.textContent = '지역 이름을 입력해주세요.';
      return;
    }
    searchStatus.textContent = '🔍 검색 중이에요...';
    searchResults.innerHTML = '';

    try {
      // Open-Meteo 지오코딩 API (무료, 키 필요 없음)
      const url = `https://geocoding-api.open-meteo.com/v1/search?name=${encodeURIComponent(query)}&count=6&language=ko&format=json`;
      const res = await fetch(url);
      const data = await res.json();

      if (!data.results || data.results.length === 0){
        searchStatus.textContent = '검색 결과가 없어요. 다른 이름으로 시도해보세요.';
        return;
      }

      searchStatus.textContent = '';
      data.results.forEach(place => {
        const item = document.createElement('div');
        item.className = 'search-result-item';
        const subInfo = [place.admin1, place.country].filter(Boolean).join(' · ');
        item.innerHTML = `${place.name}<span>${subInfo}</span>`;
        item.addEventListener('click', () => {
          currentLocation = {
            name: place.name,
            sub: subInfo || '위치 선택됨',
            latitude: place.latitude,
            longitude: place.longitude,
          };
          loadWeatherAndShowResult();
        });
        searchResults.appendChild(item);
      });
    } catch (err){
      searchStatus.textContent = '검색 중 오류가 발생했어요. 인터넷 연결을 확인해주세요.';
    }
  }

  // =====================================================
  // 날씨 데이터를 불러와서 결과 화면을 채우는 함수
  // =====================================================
  async function loadWeatherAndShowResult(){
    if (!currentLocation) return;

    // 결과 화면으로 넘어가면서 로딩 표시
    showScreen('result');
    document.getElementById('result-label').textContent = '날씨를 불러오는 중이에요...';
    document.getElementById('result-temp').textContent = '';
    document.getElementById('result-emoji').textContent = '⏳';

    try {
      const { latitude, longitude } = currentLocation;
      // Open-Meteo 실시간 날씨 API (무료, 키 필요 없음)
      const url = `https://api.open-meteo.com/v1/forecast?latitude=${latitude}&longitude=${longitude}&current_weather=true&timezone=auto`;
      const res = await fetch(url);
      const data = await res.json();
      const current = data.current_weather;

      const tempC = current.temperature;
      const code = current.weathercode;
      const windKmh = current.windspeed;

      const info = getWeatherInfo(code);
      const outfit = buildOutfit(tempC, code, windKmh);

      // 결과 화면 채우기
      document.getElementById('result-emoji').textContent = info.emoji;
      document.getElementById('result-temp').textContent = `${Math.round(tempC)}℃`;
      document.getElementById('result-label').textContent = info.label;
      document.getElementById('result-sub').textContent =
        `${currentLocation.name} · 바람 ${Math.round(windKmh)}km/h`;

      document.getElementById('oc-top').textContent = outfit.top;
      document.getElementById('oc-bottom').textContent = outfit.bottom;
      document.getElementById('oc-outer').textContent = outfit.outer;
      document.getElementById('oc-shoes').textContent = outfit.shoes;

      const umbrellaBox = document.getElementById('umbrella-box');
      umbrellaBox.className = 'umbrella-box ' + (outfit.umbrella ? 'umbrella-yes' : 'umbrella-no');
      document.getElementById('umbrella-text').textContent =
        (outfit.umbrella ? '☔ ' : '🙂 ') + outfit.umbrellaText;

      document.getElementById('result-tip').textContent = outfit.tip;

    } catch (err){
      document.getElementById('result-label').textContent = '날씨를 불러오지 못했어요.';
      document.getElementById('result-sub').textContent = '인터넷 연결을 확인하고 다시 시도해주세요.';
      document.getElementById('result-emoji').textContent = '⚠️';
    }
  }

  // =====================================================
  // 결과 화면: "지역 다시 선택하기" 버튼
  // =====================================================
  document.getElementById('btn-reset').addEventListener('click', () => {
    currentLocation = null;
    searchInput.value = '';
    searchResults.innerHTML = '';
    searchStatus.textContent = '';
    startStatus.textContent = '';
    startError.style.display = 'none';
    showScreen('start');
  });
</script>
</body>
</html>
