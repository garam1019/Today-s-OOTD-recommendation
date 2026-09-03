<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>오늘의 OOTD (오프라인)</title>
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

  .big-emoji{ font-size: 60px; margin-bottom: 8px; }

  .desc-text{ font-size: 17px; color: var(--brown); line-height: 1.6; margin: 10px 0 24px; }

  .field-label{
    text-align: left;
    font-size: 15px;
    font-weight: 800;
    color: var(--brown-dark);
    margin: 0 0 10px;
  }

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
  .primary-btn:disabled{ opacity: 0.5; cursor: not-allowed; transform: none; }

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

  .status-text{ font-size: 14px; color: var(--brown); margin-top: 10px; min-height: 18px; }

  /* 지역 입력 화면 */
  .region-input{
    width: 100%;
    padding: 16px 18px;
    border-radius: 16px;
    border: 2px solid var(--yellow-deep);
    font-size: 18px;
    font-family: inherit;
    background: var(--cream);
    color: var(--brown-dark);
    text-align: center;
    margin-bottom: 18px;
  }
  .region-input:focus{ outline: none; border-color: var(--coral); }

  /* 위치 확인 화면 */
  .location-card{
    background: linear-gradient(160deg, var(--sky), var(--sky-deep));
    color: var(--white);
    border-radius: 20px;
    padding: 24px 18px;
    margin-bottom: 22px;
  }
  .location-card .loc-name{ font-size: 26px; font-weight: 900; margin: 4px 0; }
  .location-card .loc-sub{ font-size: 14px; opacity: 0.95; }

  .yes-no-row{ display: flex; gap: 10px; }
  .yes-no-row button{ flex: 1; }
  .no-btn{
    background: var(--white);
    color: var(--brown-dark);
    border: 2px solid #D8C7A8;
  }
  .no-btn:hover{ background: var(--cream); }

  /* 날씨 입력 화면 */
  .weather-form{ text-align: left; }

  .cond-grid{
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 8px;
    margin-bottom: 22px;
  }
  .cond-btn{
    background: var(--cream);
    border: 2px solid var(--cream-deep);
    border-radius: 14px;
    padding: 12px 4px;
    font-size: 13px;
    font-weight: 700;
    color: var(--brown-dark);
    cursor: pointer;
    font-family: inherit;
    transition: border 0.15s ease, background 0.15s ease, transform 0.15s ease;
  }
  .cond-btn .cb-emoji{ font-size: 26px; display: block; margin-bottom: 4px; }
  .cond-btn:hover{ transform: translateY(-2px); }
  .cond-btn.selected{
    background: var(--yellow);
    border-color: var(--yellow-deep);
  }

  .wind-row{ display: flex; gap: 8px; margin-bottom: 22px; }
  .wind-btn{
    flex: 1;
    background: var(--cream);
    border: 2px solid var(--cream-deep);
    border-radius: 14px;
    padding: 12px 6px;
    font-size: 13px;
    font-weight: 700;
    color: var(--brown-dark);
    cursor: pointer;
    font-family: inherit;
    transition: border 0.15s ease, background 0.15s ease, transform 0.15s ease;
  }
  .wind-btn .wb-emoji{ font-size: 22px; display: block; margin-bottom: 4px; }
  .wind-btn:hover{ transform: translateY(-2px); }
  .wind-btn.selected{ background: var(--sky); border-color: var(--sky-deep); }

  .temp-row{
    display: flex;
    align-items: center;
    gap: 10px;
    margin-bottom: 24px;
  }
  .temp-btn-round{
    width: 44px; height: 44px;
    border-radius: 50%;
    border: 2px solid var(--yellow-deep);
    background: var(--cream);
    font-size: 22px;
    font-weight: 800;
    color: var(--brown-dark);
    cursor: pointer;
    flex-shrink: 0;
  }
  .temp-btn-round:hover{ background: var(--yellow); }
  .temp-display{
    flex: 1;
    text-align: center;
    font-size: 30px;
    font-weight: 900;
    background: var(--cream);
    border-radius: 14px;
    padding: 10px;
  }

  /* 결과 화면 */
  .weather-summary{
    background: linear-gradient(160deg, var(--yellow), var(--yellow-deep));
    border-radius: 22px;
    padding: 26px 18px;
    margin-bottom: 22px;
  }
  .weather-summary .w-emoji{ font-size: 60px; }
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

  .offline-note{
    font-size: 12px;
    color: var(--brown);
    opacity: 0.75;
    margin-top: 18px;
  }

  @media (max-width: 420px){
    h1{ font-size: 26px; }
    .outfit-grid{ grid-template-columns: 1fr; }
    .cond-grid{ grid-template-columns: repeat(4, 1fr); }
  }
</style>
</head>
<body>
<div class="wrap">

  <header>
    <span class="badge">오프라인 · 인터넷 연결 불필요</span>
    <h1>👕 날씨 기반 OOTD</h1>
    <p>지금 날씨를 직접 골라 입력하면<br>바로 그 자리에서 코디를 추천해드려요.</p>
  </header>

  <div class="panel">

    <!-- 화면 1: 지역 입력 -->
    <div class="screen active" id="screen-region">
      <div class="big-emoji">📍</div>
      <p class="desc-text">지금 계신 지역 이름을 입력해주세요.</p>
      <input type="text" class="region-input" id="region-input" placeholder="예: 서울시 강남구">
      <button class="primary-btn" id="btn-region-next">다음</button>
      <div class="status-text" id="region-status"></div>
    </div>

    <!-- 화면 2: 위치 확인 -->
    <div class="screen" id="screen-confirm">
      <div class="location-card">
        <div style="font-size:14px; opacity:0.9;">입력하신 위치</div>
        <div class="loc-name" id="confirm-loc-name">-</div>
        <div class="loc-sub">이 위치가 맞나요?</div>
      </div>
      <div class="yes-no-row">
        <button class="primary-btn" id="btn-yes">예, 맞아요</button>
        <button class="secondary-btn no-btn" id="btn-no">아니요, 다시 입력할게요</button>
      </div>
    </div>

    <!-- 화면 3: 날씨 직접 입력 -->
    <div class="screen" id="screen-weather-input">
      <div class="weather-form">
        <p class="field-label">☁️ 지금 하늘 상태는 어떤가요?</p>
        <div class="cond-grid" id="cond-grid"></div>

        <p class="field-label">💨 바람은 어느 정도인가요?</p>
        <div class="wind-row" id="wind-row"></div>

        <p class="field-label">🌡️ 현재 기온은 몇 도인가요?</p>
        <div class="temp-row">
          <button class="temp-btn-round" id="temp-minus">−</button>
          <div class="temp-display"><span id="temp-value">18</span>℃</div>
          <button class="temp-btn-round" id="temp-plus">+</button>
        </div>
      </div>
      <button class="primary-btn" id="btn-get-outfit" disabled>이 날씨로 코디 추천받기</button>
      <div class="status-text" id="weather-input-status">하늘 상태와 바람을 먼저 골라주세요.</div>
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

      <button class="secondary-btn" id="btn-back-weather">🌤️ 날씨 다시 입력하기</button>
      <button class="secondary-btn" id="btn-reset">🔄 지역 다시 선택하기</button>
    </div>

    <p class="offline-note">※ 인터넷 연결 없이 완전히 오프라인으로 작동해요. 날씨 정보는 직접 입력한 값을 기준으로 추천돼요.</p>

  </div>
</div>

<script>
  // =====================================================
  // 화면 전환 관련 요소
  // =====================================================
  const screens = {
    region: document.getElementById('screen-region'),
    confirm: document.getElementById('screen-confirm'),
    weatherInput: document.getElementById('screen-weather-input'),
    result: document.getElementById('screen-result'),
  };

  function showScreen(name){
    Object.values(screens).forEach(s => s.classList.remove('active'));
    screens[name].classList.add('active');
    window.scrollTo({ top: 0, behavior: 'smooth' });
  }

  // 사용자가 입력/선택한 정보를 담아둘 변수들
  let regionName = '';
  let selectedCondition = null; // { key, label, emoji, code }
  let selectedWind = null;      // { key, label, emoji, kmh }
  let currentTemp = 18;

  // =====================================================
  // 날씨 상태 목록 (직접 선택하는 8가지) — 코드값은 기존 옷차림 로직과 연결
  // =====================================================
  const CONDITIONS = [
    { key: 'clear',   label: '맑음',     emoji: '☀️', code: 0  },
    { key: 'cloudy2',  label: '구름많음', emoji: '⛅', code: 2  },
    { key: 'overcast', label: '흐림',     emoji: '☁️', code: 3  },
    { key: 'fog',      label: '안개',     emoji: '🌫️', code: 45 },
    { key: 'rain',     label: '비',       emoji: '🌧️', code: 63 },
    { key: 'shower',   label: '소나기',   emoji: '🌦️', code: 81 },
    { key: 'thunder',  label: '뇌우',     emoji: '⛈️', code: 95 },
    { key: 'snow',     label: '눈',       emoji: '❄️', code: 73 },
  ];

  // 바람 세기 3단계 (기존 로직의 강풍 40km/h, 태풍급 60km/h 기준과 연결)
  const WINDS = [
    { key: 'calm',     label: '잔잔함',   emoji: '🍃', kmh: 10 },
    { key: 'strong',   label: '바람 강함', emoji: '💨', kmh: 45 },
    { key: 'typhoon',  label: '태풍급',   emoji: '🌀', kmh: 65 },
  ];

  // =====================================================
  // 날씨 코드로 비/눈/뇌우/안개/맑음 여부 판단
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
  // 화면 1: 지역 입력
  // =====================================================
  const regionInput = document.getElementById('region-input');
  const regionStatus = document.getElementById('region-status');

  document.getElementById('btn-region-next').addEventListener('click', () => {
    const value = regionInput.value.trim();
    if (!value){
      regionStatus.textContent = '지역 이름을 입력해주세요.';
      return;
    }
    regionName = value;
    regionStatus.textContent = '';
    document.getElementById('confirm-loc-name').textContent = regionName;
    showScreen('confirm');
  });

  regionInput.addEventListener('keydown', (e) => {
    if (e.key === 'Enter') document.getElementById('btn-region-next').click();
  });

  // =====================================================
  // 화면 2: 위치 확인 (예 / 아니요)
  // =====================================================
  document.getElementById('btn-yes').addEventListener('click', () => {
    showScreen('weatherInput');
  });

  document.getElementById('btn-no').addEventListener('click', () => {
    regionInput.value = '';
    regionInput.focus();
    showScreen('region');
  });

  // =====================================================
  // 화면 3: 날씨 직접 입력
  // =====================================================
  const condGrid = document.getElementById('cond-grid');
  const windRow = document.getElementById('wind-row');
  const btnGetOutfit = document.getElementById('btn-get-outfit');
  const weatherInputStatus = document.getElementById('weather-input-status');

  // 하늘 상태 버튼 생성
  CONDITIONS.forEach(cond => {
    const btn = document.createElement('button');
    btn.className = 'cond-btn';
    btn.innerHTML = `<span class="cb-emoji">${cond.emoji}</span>${cond.label}`;
    btn.addEventListener('click', () => {
      selectedCondition = cond;
      document.querySelectorAll('.cond-btn').forEach(b => b.classList.remove('selected'));
      btn.classList.add('selected');
      checkWeatherFormReady();
    });
    condGrid.appendChild(btn);
  });

  // 바람 세기 버튼 생성
  WINDS.forEach(wind => {
    const btn = document.createElement('button');
    btn.className = 'wind-btn';
    btn.innerHTML = `<span class="wb-emoji">${wind.emoji}</span>${wind.label}`;
    btn.addEventListener('click', () => {
      selectedWind = wind;
      document.querySelectorAll('.wind-btn').forEach(b => b.classList.remove('selected'));
      btn.classList.add('selected');
      checkWeatherFormReady();
    });
    windRow.appendChild(btn);
  });

  function checkWeatherFormReady(){
    if (selectedCondition && selectedWind){
      btnGetOutfit.disabled = false;
      weatherInputStatus.textContent = '';
    } else {
      btnGetOutfit.disabled = true;
      weatherInputStatus.textContent = '하늘 상태와 바람을 먼저 골라주세요.';
    }
  }

  // 기온 +/- 버튼
  const tempValueEl = document.getElementById('temp-value');
  document.getElementById('temp-minus').addEventListener('click', () => {
    currentTemp = Math.max(-20, currentTemp - 1);
    tempValueEl.textContent = currentTemp;
  });
  document.getElementById('temp-plus').addEventListener('click', () => {
    currentTemp = Math.min(45, currentTemp + 1);
    tempValueEl.textContent = currentTemp;
  });

  btnGetOutfit.addEventListener('click', () => {
    if (!selectedCondition || !selectedWind) return;
    showResult();
  });

  // =====================================================
  // 화면 4: 결과 표시 (완전히 오프라인 계산, 네트워크 요청 없음)
  // =====================================================
  function showResult(){
    const outfit = buildOutfit(currentTemp, selectedCondition.code, selectedWind.kmh);

    document.getElementById('result-emoji').textContent = selectedCondition.emoji;
    document.getElementById('result-temp').textContent = `${currentTemp}℃`;
    document.getElementById('result-label').textContent = selectedCondition.label;
    document.getElementById('result-sub').textContent =
      `${regionName} · 바람 ${selectedWind.label}`;

    document.getElementById('oc-top').textContent = outfit.top;
    document.getElementById('oc-bottom').textContent = outfit.bottom;
    document.getElementById('oc-outer').textContent = outfit.outer;
    document.getElementById('oc-shoes').textContent = outfit.shoes;

    const umbrellaBox = document.getElementById('umbrella-box');
    umbrellaBox.className = 'umbrella-box ' + (outfit.umbrella ? 'umbrella-yes' : 'umbrella-no');
    document.getElementById('umbrella-text').textContent =
      (outfit.umbrella ? '☔ ' : '🙂 ') + outfit.umbrellaText;

    document.getElementById('result-tip').textContent = outfit.tip;

    showScreen('result');
  }

  // =====================================================
  // 결과 화면 버튼들
  // =====================================================
  document.getElementById('btn-back-weather').addEventListener('click', () => {
    showScreen('weatherInput');
  });

  document.getElementById('btn-reset').addEventListener('click', () => {
    regionName = '';
    selectedCondition = null;
    selectedWind = null;
    currentTemp = 18;
    tempValueEl.textContent = currentTemp;
    document.querySelectorAll('.cond-btn').forEach(b => b.classList.remove('selected'));
    document.querySelectorAll('.wind-btn').forEach(b => b.classList.remove('selected'));
    checkWeatherFormReady();
    regionInput.value = '';
    regionStatus.textContent = '';
    showScreen('region');
  });
</script>
</body>
</html>
