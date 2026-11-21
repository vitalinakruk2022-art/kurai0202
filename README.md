<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>KURAI — Сайт</title>

<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;500;600&family=Nunito:wght@300;400;500;600&display=swap" rel="stylesheet">

<style>
  /* БАЗОВЫЕ НАСТРОЙКИ */
  * { box-sizing: border-box; margin: 0; padding: 0; }
  
  :root {
    --bg: #040a07; --panel: rgba(14, 26, 20, 0.65); --line: rgba(85, 230, 165, 0.15);
    --green: #55e6a5; --green-dim: #2c8c64; --text: #e8f5ee; --muted: #8fa89b;
    --radius-lg: 24px; --radius-sm: 16px;
  }

  /* Скрываем радио-кнопки */
  input[type="radio"] { display: none; }

  body {
    font-family: 'Nunito', sans-serif; font-weight: 400;
    background-color: var(--bg);
    background-image: radial-gradient(circle at 15% 0%, rgba(85, 230, 165, 0.08), transparent 40%), radial-gradient(circle at 85% 100%, rgba(85, 230, 165, 0.05), transparent 40%);
    background-attachment: fixed; color: var(--text); min-height: 100vh; line-height: 1.7; font-size: 15.5px;
    padding-bottom: 100px; /* Отступ, чтобы панель корзины не перекрывала контент */
  }

  /* ШАПКА */
  .site-header {
    position: sticky; top: 0; z-index: 50; display: flex; flex-wrap: wrap; gap: 20px; justify-content: space-between; align-items: center;
    padding: 20px 32px; background: rgba(4, 10, 7, 0.7); backdrop-filter: blur(16px); -webkit-backdrop-filter: blur(16px); border-bottom: 1px solid var(--line);
  }
  
  .logo {
    font-family: 'Montserrat', sans-serif; font-size: 1.3rem; font-weight: 600; letter-spacing: .6em; text-transform: uppercase;
    text-decoration: none; padding-left: .6em; cursor: pointer; background: linear-gradient(135deg, #ffffff, var(--green)); -webkit-background-clip: text; background-clip: text; color: transparent;
  }

  .nav { display: flex; flex-wrap: wrap; gap: 8px; }
  .nav label {
    font-family: 'Montserrat', sans-serif; font-size: 0.85rem; font-weight: 500; letter-spacing: .04em;
    color: var(--muted); padding: 10px 18px; border-radius: 50px; border: 1px solid transparent; transition: all 0.3s ease; cursor: pointer; display: inline-block;
  }
  .nav label:hover { color: #fff; background: rgba(85, 230, 165, 0.08); }

  main { max-width: 1000px; margin: 0 auto; padding: 60px 24px 20px; }
  
  .page { display: none; }
  @keyframes softFade { from { opacity: 0; transform: translateY(8px); } to { opacity: 1; transform: translateY(0); } }

  /* ПЕРЕКЛЮЧЕНИЕ ВКЛАДОК */
  #tab-main:checked ~ main #page-main { display: block; animation: softFade 0.4s ease; }
  #tab-main:checked ~ .site-header label[for="tab-main"] { color: #000; background: var(--green); box-shadow: 0 4px 15px rgba(85, 230, 165, 0.3); }

  #tab-genshin:checked ~ main #page-genshin { display: block; animation: softFade 0.4s ease; }
  #tab-genshin:checked ~ .site-header label[for="tab-genshin"] { color: #000; background: var(--green); box-shadow: 0 4px 15px rgba(85, 230, 165, 0.3); }

  #tab-ads:checked ~ main #page-ads { display: block; animation: softFade 0.4s ease; }
  #tab-ads:checked ~ .site-header label[for="tab-ads"] { color: #000; background: var(--green); box-shadow: 0 4px 15px rgba(85, 230, 165, 0.3); }

  /* ТИПОГРАФИКА */
  h1, h2, h3 { font-family: 'Montserrat', sans-serif; font-weight: 600; color: #fff; }
  .hero h1 { font-size: clamp(2.2rem, 5vw, 3.2rem); margin-bottom: 16px; line-height: 1.2; }
  .hero h1 span { color: var(--green); text-shadow: 0 0 20px rgba(85, 230, 165, 0.3); }
  .page-title { font-size: clamp(1.8rem, 4vw, 2.4rem); margin-bottom: 12px; }
  .page-sub { font-size: 1.05rem; color: var(--muted); margin-bottom: 40px; font-weight: 300; }

  /* КАРТОЧКИ НА ГЛАВНОЙ */
  .cards { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 20px; margin-top: 20px; }
  .card { display: block; text-decoration: none; background: var(--panel); border: 1px solid var(--line); border-radius: var(--radius-lg); padding: 32px 28px; cursor: pointer; transition: all 0.3s ease; backdrop-filter: blur(10px); }
  .card:hover { transform: translateY(-4px); border-color: rgba(85, 230, 165, 0.4); background: rgba(14, 26, 20, 0.8); }
  .card h3 { font-size: 1.2rem; margin-bottom: 12px; font-weight: 500; color: var(--green); }

  /* СЕКЦИИ ПРАЙСА */
  .section { background: var(--panel); border: 1px solid var(--line); border-radius: var(--radius-lg); padding: 28px; margin-bottom: 24px; backdrop-filter: blur(10px); }
  .section h2 { font-size: 1.25rem; margin-bottom: 16px; font-weight: 500; }
  .section h2 .num { color: var(--green); margin-right: 12px; }
  .service { margin-top: 20px; padding-top: 20px; border-top: 1px dashed rgba(85, 230, 165, 0.15); }
  .service:first-of-type { border-top: none; margin-top: 0; padding-top: 0; }
  .service-title { font-size: 0.95rem; color: #c9ded4; margin-bottom: 12px; font-weight: 500; }

  /* СТРОКИ С ЦЕНАМИ */
  .price-list { display: grid; gap: 10px; }
  .price-row { 
    display: flex; justify-content: space-between; align-items: center; gap: 16px; flex-wrap: wrap; 
    padding: 14px 20px; border-radius: var(--radius-sm); background: rgba(85, 230, 165, 0.03); border: 1px solid rgba(85, 230, 165, 0.08); transition: background 0.2s ease;
  }
  .price-row:hover { background: rgba(85, 230, 165, 0.08); }
  .name { font-weight: 400; max-width: 60ch; font-size: 0.95rem; }
  
  .price { display: flex; align-items: center; gap: 10px; flex-wrap: wrap; }
  .stars, .rub { font-family: 'Montserrat', sans-serif; font-size: 0.8rem; padding: 5px 14px; border-radius: 50px; white-space: nowrap; }
  .stars { background: rgba(85, 230, 165, 0.15); color: #9af0c6; }
  .rub { background: rgba(255, 255, 255, 0.05); color: #d1e0d7; }

  /* КНОПКА ДОБАВИТЬ */
  .add-btn {
    background: transparent; border: 1px solid var(--green); color: var(--green);
    padding: 5px 14px; border-radius: 50px; font-family: 'Nunito', sans-serif; font-weight: 700;
    cursor: pointer; transition: all 0.2s; font-size: 1rem; line-height: 1;
    display: flex; align-items: center; justify-content: center; min-width: 32px; height: 32px;
  }
  .add-btn:hover { background: var(--green); color: #000; transform: scale(1.1); }
  .add-btn.added { background: var(--green); color: #000; pointer-events: none; opacity: 0.7; }

  .note { margin-top: 20px; padding: 16px 20px; border-left: 2px solid var(--green); background: linear-gradient(90deg, rgba(85, 230, 165, 0.06), transparent); border-radius: 0 var(--radius-sm) var(--radius-sm) 0; color: var(--muted); font-size: 0.9rem; font-weight: 300; }

  /* ПОДВАЛ */
  .site-footer { border-top: 1px solid var(--line); padding: 30px 24px; text-align: center; color: var(--muted); font-size: 0.9rem; font-family: 'Montserrat', sans-serif; background: rgba(4, 10, 7, 0.5); margin-bottom: 80px; /* отступ для корзины */ }
  .site-footer a { color: var(--green); text-decoration: none; }

  /* ПАНЕЛЬ КОРЗИНЫ ВНИЗУ */
  .cart-bar {
    position: fixed; bottom: 0; left: 0; right: 0; z-index: 100;
    background: rgba(10, 20, 15, 0.95); backdrop-filter: blur(20px);
    border-top: 1px solid var(--green); padding: 16px 24px;
    display: flex; justify-content: space-between; align-items: center; gap: 16px;
    transform: translateY(100%); transition: transform 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
    box-shadow: 0 -10px 30px rgba(0,0,0,0.5);
  }
  .cart-bar.active { transform: translateY(0); }
  .cart-info { font-family: 'Montserrat', sans-serif; font-size: 0.95rem; color: var(--text); }
  .cart-info span { color: var(--green); font-weight: 600; font-size: 1.1rem; }
  
  .checkout-btn {
    background: var(--green); color: #000; border: none; padding: 12px 28px;
    border-radius: 50px; font-family: 'Montserrat', sans-serif; font-weight: 600;
    cursor: pointer; transition: 0.2s; font-size: 0.95rem;
  }
  .checkout-btn:hover { background: #fff; transform: scale(1.02); box-shadow: 0 0 15px rgba(85, 230, 165, 0.4); }

  /* МОДАЛЬНОЕ ОКНО ОФОРМЛЕНИЯ */
  .modal-overlay {
    position: fixed; inset: 0; background: rgba(0,0,0,0.85); backdrop-filter: blur(5px);
    z-index: 200; display: none; align-items: center; justify-content: center; padding: 20px;
  }
  .modal-overlay.active { display: flex; animation: softFade 0.3s ease; }
  .modal-content {
    background: var(--panel); border: 1px solid var(--green); border-radius: var(--radius-lg);
    padding: 32px; width: 100%; max-width: 450px; text-align: center;
    box-shadow: 0 20px 50px rgba(0,0,0,0.8);
  }
  .modal-content h2 { margin-bottom: 10px; color: var(--green); }
  .modal-content p { color: var(--muted); font-size: 0.9rem; margin-bottom: 20px; }
  .modal-content input {
    width: 100%; padding: 14px 16px; border-radius: var(--radius-sm);
    background: rgba(0,0,0,0.4); border: 1px solid var(--line); color: #fff;
    font-family: 'Nunito', sans-serif; font-size: 1rem; margin-bottom: 20px; outline: none; transition: border 0.3s;
  }
  .modal-content input:focus { border-color: var(--green); box-shadow: 0 0 10px rgba(85, 230, 165, 0.2); }
  
  .modal-actions { display: flex; gap: 12px; }
  .btn-cancel { flex: 1; background: transparent; border: 1px solid var(--muted); color: var(--muted); padding: 14px; border-radius: 50px; cursor: pointer; font-family: 'Montserrat'; font-weight: 500; transition: 0.2s; }
  .btn-cancel:hover { border-color: #fff; color: #fff; }
  .btn-submit { flex: 2; background: var(--green); border: none; color: #000; padding: 14px; border-radius: 50px; font-family: 'Montserrat'; font-weight: 600; cursor: pointer; transition: 0.2s; }
  .btn-submit:hover { background: #fff; }

  @media (max-width: 640px) {
    .site-header { padding: 16px; justify-content: center; }
    .logo { width: 100%; text-align: center; margin-bottom: 8px; }
    main { padding: 32px 16px 20px; }
    .price-row { flex-direction: column; align-items: flex-start; gap: 10px; padding: 16px; }
    .price { width: 100%; justify-content: space-between; }
    .cart-bar { flex-direction: column; gap: 12px; text-align: center; padding: 16px; }
    .checkout-btn { width: 100%; }
  }
</style>
</head>
<body>

<!-- УПРАВЛЯЮЩИЕ РАДИОКНОПКИ -->
<input type="radio" name="tabs" id="tab-main" checked>
<input type="radio" name="tabs" id="tab-genshin">
<input type="radio" name="tabs" id="tab-ads">

<header class="site-header">
  <label for="tab-main" class="logo">KURAI</label>
  <nav class="nav">
    <label for="tab-main">Главная</label>
    <label for="tab-genshin">Genshin</label>
    <label for="tab-ads">Реклама</label>
  </nav>
</header>

<main>
  <!-- ГЛАВНАЯ СТРАНИЦА -->
  <div id="page-main" class="page">
    <section class="hero">
      <h1>Добро пожаловать в <span>KURAI</span></h1>
      <p class="page-sub">Услуги по Genshin Impact, контент канала и реклама — всё в одном месте.</p>
    </section>
    <div class="cards">
      <label for="tab-genshin" class="card">
        <h3>Genshin Impact</h3>
        <p>Полный прайс-лист на зачистку, квесты, прокачку персонажей, присмотр за аккаунтом и ивенты.</p>
      </label>
      <label for="tab-ads" class="card">
        <h3>Реклама и ВП</h3>
        <p>Актуальные цены на рекламу канала и взаимный пиар с перекрытием.</p>
      </label>
    </div>
  </div>

  <!-- СТРАНИЦА GENSHIN -->
  <div id="page-genshin" class="page">
    <h1 class="page-title">Прайс-лист</h1>
    <p class="page-sub">Нажмите на «+» напротив нужной услуги, чтобы добавить её в заказ.</p>
    
    <section class="section">
      <h2><span class="num">1.</span> Зачистка фулл</h2>
      <p class="service-title">Все загадки, сундуки и т.д. — не смотря на то, что уже есть 100% на карте</p>
      
      <div class="service">
        <p class="service-title">1.1 Фулл зачистка региона (интерактивная карта от HoYo)</p>
        <div class="price-list">
          <div class="price-row"><span class="name">от 0–20%</span><span class="price"><span class="stars">300 зв.</span><span class="rub">420 ₽</span><button class="add-btn" data-name="Фулл зачистка региона (0-20%)" data-price="300 зв. / 420 ₽">+</button></span></div>
          <div class="price-row"><span class="name">от 20–50%</span><span class="price"><span class="stars">250 зв.</span><span class="rub">350 ₽</span><button class="add-btn" data-name="Фулл зачистка региона (20-50%)" data-price="250 зв. / 350 ₽">+</button></span></div>
          <div class="price-row"><span class="name">от 50–80%</span><span class="price"><span class="stars">225 зв.</span><span class="rub">315 ₽</span><button class="add-btn" data-name="Фулл зачистка региона (50-80%)" data-price="225 зв. / 315 ₽">+</button></span></div>
          <div class="price-row"><span class="name">от 80–100%</span><span class="price"><span class="stars">200 зв.</span><span class="rub">280 ₽</span><button class="add-btn" data-name="Фулл зачистка региона (80-100%)" data-price="200 зв. / 280 ₽">+</button></span></div>
        </div>
        <p class="note">P.S. Относится к регионам: Монштат, Ли Юэ, Инадзума, Сумеру, Натлан, Нод-Край и Снежная. А также к доп. локациям: Разлом: Подземные шахты, Энканомия, Море Древности, Священная Гора, Храм пространства, Морозная Луна.</p>
      </div>

      <div class="service">
        <p class="service-title">1.2 Фулл зачистка локации (интерактивная карта от HoYo)</p>
        <div class="price-list">
          <div class="price-row"><span class="name">от 0–20%</span><span class="price"><span class="stars">100 зв.</span><span class="rub">140 ₽</span><button class="add-btn" data-name="Фулл зачистка локации (0-20%)" data-price="100 зв. / 140 ₽">+</button></span></div>
          <div class="price-row"><span class="name">от 20–50%</span><span class="price"><span class="stars">75 зв.</span><span class="rub">105 ₽</span><button class="add-btn" data-name="Фулл зачистка локации (20-50%)" data-price="75 зв. / 105 ₽">+</button></span></div>
          <div class="price-row"><span class="name">от 50–80%</span><span class="price"><span class="stars">50 зв.</span><span class="rub">70 ₽</span><button class="add-btn" data-name="Фулл зачистка локации (50-80%)" data-price="50 зв. / 70 ₽">+</button></span></div>
          <div class="price-row"><span class="name">от 80–100%</span><span class="price"><span class="stars">25 зв.</span><span class="rub">35 ₽</span><button class="add-btn" data-name="Фулл зачистка локации (80-100%)" data-price="25 зв. / 35 ₽">+</button></span></div>
        </div>
      </div>
    </section>

    <section class="section">
      <h2><span class="num">2.</span> Зачистка до 100%</h2>
      <p class="service-title">Не смотря на то, что остались сундуки ещё</p>

      <div class="service">
        <p class="service-title">2.1 Зачистка до 100% региона (карта от HoYo + компас)</p>
        <div class="price-list">
          <div class="price-row"><span class="name">от 0–20%</span><span class="price"><span class="stars">200 зв.</span><span class="rub">280 ₽</span><button class="add-btn" data-name="Зачистка до 100% региона (0-20%)" data-price="200 зв. / 280 ₽">+</button></span></div>
          <div class="price-row"><span class="name">от 20–50%</span><span class="price"><span class="stars">175 зв.</span><span class="rub">240 ₽</span><button class="add-btn" data-name="Зачистка до 100% региона (20-50%)" data-price="175 зв. / 240 ₽">+</button></span></div>
          <div class="price-row"><span class="name">от 50–80%</span><span class="price"><span class="stars">150 зв.</span><span class="rub">210 ₽</span><button class="add-btn" data-name="Зачистка до 100% региона (50-80%)" data-price="150 зв. / 210 ₽">+</button></span></div>
          <div class="price-row"><span class="name">от 80–100%</span><span class="price"><span class="stars">125 зв.</span><span class="rub">175 ₽</span><button class="add-btn" data-name="Зачистка до 100% региона (80-100%)" data-price="125 зв. / 175 ₽">+</button></span></div>
        </div>
      </div>

      <div class="service">
        <p class="service-title">2.2 Зачистка до 100% локации (карта от HoYo + компас)</p>
        <div class="price-list">
          <div class="price-row"><span class="name">от 0–20%</span><span class="price"><span class="stars">75 зв.</span><span class="rub">105 ₽</span><button class="add-btn" data-name="Зачистка до 100% локации (0-20%)" data-price="75 зв. / 105 ₽">+</button></span></div>
          <div class="price-row"><span class="name">от 20–50%</span><span class="price"><span class="stars">50 зв.</span><span class="rub">70 ₽</span><button class="add-btn" data-name="Зачистка до 100% локации (20-50%)" data-price="50 зв. / 70 ₽">+</button></span></div>
          <div class="price-row"><span class="name">от 50–80%</span><span class="price"><span class="stars">25 зв.</span><span class="rub">35 ₽</span><button class="add-btn" data-name="Зачистка до 100% локации (50-80%)" data-price="25 зв. / 35 ₽">+</button></span></div>
          <div class="price-row"><span class="name">от 80–100%</span><span class="price"><span class="stars">15 зв.</span><span class="rub">21 ₽</span><button class="add-btn" data-name="Зачистка до 100% локации (80-100%)" data-price="15 зв. / 21 ₽">+</button></span></div>
        </div>
      </div>
    </section>

    <section class="section">
      <h2><span class="num">3.</span> Квесты и сюжет</h2>
      <div class="price-list">
        <div class="price-row"><span class="name">Любые квесты с самого их начала</span><span class="price"><span class="stars">50 зв.</span><span class="rub">70 ₽</span><button class="add-btn" data-name="Квесты с самого начала" data-price="50 зв. / 70 ₽">+</button></span></div>
        <div class="price-row"><span class="name">Квесты не с самого начала (например, аранары)</span><span class="price"><span class="stars">75 зв.</span><span class="rub">105 ₽</span><button class="add-btn" data-name="Квесты не с начала" data-price="75 зв. / 105 ₽">+</button></span></div>
        <div class="price-row"><span class="name">Сюжет, 1 глава</span><span class="price"><span class="stars">50 зв.</span><span class="rub">70 ₽</span><button class="add-btn" data-name="Сюжет 1 глава" data-price="50 зв. / 70 ₽">+</button></span></div>
        <div class="price-row"><span class="name">Сюжет, 1 регион (≈10 глав)</span><span class="price"><span class="stars">500 зв.</span><span class="rub">700 ₽</span><button class="add-btn" data-name="Сюжет 1 регион (10 глав)" data-price="500 зв. / 700 ₽">+</button></span></div>
        <div class="price-row"><span class="name">Отдельные / побочные задания</span><span class="price"><span class="stars">25 зв.</span><span class="rub">35 ₽</span><button class="add-btn" data-name="Отдельные / побочные задания" data-price="25 зв. / 35 ₽">+</button></span></div>
        <div class="price-row"><span class="name">Задания легенд / встречи</span><span class="price"><span class="stars">75 зв.</span><span class="rub">105 ₽</span><button class="add-btn" data-name="Задания легенд / встречи" data-price="75 зв. / 105 ₽">+</button></span></div>
        <div class="price-row"><span class="name">1 задание репутации Натлана</span><span class="price"><span class="stars">100 зв.</span><span class="rub">140 ₽</span><button class="add-btn" data-name="1 задание репутации Натлана" data-price="100 зв. / 140 ₽">+</button></span></div>
        <div class="price-row"><span class="name">1 задание репутации других регионов (кроме квестов)</span><span class="price"><span class="stars">25 зв.</span><span class="rub">35 ₽</span><button class="add-btn" data-name="1 задание репутации других регионов" data-price="25 зв. / 35 ₽">+</button></span></div>
      </div>
    </section>

    <section class="section">
      <h2><span class="num">4.</span> Прокачка персонажей</h2>
      <div class="price-list">
        <div class="price-row"><span class="name">Полная сборка 1 персонажа</span><span 
                <div class="price-row"><span 