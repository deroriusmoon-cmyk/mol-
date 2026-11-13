<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>濃度をイメージしよう</title>

<style>
  :root {
    --ink: #17324a;
    --blue: #17669f;
    --blue-dark: #124d7d;
    --border: #c6dce9;
    --background: #edf5fa;
    --green: #157143;
    --red: #a52d35;
  }

  * {
    box-sizing: border-box;
  }

  body {
    margin: 0;
    color: var(--ink);
    background: var(--background);
    font-family:
      "Hiragino Kaku Gothic ProN",
      "Yu Gothic",
      "Meiryo",
      sans-serif;
    font-size: 17px;
    font-weight: 700;
    line-height: 1.45;
  }

  button,
  input,
  select {
    font: inherit;
  }

  button {
    cursor: pointer;
  }

  button:focus-visible,
  input:focus-visible,
  select:focus-visible,
  summary:focus-visible {
    outline: 3px solid #ed9d28;
    outline-offset: 3px;
  }

  header {
    color: white;
    background: linear-gradient(115deg, #145789, #258da2);
  }

  .header-inner {
    max-width: 1300px;
    margin: auto;
    padding: 10px 20px;
  }

  h1 {
    margin: 0;
    font-size: clamp(1.3rem, 2.5vw, 1.8rem);
    font-weight: 900;
  }

  header p {
    margin: 0;
    font-size: 0.9rem;
    font-weight: 700;
  }

  main {
    width: min(1300px, calc(100% - 28px));
    margin: 12px auto 24px;
  }

  h2,
  h3,
  p {
    margin-top: 0;
  }

  h2 {
    margin-bottom: 8px;
    color: var(--blue-dark);
    font-size: clamp(1.25rem, 2.3vw, 1.65rem);
    font-weight: 900;
  }

  h3 {
    font-weight: 900;
  }

  .screen {
    display: none;
  }

  .screen.active {
    display: block;
  }

  .card {
    background: white;
    border: 1px solid var(--border);
    border-radius: 14px;
    box-shadow: 0 4px 14px rgba(25, 70, 100, 0.06);
  }

  .back-button,
  .primary-button,
  .secondary-button {
    min-height: 42px;
    padding: 8px 16px;
    border-radius: 9px;
    font-weight: 900;
  }

  .back-button,
  .secondary-button {
    color: var(--blue-dark);
    background: white;
    border: 2px solid var(--blue);
  }

  .back-button {
    margin-bottom: 8px;
  }

  .primary-button {
    color: white;
    background: var(--blue);
    border: 2px solid var(--blue);
  }

  .primary-button:hover {
    background: var(--blue-dark);
  }

  /* =========================
     メニュー画面
  ========================= */

  .menu-intro {
    padding: 24px;
    text-align: center;
  }

  .menu-intro p {
    margin-bottom: 0;
    font-size: 1.1rem;
  }

  .menu-grid {
    display: grid;
    grid-template-columns: repeat(2, minmax(0, 1fr));
    gap: 18px;
    max-width: 900px;
    margin: 18px auto 0;
  }

  .menu-card {
    min-height: 220px;
    padding: 24px;
    text-align: left;
    color: var(--ink);
    background: white;
    border: 2px solid var(--border);
    border-radius: 15px;
    box-shadow: 0 4px 14px rgba(25, 70, 100, 0.06);
  }

  .menu-card:hover {
    border-color: var(--blue);
    background: #f8fcff;
  }

  .menu-icon {
    display: block;
    margin-bottom: 8px;
    font-size: 2.4rem;
  }

  .menu-title {
    display: block;
    color: var(--blue-dark);
    font-size: 1.45rem;
    font-weight: 900;
  }

  .menu-description {
    display: block;
    margin-top: 8px;
    font-size: 1rem;
  }

  .menu-arrow {
    display: block;
    margin-top: 14px;
    color: var(--blue);
    font-size: 1.05rem;
    font-weight: 900;
  }

  /* =========================
     濃度のイメージ
  ========================= */

  .image-card {
    padding: 14px;
  }

  .image-heading {
    display: flex;
    flex-wrap: wrap;
    align-items: baseline;
    justify-content: space-between;
    gap: 4px 12px;
    margin-bottom: 10px;
  }

  .image-heading h2,
  .image-heading p {
    margin: 0;
  }

  .image-heading p {
    font-size: 1rem;
  }

  .image-layout {
    display: grid;
    grid-template-columns:
      minmax(170px, 0.75fr)
      minmax(260px, 1.05fr)
      minmax(280px, 1.15fr);
    gap: 12px;
    align-items: stretch;
  }

  .beaker-box,
  .control-box,
  .result-box {
    min-width: 0;
    padding: 13px;
    border-radius: 12px;
  }

  .beaker-box {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    text-align: center;
    background: #edf9fd;
  }

  .beaker-box svg {
    display: block;
    width: min(100%, 185px);
    height: auto;
    max-height: 245px;
  }

  .beaker-caption {
    margin: 7px 0 0;
    font-size: 0.88rem;
    font-weight: 800;
  }

  .control-box {
    background: #f3f8fb;
  }

  .control-box h3,
  .result-box h3 {
    margin: 0 0 10px;
    color: var(--blue-dark);
    font-size: 1.15rem;
  }

  .control {
    margin-bottom: 11px;
  }

  .control:last-of-type {
    margin-bottom: 0;
  }

  .control label {
    display: block;
    margin-bottom: 4px;
    font-size: 1rem;
    font-weight: 900;
  }

  input[type="number"],
  select {
    width: 100%;
    min-height: 44px;
    padding: 7px 10px;
    color: var(--ink);
    background: white;
    border: 2px solid #a8c3d2;
    border-radius: 8px;
    font-size: 1.1rem;
    font-weight: 900;
  }

  input[type="range"] {
    width: 100%;
    min-height: 30px;
    margin: 3px 0 0;
    accent-color: var(--blue);
  }

  .control-note {
    margin: 3px 0 0;
    color: #496779;
    font-size: 0.8rem;
    font-weight: 800;
  }

  .error {
    margin: 5px 0 0;
    color: var(--red);
    font-size: 0.85rem;
    font-weight: 900;
  }

  .error:empty {
    display: none;
  }

  .result-box {
    background: #eaf5fb;
  }

  .result-item {
    padding: 8px 0;
    border-bottom: 1px solid #c5dce9;
  }

  .result-item:last-child {
    border-bottom: 0;
  }

  .result-top {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    align-items: baseline;
    gap: 2px 8px;
  }

  .result-label {
    font-size: 1rem;
    font-weight: 900;
  }

  .result-value {
    color: var(--blue-dark);
    font-size: clamp(1.4rem, 2.6vw, 1.9rem);
    font-weight: 900;
    text-align: right;
    overflow-wrap: anywhere;
  }

  .result-unit {
    font-size: 0.9rem;
  }

  .result-formula {
    margin-top: 3px;
    color: #436579;
    font-size: 0.88rem;
    font-weight: 800;
    overflow-wrap: anywhere;
  }

  .study-details {
    margin-top: 9px;
    padding: 9px 14px;
    background: white;
    border: 1px solid var(--border);
    border-radius: 10px;
  }

  summary {
    color: var(--blue-dark);
    cursor: pointer;
    font-weight: 900;
  }

  .study-details ul {
    margin: 8px 0;
    padding-left: 1.4em;
  }

  .study-details li {
    margin-bottom: 5px;
  }

  /* =========================
     クイズ
  ========================= */

  .quiz-card {
    max-width: 900px;
    margin: auto;
    padding: clamp(16px, 2.5vw, 24px);
  }

  .quiz-top {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    align-items: center;
    gap: 8px;
  }

  .quiz-top h2 {
    margin: 0;
  }

  .progress-label {
    color: var(--blue-dark);
    font-size: 1rem;
    font-weight: 900;
  }

  .progress-track {
    height: 10px;
    margin: 12px 0 16px;
    overflow: hidden;
    background: #d9eaf3;
    border-radius: 20px;
  }

  .progress-bar {
    width: 0;
    height: 100%;
    background: #2589ad;
    transition: width 0.2s;
  }

  .question-number {
    display: inline-block;
    padding: 4px 12px;
    color: white;
    background: var(--blue);
    border-radius: 20px;
    font-size: 0.95rem;
    font-weight: 900;
  }

  .question-text {
    margin: 10px 0 15px;
    font-size: clamp(1.15rem, 2.3vw, 1.4rem);
    font-weight: 900;
    line-height: 1.5;
  }

  .choices {
    display: grid;
    grid-template-columns: repeat(2, minmax(0, 1fr));
    gap: 10px;
  }

  .choice {
    min-height: 66px;
    padding: 10px 12px;
    text-align: left;
    color: var(--ink);
    background: #f6fbfe;
    border: 2px solid #bfd8e6;
    border-radius: 10px;
    font-size: 1.1rem;
    font-weight: 900;
  }

  .choice:hover:not(:disabled) {
    background: #e8f5fc;
    border-color: var(--blue);
  }

  .choice:disabled {
    cursor: default;
    opacity: 1;
  }

  .choice.correct-choice {
    color: #105c39;
    background: #e3f6e9;
    border-color: #258e59;
  }

  .choice.wrong-choice {
    color: #88232b;
    background: #fff0f0;
    border-color: #c65058;
  }

  .choice-letter {
    display: inline-flex;
    width: 30px;
    height: 30px;
    margin-right: 8px;
    align-items: center;
    justify-content: center;
    color: white;
    background: #61879d;
    border-radius: 50%;
    font-size: 0.9rem;
    font-weight: 900;
  }

  .feedback {
    margin-top: 14px;
    padding: 12px 15px;
    border-radius: 10px;
  }

  .feedback.correct {
    background: #e5f6ec;
    border-left: 5px solid #258e59;
  }

  .feedback.incorrect {
    background: #fff0eb;
    border-left: 5px solid #d06a49;
  }

  .feedback-title {
    margin: 0 0 4px;
    font-size: 1.2rem;
    font-weight: 900;
  }

  .feedback p {
    margin: 4px 0;
  }

  .quiz-actions {
    margin-top: 12px;
    text-align: right;
  }

  .quiz-summary {
    text-align: center;
  }

  .score {
    margin: 18px 0;
    color: var(--blue-dark);
    font-size: clamp(1.7rem, 4vw, 2.5rem);
    font-weight: 900;
  }

  .summary-actions {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 10px;
  }

  [hidden] {
    display: none !important;
  }

  /* 狭い画面では縦に並べる */
  @media (max-width: 760px) {
    .image-layout {
      grid-template-columns: minmax(140px, 0.8fr) minmax(0, 1.2fr);
    }

    .result-box {
      grid-column: 1 / -1;
      display: grid;
      grid-template-columns: repeat(3, minmax(0, 1fr));
      gap: 8px;
    }

    .result-box h3 {
      grid-column: 1 / -1;
      margin-bottom: 0;
    }

    .result-item {
      padding: 4px 8px;
      border-right: 1px solid #c5dce9;
      border-bottom: 0;
    }

    .result-item:last-child {
      border-right: 0;
    }

    .result-top {
      display: block;
    }

    .result-value {
      text-align: left;
    }
  }

  @media (max-width: 520px) {
    body {
      font-size: 16px;
    }

    main {
      width: calc(100% - 16px);
      margin-top: 8px;
    }

    .header-inner {
      padding: 9px 12px;
    }

    .menu-grid,
    .choices {
      grid-template-columns: 1fr;
    }

    .menu-card {
      min-height: 150px;
    }

    .image-card {
      padding: 10px;
    }

    .image-layout {
      gap: 8px;
    }

    .beaker-box,
    .control-box,
    .result-box {
      padding: 9px;
    }

    .beaker-box svg {
      width: min(100%, 140px);
    }

    .beaker-caption,
    .control-note {
      font-size: 0.75rem;
    }

    .result-box {
      grid-template-columns: 1fr;
    }

    .result-box h3 {
      grid-column: auto;
    }

    .result-item {
      border-right: 0;
      border-bottom: 1px solid #c5dce9;
    }

    .result-top {
      display: flex;
    }

    .result-value {
      text-align: right;
    }
  }
</style>
</head>

<body>

<header>
  <div class="header-inner">
    <h1>濃度をイメージしよう</h1>
    <p>化学基礎｜質量％濃度・モル濃度</p>
  </div>
</header>

<main>

  <!-- メニュー -->
  <section id="menu-screen" class="screen active">
    <div class="card menu-intro">
      <h2>学習メニュー</h2>
      <p>学習したい内容を選びましょう。</p>
    </div>

    <div class="menu-grid">
      <button type="button" class="menu-card" id="open-image">
        <span class="menu-icon" aria-hidden="true">🧪</span>
        <span class="menu-title">濃度のイメージ</span>
        <span class="menu-description">
          水と NaCl の量を変えて、濃度を見てみよう。
        </span>
        <span class="menu-arrow">スタート →</span>
      </button>

      <button type="button" class="menu-card" id="open-quiz">
        <span class="menu-icon" aria-hidden="true">✏️</span>
        <span class="menu-title">４択クイズ</span>
        <span class="menu-description">
          簡単な計算にチャレンジ！答えを選んで解説を確認しよう。
        </span>
        <span class="menu-arrow">スタート →</span>
      </button>
    </div>
  </section>

  <!-- 濃度のイメージ -->
  <section id="image-screen" class="screen">
    <button type="button" class="back-button go-menu">
      ← メニューへ
    </button>

    <div class="card image-card">
      <div class="image-heading">
        <h2>🧪 NaCl を溶かしてみよう</h2>
        <p>量を変えると、濃度はどう変わる？</p>
      </div>

      <div class="image-layout">

        <!-- ビーカー -->
        <div class="beaker-box">
          <svg
            viewBox="0 0 220 245"
            role="img"
            aria-label="水溶液の入ったビーカーの模式図"
          >
            <defs>
              <clipPath id="beaker-clip">
                <path
                  d="M 40 25 L 50 218 Q 51 230 64 230
                     L 156 230 Q 169 230 170 218 L 180 25 Z"
                ></path>
              </clipPath>
            </defs>

            <g clip-path="url(#beaker-clip)">
              <rect
                x="35"
                y="75"
                width="150"
                height="160"
                fill="#b7e6f5"
              ></rect>

              <path
                d="M 35 75 Q 72 69 110 75 T 185 75"
                fill="none"
                stroke="#55b8d6"
                stroke-width="3"
              ></path>

              <g id="particles"></g>
            </g>

            <path
              d="M 40 25 L 50 218 Q 51 230 64 230
                 L 156 230 Q 169 230 170 218 L 180 25"
              fill="none"
              stroke="#416d84"
              stroke-width="5"
              stroke-linecap="round"
            ></path>

            <path
              d="M 34 25 H 186"
              fill="none"
              stroke="#416d84"
              stroke-width="5"
              stroke-linecap="round"
            ></path>

            <g stroke="#6a91a4" stroke-width="2">
              <line x1="47" y1="105" x2="64" y2="105"></line>
              <line x1="48" y1="140" x2="60" y2="140"></line>
              <line x1="49" y1="175" x2="66" y2="175"></line>
              <line x1="50" y1="205" x2="61" y2="205"></line>
            </g>
          </svg>

          <p class="beaker-caption">
            青：水溶液<br>
            白い点：NaCl の模式図
          </p>
        </div>

        <!-- 入力 -->
        <div class="control-box">
          <h3>量を指定</h3>

          <div class="control">
            <label for="volume">溶液の体積</label>
            <select id="volume">
              <option value="1000">1 L（1000 mL）</option>
              <option value="500">500 mL</option>
              <option value="100">100 mL</option>
            </select>
            <p class="control-note">溶かした後の溶液全体の体積</p>
          </div>

          <div class="control">
            <label for="water">水の質量［g］</label>
            <input
              id="water"
              type="number"
              min="0.01"
              step="any"
              value="1000"
              inputmode="decimal"
            >
          </div>

          <div class="control">
            <label for="salt">NaCl の質量［g］</label>
            <input
              id="salt"
              type="number"
              min="0"
              step="any"
              value="58.5"
              inputmode="decimal"
            >

            <input
              id="salt-range"
              type="range"
              min="0"
              max="200"
              step="0.5"
              value="58.5"
              aria-label="NaCl の質量をスライダーで変更"
            >

            <p class="control-note">
              スライダー：0〜200 g。数値は直接入力もできます。
            </p>
          </div>

          <p id="input-error" class="error" role="status"></p>
        </div>

        <!-- 計算結果 -->
        <div class="result-box" aria-live="polite">
          <h3>計算結果</h3>

          <div class="result-item">
            <div class="result-top">
              <span class="result-label">NaCl の物質量</span>
              <span class="result-value">
                <span id="mol-result">—</span>
                <span class="result-unit">mol</span>
              </span>
            </div>
            <div id="mol-formula" class="result-formula"></div>
          </div>

          <div class="result-item">
            <div class="result-top">
              <span class="result-label">質量％濃度</span>
              <span class="result-value">
                <span id="percent-result">—</span>
                <span class="result-unit">%</span>
              </span>
            </div>
            <div id="percent-formula" class="result-formula"></div>
          </div>

          <div class="result-item">
            <div class="result-top">
              <span class="result-label">モル濃度</span>
              <span class="result-value">
                <span id="molarity-result">—</span>
                <span class="result-unit">mol/L</span>
              </span>
            </div>
            <div id="molarity-formula" class="result-formula"></div>
          </div>
        </div>

      </div>
    </div>

    <details class="study-details">
      <summary>公式と観察のポイントを見る</summary>
      <ul>
        <li>
          NaCl の物質量［mol］
          ＝ NaCl の質量［g］÷ 58.5［g/mol］
        </li>
        <li>
          質量％濃度［%］
          ＝ 溶質の質量 ÷ 溶液の質量 × 100
        </li>
        <li>
          モル濃度［mol/L］
          ＝ 溶質の物質量 ÷ 溶液の体積［L］
        </li>
        <li>NaCl の量を増やすと、濃度はどう変わる？</li>
        <li>
          NaCl の量を変えずに溶液の体積を小さくすると、
          モル濃度はどう変わる？
        </li>
      </ul>
      <p>※計算結果は見やすく丸めて表示しています。</p>
    </details>
  </section>

  <!-- ４択クイズ -->
  <section id="quiz-screen" class="screen">
    <button type="button" class="back-button go-menu">
      ← メニューへ
    </button>

    <div class="card quiz-card">
      <div id="quiz-playing">
        <div class="quiz-top">
          <h2>✏️ ４択クイズ</h2>
          <span id="progress-label" class="progress-label"></span>
        </div>

        <div
          id="progress-track"
          class="progress-track"
          role="progressbar"
          aria-label="クイズの進み具合"
          aria-valuemin="0"
          aria-valuemax="5"
          aria-valuenow="0"
        >
          <div id="progress-bar" class="progress-bar"></div>
        </div>

        <span id="question-number" class="question-number"></span>
        <p id="question-text" class="question-text"></p>

        <div id="choices" class="choices" aria-label="選択肢"></div>

        <div id="feedback" class="feedback" role="status" hidden>
          <p id="feedback-title" class="feedback-title"></p>
          <p id="feedback-answer"></p>
          <p id="feedback-explanation"></p>
        </div>

        <div class="quiz-actions">
          <button
            type="button"
            id="next-question"
            class="primary-button"
            hidden
          >
            次の問題へ →
          </button>
        </div>
      </div>

      <div id="quiz-summary" class="quiz-summary" hidden>
        <h2>クイズ終了！</h2>
        <p id="score" class="score"></p>
        <p id="score-message"></p>

        <div class="summary-actions">
          <button type="button" id="retry-quiz" class="primary-button">
            もう一度挑戦
          </button>

          <button type="button" class="secondary-button go-menu">
            メニューへ
          </button>
        </div>
      </div>
    </div>
  </section>

</main>

<script>
"use strict";

/* =========================
   画面切り替え
========================= */

const screens = document.querySelectorAll(".screen");

function showScreen(id) {
  screens.forEach((screen) => {
    screen.classList.toggle("active", screen.id === id);
  });

  window.scrollTo(0, 0);
}

document.getElementById("open-image").addEventListener("click", () => {
  showScreen("image-screen");
});

document.getElementById("open-quiz").addEventListener("click", () => {
  startQuiz();
  showScreen("quiz-screen");
});

document.querySelectorAll(".go-menu").forEach((button) => {
  button.addEventListener("click", () => {
    showScreen("menu-screen");
  });
});

/* =========================
   濃度の計算
========================= */

const MOLAR_MASS_NACL = 58.5;

const volumeInput = document.getElementById("volume");
const waterInput = document.getElementById("water");
const saltInput = document.getElementById("salt");
const saltRange = document.getElementById("salt-range");
const inputError = document.getElementById("input-error");

const molResult = document.getElementById("mol-result");
const percentResult = document.getElementById("percent-result");
const molarityResult = document.getElementById("molarity-result");

const molFormula = document.getElementById("mol-formula");
const percentFormula = document.getElementById("percent-formula");
const molarityFormula = document.getElementById("molarity-formula");

const particles = document.getElementById("particles");
const svgNamespace = "http://www.w3.org/2000/svg";

function formatNumber(value) {
  if (!Number.isFinite(value)) return "—";
  if (value === 0) return "0";

  const absolute = Math.abs(value);

  if (absolute >= 1000000 || absolute < 0.001) {
    return value.toExponential(3);
  }

  return Number(value.toPrecision(4)).toLocaleString("ja-JP", {
    maximumFractionDigits: 8
  });
}

function clearResults() {
  molResult.textContent = "—";
  percentResult.textContent = "—";
  molarityResult.textContent = "—";

  molFormula.textContent = "";
  percentFormula.textContent = "";
  molarityFormula.textContent = "";

  particles.replaceChildren();
}

function drawParticles(molarity) {
  particles.replaceChildren();

  if (molarity <= 0) return;

  /*
    白い点は模式図。
    濃度が高いほど点を増やすが、実際の粒子数を示すものではない。
  */
  const count = Math.min(
    65,
    Math.max(3, Math.round(8 + 18 * Math.log10(1 + molarity * 10)))
  );

  for (let i = 0; i < count; i++) {
    const x = 62 + ((i * 47 + 13) % 96);
    const y = 88 + ((i * 67 + 17) % 126);

    const dot = document.createElementNS(svgNamespace, "circle");

    dot.setAttribute("cx", x);
    dot.setAttribute("cy", y);
    dot.setAttribute("r", i % 3 === 0 ? "3.3" : "2.6");
    dot.setAttribute("fill", "#ffffff");
    dot.setAttribute("stroke", "#4d9dbd");
    dot.setAttribute("stroke-width", "1");

    particles.appendChild(dot);
  }
}

function updateCalculation() {
  const waterText = waterInput.value.trim();
  const saltText = saltInput.value.trim();

  const water = Number(waterText);
  const salt = Number(saltText);
  const volumeML = Number(volumeInput.value);

  if (
    waterText === "" ||
    saltText === "" ||
    !Number.isFinite(water) ||
    !Number.isFinite(salt) ||
    water <= 0 ||
    salt < 0
  ) {
    inputError.textContent =
      "水は 0 より大きく、NaCl は 0 以上の値を入力してください。";
    clearResults();
    return;
  }

  const solutionMass = water + salt;
  const volumeL = volumeML / 1000;
  const mol = salt / MOLAR_MASS_NACL;
  const percent = (salt / solutionMass) * 100;
  const molarity = mol / volumeL;

  if (
    !Number.isFinite(solutionMass) ||
    !Number.isFinite(mol) ||
    !Number.isFinite(percent) ||
    !Number.isFinite(molarity)
  ) {
    inputError.textContent = "計算できる範囲の数値を入力してください。";
    clearResults();
    return;
  }

  inputError.textContent = "";

  molResult.textContent = formatNumber(mol);
  percentResult.textContent = formatNumber(percent);
  molarityResult.textContent = formatNumber(molarity);

  molFormula.textContent =
    `${formatNumber(salt)} g ÷ 58.5 g/mol`;

  percentFormula.textContent =
    `${formatNumber(salt)} ÷ ` +
    `(${formatNumber(water)} + ${formatNumber(salt)}) × 100`;

  molarityFormula.textContent =
    `約 ${formatNumber(mol)} mol ÷ ${formatNumber(volumeL)} L`;

  drawParticles(molarity);
}

/*
  体積を切り替えたとき、水の質量を初期値に設定。
  設定後は水の質量を自由に変更できる。
*/
volumeInput.addEventListener("change", () => {
  waterInput.value = volumeInput.value;
  updateCalculation();
});

waterInput.addEventListener("input", updateCalculation);

saltInput.addEventListener("input", () => {
  const value = Number(saltInput.value);

  if (
    saltInput.value.trim() !== "" &&
    Number.isFinite(value) &&
    value >= 0
  ) {
    saltRange.value = Math.min(value, Number(saltRange.max));
  }

  updateCalculation();
});

saltRange.addEventListener("input", () => {
  saltInput.value = saltRange.value;
  updateCalculation();
});

updateCalculation();

/* =========================
   ４択クイズ
========================= */

const questions = [
  {
    question:
      "水 90 g に NaCl 10 g をすべて溶かしました。水溶液の質量％濃度は？",
    choices: [
      "5 %",
      "10 %",
      "20 %",
      "90 %"
    ],
    answer: 1,
    explanation:
      "溶液の質量は 90 + 10 = 100 g。" +
      "10 ÷ 100 × 100 = 10 % です。"
  },
  {
    question:
      "水 80 g に NaCl 20 g をすべて溶かしました。水溶液の質量％濃度は？",
    choices: [
      "10 %",
      "20 %",
      "25 %",
      "80 %"
    ],
    answer: 1,
    explanation:
      "溶液の質量は 80 + 20 = 100 g。" +
      "20 ÷ 100 × 100 = 20 % です。"
  },
  {
    question:
      "NaCl 0.20 mol を水に溶かし、溶液を 1.0 L にしました。モル濃度は？",
    choices: [
      "0.10 mol/L",
      "0.20 mol/L",
      "0.50 mol/L",
      "2.0 mol/L"
    ],
    answer: 1,
    explanation:
      "モル濃度は物質量 ÷ 溶液の体積。" +
      "0.20 ÷ 1.0 = 0.20 mol/L です。"
  },
  {
    question:
      "NaCl 0.10 mol を水に溶かし、溶液を 500 mL にしました。モル濃度は？",
    choices: [
      "0.05 mol/L",
      "0.10 mol/L",
      "0.20 mol/L",
      "0.50 mol/L"
    ],
    answer: 2,
    explanation:
      "500 mL = 0.50 L。" +
      "0.10 ÷ 0.50 = 0.20 mol/L です。"
  },
  {
    question:
      "NaCl 5.85 g を水に溶かし、溶液を 1.0 L にしました。" +
      "モル濃度は？ ただし、NaCl の式量は 58.5 とします。",
    choices: [
      "0.01 mol/L",
      "0.10 mol/L",
      "1.0 mol/L",
      "10 mol/L"
    ],
    answer: 1,
    explanation:
      "NaCl のモル質量は 58.5 g/mol。" +
      "物質量は 5.85 ÷ 58.5 = 0.10 mol。" +
      "0.10 ÷ 1.0 = 0.10 mol/L です。"
  }
];

const letters = ["ア", "イ", "ウ", "エ"];

const quizPlaying = document.getElementById("quiz-playing");
const quizSummary = document.getElementById("quiz-summary");

const progressLabel = document.getElementById("progress-label");
const progressTrack = document.getElementById("progress-track");
const progressBar = document.getElementById("progress-bar");

const questionNumber = document.getElementById("question-number");
const questionText = document.getElementById("question-text");
const choicesContainer = document.getElementById("choices");

const feedback = document.getElementById("feedback");
const feedbackTitle = document.getElementById("feedback-title");
const feedbackAnswer = document.getElementById("feedback-answer");
const feedbackExplanation = document.getElementById("feedback-explanation");

const nextButton = document.getElementById("next-question");
const scoreDisplay = document.getElementById("score");
const scoreMessage = document.getElementById("score-message");

let currentQuestion = 0;
let score = 0;
let answered = false;

function startQuiz() {
  currentQuestion = 0;
  score = 0;
  answered = false;

  quizPlaying.hidden = false;
  quizSummary.hidden = true;

  renderQuestion();
}

function renderQuestion() {
  const question = questions[currentQuestion];

  answered = false;
  feedback.hidden = true;
  feedback.className = "feedback";
  nextButton.hidden = true;

  progressLabel.textContent =
    `${currentQuestion + 1} / ${questions.length} 問`;

  progressTrack.setAttribute("aria-valuemax", questions.length);
  progressTrack.setAttribute("aria-valuenow", currentQuestion);

  progressBar.style.width =
    `${(currentQuestion / questions.length) * 100}%`;

  questionNumber.textContent = `第 ${currentQuestion + 1} 問`;
  questionText.textContent = question.question;

  choicesContainer.replaceChildren();

  question.choices.forEach((choiceText, index) => {
    const button = document.createElement("button");
    button.type = "button";
    button.className = "choice";

    const letter = document.createElement("span");
    letter.className = "choice-letter";
    letter.textContent = letters[index];

    const text = document.createElement("span");
    text.textContent = choiceText;

    button.append(letter, text);
    button.addEventListener("click", () => selectAnswer(index));

    choicesContainer.appendChild(button);
  });
}

function selectAnswer(selectedIndex) {
  if (answered) return;

  answered = true;

  const question = questions[currentQuestion];
  const correct = selectedIndex === question.answer;
  const choiceButtons = choicesContainer.querySelectorAll(".choice");

  if (correct) {
    score++;
  }

  choiceButtons.forEach((button, index) => {
    button.disabled = true;

    if (index === question.answer) {
      button.classList.add("correct-choice");
    } else if (index === selectedIndex) {
      button.classList.add("wrong-choice");
    }
  });

  feedback.hidden = false;
  feedback.classList.add(correct ? "correct" : "incorrect");

  feedbackTitle.textContent = correct ? "正解！" : "おしい！";

  feedbackAnswer.textContent =
    `正解：${letters[question.answer]}　` +
    question.choices[question.answer];

  feedbackExplanation.textContent = question.explanation;

  nextButton.textContent =
    currentQuestion === questions.length - 1
      ? "結果を見る →"
      : "次の問題へ →";

  nextButton.hidden = false;

  progressTrack.setAttribute("aria-valuenow", currentQuestion + 1);

  progressBar.style.width =
    `${((currentQuestion + 1) / questions.length) * 100}%`;
}

nextButton.addEventListener("click", () => {
  if (currentQuestion < questions.length - 1) {
    currentQuestion++;
    renderQuestion();
  } else {
    showSummary();
  }
});

function showSummary() {
  quizPlaying.hidden = true;
  quizSummary.hidden = false;

  scoreDisplay.textContent =
    `${questions.length} 問中 ${score} 問正解！`;

  if (score === questions.length) {
    scoreMessage.textContent =
      "全問正解！濃度の考え方をよく理解しています。";
  } else if (score >= 3) {
    scoreMessage.textContent =
      "よくできました！解説を確認して、もう一度挑戦しましょう。";
  } else {
    scoreMessage.textContent =
      "イメージ画面で確認してから、もう一度挑戦してみましょう。";
  }
}

document.getElementById("retry-quiz").addEventListener("click", startQuiz);
</script>

</body>
</html>
