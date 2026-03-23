# flugamewou7.github.io
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>AI Study Buddy - Free Quizlet Alternative</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/4.0.379/pdf.min.mjs" type="module"></script>
  <style>
    :root {
      --bg: #f8f9fa;
      --text: #212529;
      --card: #ffffff;
      --primary: #4361ee;
      --primary-dark: #3f37c9;
      --accent: #ff6b6b;
      --gray: #6c757d;
    }
    [data-theme="dark"] {
      --bg: #121212;
      --text: #e0e0e0;
      --card: #1e1e1e;
      --primary: #5c7cfa;
      --primary-dark: #4c6ef5;
      --accent: #ff8787;
      --gray: #adb5bd;
    }
    body {
      font-family: system-ui, -apple-system, sans-serif;
      background: var(--bg);
      color: var(--text);
      margin: 0;
      padding: 20px;
      min-height: 100vh;
      transition: background 0.3s, color 0.3s;
    }
    .container { max-width: 1100px; margin: 0 auto; }
    header {
      text-align: center;
      margin-bottom: 2rem;
    }
    h1 {
      margin: 0;
      font-size: 2.5rem;
      color: var(--primary);
    }
    .theme-toggle {
      position: absolute;
      top: 20px;
      right: 20px;
      background: none;
      border: 1px solid var(--gray);
      color: var(--text);
      padding: 8px 12px;
      border-radius: 50px;
      cursor: pointer;
    }
    .input-area {
      background: var(--card);
      border-radius: 12px;
      padding: 1.5rem;
      box-shadow: 0 4px 20px rgba(0,0,0,0.08);
      margin-bottom: 2rem;
    }
    textarea, input[type="file"] {
      width: 100%;
      padding: 12px;
      margin: 10px 0;
      border: 1px solid #ccc;
      border-radius: 8px;
      font-size: 1rem;
      background: var(--bg);
      color: var(--text);
    }
    button {
      background: var(--primary);
      color: white;
      border: none;
      padding: 12px 24px;
      border-radius: 8px;
      font-size: 1rem;
      cursor: pointer;
      margin: 8px 8px 8px 0;
      transition: background 0.2s;
    }
    button:hover { background: var(--primary-dark); }
    button.secondary { background: var(--gray); }
    .tabs {
      display: flex;
      gap: 10px;
      margin: 1.5rem 0;
      flex-wrap: wrap;
    }
    .tab-btn {
      padding: 10px 20px;
      background: transparent;
      border: 2px solid var(--primary);
      color: var(--primary);
      border-radius: 50px;
      cursor: pointer;
      font-weight: 600;
    }
    .tab-btn.active {
      background: var(--primary);
      color: white;
    }
    .study-area {
      background: var(--card);
      border-radius: 12px;
      padding: 2rem;
      box-shadow: 0 4px 20px rgba(0,0,0,0.08);
      min-height: 400px;
    }
    .flashcard {
      width: 100%; max-width: 500px;
      height: 280px;
      margin: 2rem auto;
      perspective: 1000px;
    }
    .flashcard-inner {
      position: relative;
      width: 100%; height: 100%;
      transition: transform 0.6s;
      transform-style: preserve-3d;
    }
    .flashcard.flipped .flashcard-inner { transform: rotateY(180deg); }
    .flashcard-front, .flashcard-back {
      position: absolute;
      width: 100%; height: 100%;
      backface-visibility: hidden;
      display: flex; align-items: center; justify-content: center;
      padding: 20px; box-sizing: border-box;
      border-radius: 16px;
      font-size: 1.4rem;
      text-align: center;
      background: var(--card);
      box-shadow: 0 10px 30px rgba(0,0,0,0.12);
    }
    .flashcard-back { transform: rotateY(180deg); background: linear-gradient(135deg, var(--primary), var(--primary-dark)); color: white; }
    .quiz-question { font-size: 1.3rem; margin-bottom: 1.5rem; }
    .options { display: grid; gap: 12px; }
    .option-btn {
      padding: 14px;
      background: var(--card);
      border: 2px solid #dee2e6;
      border-radius: 10px;
      text-align: left;
      cursor: pointer;
    }
    .option-btn:hover { border-color: var(--primary); }
    .option-btn.correct { background: #d4edda; border-color: #28a745; }
    .option-btn.wrong { background: #f8d7da; border-color: #dc3545; }
    .hidden { display: none; }
    .loading { text-align: center; font-style: italic; color: var(--gray); }
    footer { text-align: center; margin-top: 3rem; color: var(--gray); font-size: 0.9rem; }
  </style>
</head>
<body data-theme="light">

<button class="theme-toggle" onclick="toggleTheme()">Dark Mode</button>

<div class="container">
  <header>
    <h1>AI Study Buddy</h1>
    <p>Your free, private Quizlet-style study tool — powered by your notes</p>
  </header>

  <div class="input-area">
    <h2>1. Add Your Notes</h2>
    <textarea id="notes" rows="8" placeholder="Paste your notes here... or upload a PDF below"></textarea>
    <input type="file" id="pdfUpload" accept=".pdf" />
    <p style="color:var(--gray); font-size:0.95rem;">PDF support uses PDF.js — works offline after first load</p>
    <button onclick="generateContent()">Generate Study Materials</button>
  </div>

  <div id="output" class="hidden">
    <div class="tabs">
      <button class="tab-btn active" onclick="showTab('guide')">Study Guide</button>
      <button class="tab-btn" onclick="showTab('flashcards')">Flashcards</button>
      <button class="tab-btn" onclick="showTab('quiz')">Quiz</button>
      <button class="tab-btn" onclick="showTab('recall')">Active Recall</button>
      <button class="tab-btn" onclick="showTab('game')">Mini Game</button>
    </div>

    <div class="study-area">
      <div id="guide" class="tab-content">
        <h2>Quick Study Guide</h2>
        <div id="guideContent"></div>
      </div>

      <div id="flashcards" class="tab-content hidden">
        <h2>Flashcards</h2>
        <div id="fcDeck"></div>
        <div style="text-align:center; margin:1.5rem 0;">
          <button onclick="prevCard()">Previous</button>
          <button onclick="flipCard()">Flip</button>
          <button onclick="nextCard()">Next</button>
        </div>
      </div>

      <div id="quiz" class="tab-content hidden">
        <h2>Multiple Choice Quiz</h2>
        <div id="quizContent"></div>
      </div>

      <div id="recall" class="tab-content hidden">
        <h2>Active Recall</h2>
        <div id="recallContent"></div>
      </div>

      <div id="game" class="tab-content hidden">
        <h2>Mini Matching Game</h2>
        <div id="gameContent"></div>
      </div>
    </div>
  </div>

  <footer>Made with ❤️ for students • Fully local in your browser • GitHub Pages friendly</footer>
</div>

<script type="module">
  // PDF.js worker setup
  pdfjsLib.GlobalWorkerOptions.workerSrc = 'https://cdnjs.cloudflare.com/ajax/libs/pdf.js/4.0.379/pdf.worker.min.mjs';

  let cards = [];
  let currentCard = 0;
  let quizQuestions = [];
  let currentQuiz = 0;
  let theme = 'light';

  function toggleTheme() {
    theme = theme === 'light' ? 'dark' : 'light';
    document.body.dataset.theme = theme;
    document.querySelector('.theme-toggle').textContent = theme === 'light' ? 'Dark Mode' : 'Light Mode';
  }

  function showTab(tabId) {
    document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
    event.target.classList.add('active');
    document.querySelectorAll('.tab-content').forEach(c => c.classList.add('hidden'));
    document.getElementById(tabId).classList.remove('hidden');
  }

  async function extractPDFText(file) {
    const arrayBuffer = await file.arrayBuffer();
    const pdf = await pdfjsLib.getDocument({data: arrayBuffer}).promise;
    let text = '';
    for (let i = 1; i <= pdf.numPages; i++) {
      const page = await pdf.getPage(i);
      const content = await page.getTextContent();
      text += content.items.map(item => item.str).join(' ') + '\n\n';
    }
    return text.trim();
  }

  async function generateContent() {
    let text = document.getElementById('notes').value.trim();
    const file = document.getElementById('pdfUpload').files[0];

    if (file) {
      document.getElementById('notes').value = "Extracting PDF... please wait";
      text = await extractPDFText(file);
      document.getElementById('notes').value = text;
    }

    if (!text) {
      alert("Please paste notes or upload a PDF first!");
      return;
    }

    document.getElementById('output').classList.remove('hidden');

    // Simple "AI" generation logic
    const lines = text.split('\n').filter(l => l.trim());
    cards = [];

    // Try to detect definition style (term: definition or term - definition)
    lines.forEach(line => {
      const clean = line.trim();
      if (!clean) return;

      // Common patterns
      if (clean.includes(':')) {
        const [q, a] = clean.split(':').map(s => s.trim());
        if (q && a) cards.push({q, a});
      } else if (clean.match(/[-–—]/)) {
        const [q, a] = clean.split(/[-–—]/).map(s => s.trim());
        if (q && a) cards.push({q, a});
      } else if (clean.match(/\b(is|are|was|were|means|refers to)\b/i)) {
        cards.push({q: clean, a: "Explain this concept in your own words."});
      }
    });

    // Fallback: sentence-based cards
    if (cards.length < 5) {
      const sentences = text.match(/[^.!?]+[.!?]+/g) || [];
      sentences.forEach(s => {
        const sent = s.trim();
        if (sent.split(' ').length > 6 && sent.split(' ').length < 25) {
          cards.push({
            q: "What does this sentence mean?\n" + sent,
            a: sent
          });
        }
      });
    }

    // Generate variations
    const finalCards = [];
    cards.forEach(c => {
      finalCards.push({front: c.q, back: c.a}); // basic
      finalCards.push({front: c.a + " ← what is this?", back: c.q}); // reverse
      finalCards.push({front: "Complete: " + c.q.replace(/(\w+)/, '_____'), back: c.q}); // fill blank
      finalCards.push({front: c.q, back: "True or False? → " + c.a, type: 'tf'}); // tf placeholder
    });

    cards = finalCards.slice(0, 80); // limit for performance

    // Study guide
    const guide = lines.slice(0, 20).map(l => `<li>${l}</li>`).join('');
    document.getElementById('guideContent').innerHTML = `<ul>${guide || '<li>No key points detected — try clearer formatting</li>'}</ul>`;

    // Flashcards
    renderFlashcard();

    // Quiz (pick 10 random)
    quizQuestions = cards
      .filter(c => !c.type || c.type !== 'tf')
      .sort(() => Math.random() - 0.5)
      .slice(0, 12)
      .map(c => ({
        q: c.front,
        a: c.back,
        options: shuffle([c.back, ...generateWrongAnswers(c.back)])
      }));

    currentQuiz = 0;
    renderQuiz();

    // Active recall
    renderActiveRecall();

    // Game (simple matching)
    renderMatchingGame();
  }

  function shuffle(array) {
    return array.sort(() => Math.random() - 0.5);
  }

  function generateWrongAnswers(correct) {
    // Dumb but effective placeholders
    const wrongs = [
      "Not this one",
      "Incorrect option",
      correct.split(' ').reverse().join(' '),
      correct + " (wrong version)",
      "Maybe this?",
      correct.slice(0, Math.floor(correct.length/2)) + "..."
    ];
    return wrongs.slice(0, 3);
  }

  // Flashcard logic
  function renderFlashcard() {
    if (!cards.length) {
      document.getElementById('fcDeck').innerHTML = "<p>No flashcards generated yet. Try better formatted notes!</p>";
      return;
    }
    const card = cards[currentCard];
    document.getElementById('fcDeck').innerHTML = `
      <div class="flashcard" id="fc">
        <div class="flashcard-inner">
          <div class="flashcard-front">${card.front.replace(/\n/g, '<br>')}</div>
          <div class="flashcard-back">${card.back.replace(/\n/g, '<br>')}</div>
        </div>
      </div>
      <p style="text-align:center;">Card ${currentCard + 1} / ${cards.length}</p>
    `;
  }

  function flipCard() {
    document.getElementById('fc')?.classList.toggle('flipped');
  }
  function nextCard() { currentCard = (currentCard + 1) % cards.length; renderFlashcard(); }
  function prevCard() { currentCard = (currentCard - 1 + cards.length) % cards.length; renderFlashcard(); }

  // Quiz
  function renderQuiz() {
    if (!quizQuestions.length) {
      document.getElementById('quizContent').innerHTML = "<p>Not enough content for quiz yet.</p>";
      return;
    }
    const q = quizQuestions[currentQuiz];
    const opts = shuffle([...q.options]);
    let html = `<div class="quiz-question">${q.q.replace(/\n/g,'<br>')}</div>`;
    html += '<div class="options">';
    opts.forEach(o => {
      html += `<button class="option-btn" onclick="checkAnswer('${o}', '${q.a}')">${o}</button>`;
    });
    html += '</div>';
    html += `<p>Question ${currentQuiz + 1} / ${quizQuestions.length}</p>`;
    document.getElementById('quizContent').innerHTML = html;
  }

  window.checkAnswer = function(selected, correct) {
    const btns = document.querySelectorAll('.option-btn');
    btns.forEach(b => {
      if (b.textContent === correct) b.classList.add('correct');
      if (b.textContent === selected && selected !== correct) b.classList.add('wrong');
      b.disabled = true;
    });
    setTimeout(() => {
      currentQuiz = (currentQuiz + 1) % quizQuestions.length;
      renderQuiz();
    }, 1400);
  };

  // Active Recall (type answer)
  function renderActiveRecall() {
    if (!cards.length) return;
    const idx = Math.floor(Math.random() * cards.length);
    const card = cards[idx];
    document.getElementById('recallContent').innerHTML = `
      <p style="font-size:1.3rem;">${card.front.replace(/\n/g,'<br>')}</p>
      <textarea id="recallInput" rows="4" placeholder="Type your answer here..."></textarea>
      <button onclick="showRecallAnswer(${idx})">Show Answer</button>
      <div id="recallAnswer" class="hidden" style="margin-top:1rem; padding:12px; background:#e9ecef; border-radius:8px;"></div>
    `;
  }

  window.showRecallAnswer = function(idx) {
    const ans = document.getElementById('recallAnswer');
    ans.innerHTML = `<strong>Answer:</strong><br>${cards[idx].back.replace(/\n/g,'<br>')}`;
    ans.classList.remove('hidden');
  };

  // Simple matching game
  function renderMatchingGame() {
    if (cards.length < 4) {
      document.getElementById('gameContent').innerHTML = "<p>Need more cards for matching game.</p>";
      return;
    }
    const sample = shuffle(cards.slice()).slice(0, 6);
    const terms = sample.map(c => c.front);
    const defs  = shuffle(sample.map(c => c.back));

    let html = '<div style="display:grid; grid-template-columns:1fr 1fr; gap:1rem;">';
    html += '<div><h3>Terms</h3>';
    terms.forEach(t => html += `<div style="padding:12px; background:var(--card); border:1px solid #dee2e6; border-radius:8px;">${t}</div>`);
    html += '</div><div><h3>Definitions (shuffled)</h3>';
    defs.forEach(d => html += `<div style="padding:12px; background:var(--card); border:1px solid #dee2e6; border-radius:8px;">${d}</div>`);
    html += '</div></div>';
    html += '<p style="text-align:center; margin-top:1.5rem;">(Drag & drop coming in future update – for now match mentally!)</p>';
    document.getElementById('gameContent').innerHTML = html;
  }

</script>
</body>
</html>
