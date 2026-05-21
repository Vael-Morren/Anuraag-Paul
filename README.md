<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Vael Morren — The Realms of an Author & Developer</title>
<link href="https://fonts.googleapis.com/css2?family=Cinzel+Decorative:wght@400;700&family=Cinzel:wght@400;600&family=IM+Fell+English:ital@0;1&family=MedievalSharp&display=swap" rel="stylesheet">
<style>
:root {
  /* Obsidian Ledger (dark) */
  --bg: #1a1a1a;
  --bg2: #222220;
  --bg3: #2a2a27;
  --text: #c9a84c;
  --text-soft: #a8924a;
  --text-muted: #7a6a3a;
  --accent1: #6b8e6e;
  --accent2: #4a6e8a;
  --border: #3a3428;
  --glow: rgba(201,168,76,0.15);
  --particle: rgba(201,168,76,0.6);
  --hud-bg: rgba(26,26,26,0.9);
  --btn-bg: #2a2418;
  --btn-border: #c9a84c;
  --tab-active: rgba(201,168,76,0.12);
  --shadow: rgba(0,0,0,0.6);
}
body.light {
  --bg: #f5f0e8;
  --bg2: #ede7d8;
  --bg3: #e4dccb;
  --text: #2c2820;
  --text-soft: #4a4038;
  --text-muted: #7a7060;
  --accent1: #7a9070;
  --accent2: #a09080;
  --border: #c8b898;
  --glow: rgba(44,40,32,0.08);
  --particle: rgba(120,90,50,0.5);
  --hud-bg: rgba(245,240,232,0.92);
  --btn-bg: #e8dfc8;
  --btn-border: #8a6a40;
  --tab-active: rgba(44,40,32,0.08);
  --shadow: rgba(100,80,40,0.25);
}
body.neutral {
  --bg: #3a3d42;
  --bg2: #42454a;
  --bg3: #4a4e54;
  --text: #e8eaed;
  --text-soft: #c8ccd2;
  --text-muted: #8a909a;
  --accent1: #6a7a8a;
  --accent2: #7a8898;
  --border: #52585e;
  --glow: rgba(232,234,237,0.08);
  --particle: rgba(180,190,200,0.5);
  --hud-bg: rgba(58,61,66,0.92);
  --btn-bg: #4a4e54;
  --btn-border: #8a909a;
  --tab-active: rgba(232,234,237,0.08);
  --shadow: rgba(0,0,0,0.4);
}

*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

body {
  background-color: var(--bg);
  color: var(--text);
  font-family: 'IM Fell English', serif;
  min-height: 100vh;
  transition: background-color 0.5s, color 0.5s;
  overflow-x: hidden;
}

/* ===================== PARTICLES ===================== */
#particle-canvas {
  position: fixed; top: 0; left: 0;
  width: 100%; height: 100%;
  pointer-events: none; z-index: 0;
}

/* ===================== INTERACTIVE ASCII CAT ===================== */
#ascii-cat {
  position: fixed;
  top: 0; left: 0;
  font-family: monospace;
  font-size: 20px;
  color: var(--text);
  white-space: pre;
  pointer-events: auto;
  z-index: 150;
  cursor: pointer;
  transition: color 0.3s;
  text-shadow: 0 0 10px var(--glow);
  user-select: none;
}

/* ===================== MAIN SITE NAVIGATION ===================== */
#main-nav {
  position: relative;
  z-index: 100;
  display: flex;
  justify-content: center;
  gap: 20px;
  padding: 40px 20px 20px;
  flex-wrap: wrap;
  border-bottom: 1px solid var(--border);
  background: linear-gradient(to bottom, var(--bg), transparent);
}
.nav-btn {
  background: transparent;
  border: none;
  color: var(--text-muted);
  font-family: 'Cinzel', serif;
  font-size: 14px;
  letter-spacing: 0.15em;
  padding: 10px 20px;
  cursor: pointer;
  transition: all 0.3s;
  border-bottom: 2px solid transparent;
}
.nav-btn.active, .nav-btn:hover {
  color: var(--text);
  border-bottom-color: var(--btn-border);
  text-shadow: 0 0 8px var(--glow);
}

/* ===================== THEME TOGGLE ===================== */
#theme-toggle {
  position: absolute; top: 18px; right: 22px;
  z-index: 101;
  display: flex; align-items: center; gap: 8px;
}
.theme-btn {
  background: var(--btn-bg);
  border: 1px solid var(--border);
  color: var(--text-soft);
  font-family: 'Cinzel', serif;
  font-size: 10px;
  letter-spacing: 0.07em;
  padding: 5px 11px;
  cursor: pointer;
  transition: all 0.3s;
  border-radius: 3px;
}
.theme-btn.active {
  border-color: var(--btn-border);
  color: var(--text);
  background: var(--tab-active);
  box-shadow: 0 0 10px var(--glow);
}
.theme-btn:hover { border-color: var(--btn-border); color: var(--text); }

/* ===================== MAIN SECTIONS ===================== */
#app { position: relative; z-index: 2; padding: 40px 20px; max-width: 1000px; margin: 0 auto; }
.site-section { display: none; animation: fadeSlide 0.6s ease both; }
.site-section.active { display: block; }

/* --- LANDING PAGE --- */
.landing-container { text-align: center; padding: 20px 10px 40px; max-width: 1100px; margin: 0 auto; }
.landing-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap: 25px; margin-top: 40px; }
.landing-card {
  background: var(--bg2);
  border: 1px solid var(--border);
  padding: 40px 25px;
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.4s cubic-bezier(0.25, 1, 0.5, 1);
  text-align: center;
  position: relative;
  overflow: hidden;
  box-shadow: 0 4px 20px var(--shadow);
}
.landing-card::before {
  content: ''; position: absolute; inset: 0;
  background: linear-gradient(to bottom, transparent, var(--glow));
  opacity: 0; transition: opacity 0.4s;
}
.landing-card:hover::before { opacity: 1; }
.landing-card:hover {
  border-color: var(--btn-border);
  box-shadow: 0 6px 26px var(--glow);
  transform: translateY(-6px);
}
.landing-card .card-icon { font-size: 38px; margin-bottom: 16px; transition: transform 0.3s; }
.landing-card:hover .card-icon { transform: scale(1.15); }
.landing-card h3 { font-family: 'Cinzel', serif; color: var(--text); margin-bottom: 12px; font-size: 20px; letter-spacing: 0.05em; }
.landing-card p { font-size: 14px; color: var(--text-soft); line-height: 1.6; }
.landing-card .card-rune { font-family: monospace; font-size: 13px; color: var(--text-muted); margin-top: 18px; letter-spacing: 0.2em; opacity: 0.6; transition: color 0.3s; }
.landing-card:hover .card-rune { color: var(--text); opacity: 1; }

/* --- PORTFOLIO --- */
.portfolio-container { text-align: center; padding-top: 60px; position: relative; }
.massive-art-text {
  font-family: 'Cinzel Decorative', serif;
  font-size: clamp(40px, 10vw, 120px);
  color: var(--text);
  cursor: pointer;
  text-shadow: 0 0 40px var(--glow), 0 2px 8px var(--shadow);
  transition: all 0.3s;
  display: inline-block;
  position: relative;
  z-index: 10;
}
.massive-art-text:hover { transform: scale(1.05); text-shadow: 0 0 60px var(--particle); }
.portfolio-desc {
  font-size: clamp(16px, 2vw, 18px);
  line-height: 1.8;
  color: var(--text-soft);
  max-width: 800px;
  margin: 40px auto;
  transition: opacity 0.5s;
}
#portfolio-subsections {
  display: none; 
  flex-wrap: wrap; 
  justify-content: center; 
  gap: 30px; 
  margin-top: 60px;
}
.art-card {
  background: var(--bg2);
  border: 1px solid var(--border);
  padding: 40px;
  border-radius: 8px;
  width: 45%;
  min-width: 300px;
  cursor: pointer;
  transition: all 0.3s;
  text-align: center;
}
.art-card:hover {
  border-color: var(--btn-border);
  box-shadow: 0 4px 24px var(--glow);
  transform: translateY(-5px);
}
.art-card h3 { font-family: 'Cinzel', serif; margin-bottom: 10px; font-size: 24px; }

/* Burst Particle Canvas */
#burst-canvas { position: absolute; top: 0; left: 0; width: 100%; height: 100%; pointer-events: none; z-index: 20; }

/* --- BLOGS --- */
.blog-post {
  background: var(--bg2);
  border: 1px solid var(--border);
  padding: 30px;
  border-radius: 8px;
  margin-bottom: 30px;
  transition: all 0.3s;
}
.blog-title {
  font-family: 'Cinzel Decorative', serif;
  font-size: 24px;
  color: var(--text);
  margin-bottom: 15px;
}
.blog-content { color: var(--text-muted); font-style: italic; }

/* --- GAME DEV & AUTHOR --- */
.dev-notes-btn {
  background: var(--bg3);
  border: 1px dashed var(--btn-border);
  color: var(--text);
  font-family: 'Cinzel', serif;
  padding: 10px 20px;
  cursor: pointer;
  margin-bottom: 30px;
  border-radius: 4px;
  display: block;
  width: fit-content;
  margin-left: auto; margin-right: auto;
  transition: all 0.3s;
}
.dev-notes-btn:hover { background: var(--tab-active); box-shadow: 0 0 15px var(--glow); }

#dev-notes-area {
  display: none;
  background: var(--bg2);
  border: 1px solid var(--border);
  padding: 20px;
  margin-bottom: 30px;
  border-radius: 8px;
}

.author-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 20px;
  margin-top: 40px;
}
.author-card {
  background: var(--bg2);
  border: 1px solid var(--border);
  padding: 30px;
  border-radius: 8px;
  text-align: center;
}
.author-card h3 { font-family: 'Cinzel', serif; color: var(--text); margin-bottom: 15px; }

/* ===================== ORIGINAL GAME CSS INCLUSIONS ===================== */
.title-ornament { font-family: 'Cinzel Decorative', serif; font-size: clamp(10px, 2vw, 16px); letter-spacing: 0.4em; color: var(--accent1); margin-bottom: 12px; animation: fadeSlide 1.2s ease both; text-align:center;}
.game-title { font-family: 'Cinzel Decorative', serif; font-size: clamp(36px, 8vw, 88px); color: var(--text); line-height: 1.1; text-shadow: 0 0 40px var(--glow), 0 2px 8px var(--shadow); animation: fadeSlide 1.4s ease both; animation-delay: 0.2s; text-align:center;}
.game-subtitle { font-family: 'Cinzel', serif; font-size: clamp(12px, 2.5vw, 18px); color: var(--text-soft); letter-spacing: 0.25em; margin-top: 14px; animation: fadeSlide 1.4s ease both; animation-delay: 0.4s; text-align:center;}
.divider { display: flex; align-items: center; gap: 16px; width: 100%; max-width: 500px; margin: 28px auto; animation: fadeSlide 1.4s ease both; animation-delay: 0.5s; }
.divider-line { flex: 1; height: 1px; background: var(--border); }
.divider-gem { font-size: 18px; color: var(--text-muted); }
#hud { position: fixed; bottom: 0; left: 0; right: 0; background: var(--hud-bg); border-top: 1px solid var(--border); z-index: 90; backdrop-filter: blur(12px); box-shadow: 0 -4px 28px var(--shadow); font-family: 'Cinzel', serif; transition: all 0.5s; display: none; padding: 0 24px; }
#hud.visible { display: flex; align-items: center; }
.hud-inner { display: flex; align-items: center; width: 100%; height: 52px; gap: 0; }
.hud-player-name { font-family: 'Cinzel Decorative', serif; font-size: 11px; color: var(--text); letter-spacing: 0.12em; white-space: nowrap; padding-right: 18px; border-right: 1px solid var(--border); margin-right: 18px; flex-shrink: 0; }
.hud-stat { display: flex; flex-direction: column; align-items: center; gap: 1px; flex-shrink: 0; padding: 0 10px; border-right: 1px solid var(--border); }
.hud-stat:last-child { border-right: none; }
.hud-stat .lbl { font-size: 8px; letter-spacing: 0.18em; color: var(--text-muted); line-height: 1; }
.hud-stat .val { font-size: 14px; color: var(--text); line-height: 1; font-weight: 600; }
.hud-hp .lbl { color: #b05050; }
.hud-hp .val { color: #e06060; }
.hud-weapon { margin-left: auto; font-size: 9px; letter-spacing: 0.18em; color: var(--text-muted); font-family: 'Cinzel', serif; white-space: nowrap; padding-left: 14px; border-left: 1px solid var(--border); flex-shrink: 0; }
.hud-weapon span { color: var(--text-soft); }
.name-section { animation: fadeSlide 1.6s ease both; animation-delay: 0.6s; width: 100%; max-width: 420px; margin: 0 auto; text-align:center;}
.name-label { font-family: 'Cinzel', serif; font-size: 11px; letter-spacing: 0.2em; color: var(--text-muted); margin-bottom: 6px; display: block; text-align: left; }
.name-hint { font-family: 'IM Fell English', serif; font-size: 12px; font-style: italic; color: var(--text-muted); margin-bottom: 18px; text-align: center; }
.name-row { display: flex; gap: 10px; margin-bottom: 10px; }
.name-input { flex: 1; background: var(--bg2); border: 1px solid var(--border); border-radius: 4px; color: var(--text); font-family: 'IM Fell English', serif; font-size: 15px; padding: 10px 14px; outline: none; transition: border-color 0.3s, box-shadow 0.3s; }
.name-input::placeholder { color: var(--text-muted); font-style: italic; }
.name-input:focus { border-color: var(--btn-border); box-shadow: 0 0 12px var(--glow); }
.name-group { display: flex; flex-direction: column; flex: 1; }
.begin-btn { margin-top: 24px; padding: 16px 40px; font-family: 'Cinzel Decorative', serif; font-size: 15px; letter-spacing: 0.12em; color: var(--text); background: var(--btn-bg); border: 2px solid var(--btn-border); border-radius: 6px; cursor: pointer; position: relative; overflow: hidden; transition: all 0.35s; box-shadow: 0 2px 18px var(--glow), inset 0 1px 0 rgba(255,255,255,0.07); animation: fadeSlide 1.6s ease both; animation-delay: 0.8s; width: 100%; }
.begin-btn::before { content: ''; position: absolute; inset: 0; background: radial-gradient(ellipse at center, var(--glow) 0%, transparent 70%); opacity: 0; transition: opacity 0.3s; }
.begin-btn:hover::before { opacity: 1; }
.begin-btn:hover { box-shadow: 0 4px 30px var(--glow), 0 0 0 1px var(--btn-border); transform: translateY(-1px); }
.begin-btn:active { transform: translateY(0); }
.btn-runes { display: flex; justify-content: center; gap: 8px; font-size: 13px; margin-top: 5px; color: var(--text-muted); }

/* Campaign UI */
.game-screen { display: none; }
.game-screen.visible { display: block; animation: fadeSlide 0.5s ease both; }
.tabs { display: flex; gap: 0; border-bottom: 1px solid var(--border); max-width: 900px; margin: 0 auto 36px; }
.tab-btn { font-family: 'Cinzel', serif; font-size: 12px; letter-spacing: 0.18em; color: var(--text-muted); background: transparent; border: none; padding: 12px 28px; cursor: pointer; border-bottom: 2px solid transparent; transition: all 0.3s; position: relative; }
.tab-btn:hover, .tab-btn.active { color: var(--text); border-bottom-color: var(--btn-border); background: var(--tab-active); }
.tab-panel { display: none; max-width: 900px; margin: 0 auto; }
.tab-panel.active { display: block; }
.act-header { font-family: 'Cinzel Decorative', serif; font-size: 22px; color: var(--text); margin-bottom: 10px; text-align: center; }
.act-list { display: flex; flex-direction: column; gap: 16px; margin-top: 20px; }
.act-card { background: var(--bg2); border: 1px solid var(--border); border-radius: 8px; padding: 20px 24px; cursor: pointer; transition: all 0.3s; position: relative; overflow: hidden; text-align: left; }
.act-card:hover { border-color: var(--btn-border); box-shadow: 0 4px 24px var(--glow); transform: translateX(4px); }
.act-card-title { font-family: 'Cinzel', serif; font-size: 16px; color: var(--text); margin-bottom: 6px; }
.act-card-sub { font-size: 13px; font-style: italic; color: var(--text-muted); }
.progress-bar-wrap { margin-top: 12px; background: var(--bg3); border-radius: 20px; height: 6px; border: 1px solid var(--border); overflow: hidden; }
.progress-bar-fill { height: 100%; background: linear-gradient(90deg, var(--accent1), var(--accent2)); border-radius: 20px; width: 0%; transition: width 1s ease; }
.back-btn { background: transparent; border: 1px solid var(--border); color: var(--text-muted); font-family: 'Cinzel', serif; font-size: 11px; letter-spacing: 0.15em; padding: 7px 16px; cursor: pointer; border-radius: 3px; margin-bottom: 30px; transition: all 0.3s; }
.back-btn:hover { border-color: var(--btn-border); color: var(--text); }

/* Art and Story */
.art-placeholder { width: 100%; background: var(--bg2); border: 1px dashed var(--border); border-radius: 8px; display: flex; align-items: center; justify-content: center; flex-direction: column; gap: 10px; color: var(--text-muted); font-family: 'Cinzel', serif; font-size: 12px; letter-spacing: 0.15em; margin: 24px 0; padding: 50px 20px; position: relative; overflow: hidden; }
.art-placeholder-icon { font-size: 32px; opacity: 0.4; }
.art-tall { min-height: 220px; }
.art-medium { min-height: 160px; }
.story-para { font-size: clamp(15px, 2.2vw, 17px); line-height: 1.85; color: var(--text-soft); margin: 20px 0; transition: color 0.5s; text-align: left; }
.story-para em { color: var(--text); font-style: italic; }
.player-name-inline { color: var(--text); font-style: normal; font-weight: bold; font-family: 'Cinzel', serif; font-size: 0.95em; }

/* Banners & Zones */
.knights-banner { position: relative; text-align: center; margin: 36px 0; padding: 28px 20px; }
.knights-banner-bg { position: absolute; inset: 0; background: linear-gradient(135deg, var(--bg3) 0%, var(--bg2) 50%, var(--bg3) 100%); border: 1px solid var(--border); border-radius: 6px; z-index: 0; }
.knights-glyphs { position: absolute; inset: 0; display: flex; align-items: center; justify-content: space-between; padding: 0 14px; font-size: 22px; color: var(--text-muted); opacity: 0.4; z-index: 1; pointer-events: none; flex-wrap: wrap; gap: 4px; }
.knights-title { position: relative; z-index: 2; font-family: 'Cinzel Decorative', serif; font-size: clamp(20px, 4vw, 34px); color: var(--text); text-shadow: 0 0 30px var(--glow); cursor: default; transition: all 0.4s; display: inline-block; letter-spacing: 0.08em; }
.knights-title:hover { text-shadow: 0 0 60px var(--particle), 0 0 20px rgba(180,80,80,0.6); color: #e8c060; animation: knightsPulse 0.5s ease infinite alternate; }
.knights-magic { position: absolute; inset: 0; z-index: 1; pointer-events: none; opacity: 0; transition: opacity 0.3s; }
.knights-banner:hover .knights-magic { opacity: 1; }
@keyframes knightsPulse { from { transform: scale(1); } to { transform: scale(1.03); text-shadow: 0 0 80px var(--particle), 0 0 30px rgba(220,60,60,0.7); } }
.knights-sub { position: relative; z-index: 2; font-family: 'Cinzel', serif; font-size: 11px; letter-spacing: 0.3em; color: var(--text-muted); margin-top: 8px; }
.mood-label { font-family: 'Cinzel', serif; font-size: 9px; letter-spacing: 0.3em; color: var(--accent1); text-align: center; margin: 8px 0 2px; opacity: 0.6; }
.cozy-icon { font-size: 22px; opacity: 0.35; display: inline-block; margin: 0 4px; animation: breathe 4s ease-in-out infinite; }
@keyframes breathe { 0%, 100% { transform: scale(1); opacity: 0.35; } 50% { transform: scale(1.1); opacity: 0.55; } }
.sep { text-align: center; color: var(--text-muted); font-size: 18px; margin: 20px 0; letter-spacing: 0.3em; opacity: 0.5; }

/* Choices & Dice */
.choice-section { background: var(--bg2); border: 1px solid var(--border); border-radius: 8px; padding: 24px; margin: 28px 0; }
.choice-prompt { font-family: 'Cinzel', serif; font-size: 13px; letter-spacing: 0.15em; color: var(--text-muted); margin-bottom: 16px; text-align: center; }
.choice-btn { display: block; width: 100%; background: var(--bg3); border: 1px solid var(--border); border-radius: 5px; color: var(--text-soft); font-family: 'IM Fell English', serif; font-size: 15px; padding: 14px 18px; text-align: left; cursor: pointer; margin: 8px 0; transition: all 0.3s; position: relative; }
.choice-btn:hover { border-color: var(--btn-border); color: var(--text); box-shadow: 0 2px 14px var(--glow); transform: translateX(5px); }
.choice-dc { font-family: 'Cinzel', serif; font-size: 10px; color: var(--text-muted); display: block; margin-top: 4px; }
#outcome-section { display: none; margin-top: 28px; }
#outcome-section.visible { display: block; }
.outcome-text { font-size: clamp(15px, 2.2vw, 17px); line-height: 1.85; color: var(--text-soft); margin: 16px 0; padding: 20px; background: var(--bg2); border-left: 3px solid var(--accent2); border-radius: 0 6px 6px 0; animation: fadeSlide 0.8s ease both; text-align:left;}
.dice-roll-wrap { text-align: center; margin: 14px 0; }
.dice-display { display: inline-block; font-family: 'Cinzel Decorative', serif; font-size: 48px; color: var(--text); width: 90px; height: 90px; line-height: 90px; border: 2px solid var(--btn-border); border-radius: 12px; background: var(--bg3); box-shadow: 0 0 20px var(--glow); animation: diceSpin 0.6s ease; text-align:center;}
@keyframes diceSpin { 0% { transform: rotate(-15deg) scale(0.8); opacity: 0; } 60% { transform: rotate(5deg) scale(1.05); } 100% { transform: rotate(0deg) scale(1); opacity: 1; } }
.roll-result { font-family: 'Cinzel', serif; font-size: 13px; margin-top: 10px; color: var(--text-muted); letter-spacing: 0.15em; text-align:center;}
.roll-success { color: #70b870; }
.roll-fail { color: #c06060; }

/* Particles within game text */
.ember { position: absolute; width: 4px; height: 4px; background: radial-gradient(circle, #e07030, transparent); border-radius: 50%; pointer-events: none; animation: floatEmber var(--dur, 4s) ease-in-out infinite; opacity: 0; }
@keyframes floatEmber { 0% { transform: translateY(0) translateX(0); opacity: 0; } 20% { opacity: 0.8; } 80% { opacity: 0.4; } 100% { transform: translateY(-120px) translateX(var(--dx, 30px)); opacity: 0; } }
.war-particle { position: absolute; border-radius: 50%; pointer-events: none; animation: floatWar var(--dur, 5s) ease-in-out infinite; opacity: 0; }
@keyframes floatWar { 0% { transform: translateY(0) translateX(0) rotate(0deg); opacity: 0; } 25% { opacity: 0.7; } 75% { opacity: 0.3; } 100% { transform: translateY(-100px) translateX(var(--dx, 20px)) rotate(360deg); opacity: 0; } }

/* Global animations */
@keyframes fadeSlide { from { opacity: 0; transform: translateY(16px); } to { opacity: 1; transform: translateY(0); } }

::-webkit-scrollbar { width: 6px; }
::-webkit-scrollbar-track { background: var(--bg2); }
::-webkit-scrollbar-thumb { background: var(--border); border-radius: 3px; }

/* ===================== RESPONSIVE STYLES ===================== */
@media (max-width: 768px) {
  #main-nav { padding: 60px 10px 10px; gap: 10px; }
  .nav-btn { font-size: 12px; padding: 8px 10px; }
  #theme-toggle { top: 10px; right: 10px; flex-wrap: wrap; justify-content: flex-end; }
  .theme-btn { font-size: 9px; padding: 4px 8px; }
  .landing-card { padding: 25px 15px; }
  .art-card { width: 100%; min-width: 0; }
  .massive-art-text { font-size: 40px; }
  
  /* Responsive HUD */
  #hud { padding: 0 10px; }
  #hud.visible { height: auto; padding-bottom: 10px; }
  .hud-inner { flex-wrap: wrap; height: auto; gap: 5px; justify-content: center; padding-top: 10px; }
  .hud-player-name { border-right: none; width: 100%; text-align: center; margin: 0; padding: 0; margin-bottom: 5px; }
  .hud-weapon { border-left: none; width: 100%; text-align: center; margin: 5px 0 0 0; padding: 0; }
  
  .name-row { flex-direction: column; }
  .choice-btn { font-size: 14px; padding: 12px 14px; }
  .game-title { font-size: 32px !important; }
}
</style>
</head>
<body>

<canvas id="particle-canvas"></canvas>
<div id="ascii-cat"> /\_/\ <br>( o.o )<br> > ^ < </div>

<div id="theme-toggle">
  <button class="theme-btn active" onclick="setTheme('dark', this)">Obsidian Ledger</button>
  <button class="theme-btn" onclick="setTheme('light', this)">Weathered Parchment</button>
  <button class="theme-btn" onclick="setTheme('neutral', this)">Slated Archive</button>
</div>

<nav id="main-nav">
  <button class="nav-btn active" onclick="goHome(this)">Home</button>
  <button class="nav-btn" onclick="switchMainSection('section-portfolio', this)">Portfolio</button>
  <button class="nav-btn" onclick="switchMainSection('section-blogs', this)">Blogs</button>
  <button class="nav-btn" onclick="switchMainSection('section-gamedev', this)">My Journey as a Game Dev</button>
  <button class="nav-btn" onclick="switchMainSection('section-author', this)">My Journey as an Author</button>
</nav>

<div id="app">

  <div id="section-landing" class="site-section active">
    <div class="landing-container">
      <div class="title-ornament" style="margin-top: 20px;">✦ Chronicles & Creations ✦</div>
      <h1 class="game-title" style="font-size: clamp(36px, 6vw, 64px); margin-bottom: 20px;">Anuraag Paul</h1>
      <div class="divider"><div class="divider-line"></div><div class="divider-gem">⸸</div><div class="divider-line"></div></div>
      
      <div class="landing-grid">
        <div class="landing-card" onclick="navigateToSection('section-portfolio', 1)">
          <div class="card-icon">🎨</div>
          <h3>Portfolio</h3>
          <p>Immerse yourself in concept art, atmospheric world-building, and artistic visions inspired by legendary universes.</p>
          <div class="card-rune">ᚠ  ᛟ  ᚱ</div>
        </div>
        <div class="landing-card" onclick="navigateToSection('section-blogs', 2)">
          <div class="card-icon">📜</div>
          <h3>Blogs</h3>
          <p>Explore philosophical musings, written reflections, and deep insights into art, style, and the creative spark.</p>
          <div class="card-rune">ᚢ  ᛞ  ᚹ</div>
        </div>
        <div class="landing-card" onclick="navigateToSection('section-gamedev', 3)">
          <div class="card-icon">⚔</div>
          <h3>Game Dev</h3>
          <p>Step directly into the Chronicles of the 13th Province, an interactive textual RPG saga of high-fantasy.</p>
          <div class="card-rune">ᚦ  ⚔  ᛗ</div>
        </div>
        <div class="landing-card" onclick="navigateToSection('section-author', 4)">
          <div class="card-icon">🖋</div>
          <h3>Author Journey</h3>
          <p>Delve into the comprehensive world archives, histories, mythos, maps, and novel developments of the realm.</p>
          <div class="card-rune">ᚨ  ᛒ  ᛉ</div>
        </div>
      </div>
    </div>
  </div>

  <div id="section-portfolio" class="site-section">
    <div class="portfolio-container">
      <h1 class="massive-art-text" id="i-love-art" onclick="explodePortfolioText()">I Love Art</h1>
      <canvas id="burst-canvas"></canvas>
      
      <p class="portfolio-desc" id="portfolio-desc">
        Art is one of my biggest passions. I grew up especially being inspired by some of the early 2000s concept artists and Matte painters for some of my favourite childhood franchises such as Star Wars, Game of Thrones, Lord of the rings and Harry Potter. Here I try my best to recreate that what inspired me, and make my own creation. A concept art is empty without a concept, a world where it can exist, so I am taking on this self project where I try my hands at world building and story telling all the while applying my skills to bring those worlds to life with my Concept art.
      </p>

      <div id="portfolio-subsections">
        <div class="art-card">
          <h3>The Escape</h3>
          <p class="name-hint">Explore the gallery...</p>
        </div>
        <div class="art-card">
          <h3>Fortress of Inquisition</h3>
          <p class="name-hint">Explore the gallery...</p>
        </div>
      </div>
    </div>
  </div>

  <div id="section-blogs" class="site-section">
    <div style="text-align:center; margin-bottom: 40px;">
      <div class="title-ornament">✦ Musings & Reflections ✦</div>
    </div>
    <div class="blog-post">
      <h2 class="blog-title">Why Ai art will never be real art, my Takeaway from Brandon Sanderson.</h2>
      <div class="divider"><div class="divider-line"></div><div class="divider-gem">⸸</div><div class="divider-line"></div></div>
      <p class="blog-content">Scrolls are currently empty. The scribe is still penning this thought...</p>
    </div>
  </div>

  <div id="section-gamedev" class="site-section">
    
    <button class="dev-notes-btn" onclick="toggleDevNotes()">📜 Open Dev Notes</button>
    <div id="dev-notes-area">
      <h3 style="font-family:'Cinzel Decorative',serif; margin-bottom:10px;">Developer's Ledger</h3>
      <p style="color:var(--text-soft); font-size:14px;">Updates and general process notes on Vael Morren will be inscribed here.</p>
    </div>

    <div id="hud">
      <div class="hud-inner">
        <div class="hud-player-name" id="hud-name">⸻</div>
        <div class="hud-stat hud-hp"><span class="lbl">HP</span><span class="val">30</span></div>
        <div class="hud-stat"><span class="lbl">STR</span><span class="val">2</span></div>
        <div class="hud-stat"><span class="lbl">DEX</span><span class="val">2</span></div>
        <div class="hud-stat"><span class="lbl">INT</span><span class="val">1</span></div>
        <div class="hud-stat"><span class="lbl">WIS</span><span class="val">0</span></div>
        <div class="hud-stat"><span class="lbl">CON</span><span class="val">3</span></div>
        <div class="hud-stat"><span class="lbl">CHA</span><span class="val">1</span></div>
        <div class="hud-weapon">⚔ WEAPON &nbsp;<span>None</span></div>
      </div>
    </div>

    <div id="screen-title" class="game-screen visible">
      <div class="title-ornament">✦ &nbsp; Chronicles of the 13th Province &nbsp; ✦</div>
      <div class="game-title">Vael Morren</div>
      <div class="game-subtitle">A Tale of Empire, Rebellion &amp; Aether</div>
      <div class="divider"><div class="divider-line"></div><div class="divider-gem">⸸</div><div class="divider-line"></div></div>

      <div class="name-section">
        <p class="name-hint" style="margin-bottom:18px;"><em>Before your tale begins, speak your name into the wind — a true name, not a title given by others.</em></p>
        <div class="name-row">
          <div class="name-group">
            <label class="name-label">✦ FIRST NAME</label>
            <input class="name-input" id="inp-first" type="text" placeholder="e.g. Aldric, Mira..." maxlength="24" oninput="updateNamePreview()">
          </div>
          <div class="name-group">
            <label class="name-label">✦ FAMILY NAME</label>
            <input class="name-input" id="inp-last" type="text" placeholder="e.g. Voss, Crane..." maxlength="24" oninput="updateNamePreview()">
          </div>
        </div>
        <div id="name-preview" class="name-hint" style="margin-top:4px; min-height:20px;"></div>
        <button class="begin-btn" onclick="beginCampaign()">
          ⸻ Begin Your Campaign ⸻
          <div class="btn-runes">ᚠ &nbsp; ᚢ &nbsp; ᚦ &nbsp; ᚨ &nbsp; ᚱ</div>
        </button>
      </div>
    </div>

    <div id="screen-campaign" class="game-screen">
      <div style="text-align:center; margin-bottom: 32px;">
        <div class="title-ornament">✦ Campaign of <span id="camp-player-name" style="color:var(--text);">—</span> ✦</div>
      </div>
      <div class="tabs">
        <button class="tab-btn active" onclick="switchGameTab('your-campaign', this)">Your Campaign</button>
        <button class="tab-btn" onclick="switchGameTab('summary', this)">Campaign Summary</button>
      </div>
      <div id="tab-your-campaign" class="tab-panel active">
        <div class="act-header">The Chronicle Awaits</div>
        <p style="text-align:center; font-style:italic; color:var(--text-muted); font-size:14px; margin-bottom:8px;">Choose an Act to begin your journey</p>
        <div class="act-list">
          <div class="act-card" onclick="goToAct1()">
            <div class="act-card-title">⚔ Act I — The Weight of Chains</div>
            <div class="act-card-sub">The God Emperor's 13th Province. An Academy. A Choice.</div>
            <div class="progress-bar-wrap"><div class="progress-bar-fill" id="act1-progress" style="width:0%"></div></div>
          </div>
          <div class="act-card" style="opacity:0.4; cursor:not-allowed;" title="Locked">
            <div class="act-card-title" style="color:var(--text-muted);">⸸ Act II — Shadows of Nihon-Ja <span style="font-size:11px; margin-left:8px;">[LOCKED]</span></div>
            <div class="act-card-sub">Coming soon…</div>
            <div class="progress-bar-wrap"><div class="progress-bar-fill" style="width:0%"></div></div>
          </div>
        </div>
      </div>
      <div id="tab-summary" class="tab-panel">
        <div style="text-align:center; padding:60px 20px; color:var(--text-muted); font-style:italic; font-size:16px;">
          Your campaign summary will be inscribed here as your story unfolds…
        </div>
      </div>
    </div>

    <div id="screen-act1" class="game-screen" style="max-width:780px; margin:0 auto;">
      <button class="back-btn" onclick="backToCampaign()">← Return to Campaign</button>
      <div style="text-align:center; margin-bottom: 36px;">
        <div class="title-ornament">Act I</div>
        <div class="act-card-title" style="font-family:'Cinzel Decorative',serif; font-size:26px; margin-bottom:6px;">The Weight of Chains</div>
        <div class="progress-bar-wrap" style="max-width:400px; margin:14px auto;">
          <div class="progress-bar-fill" id="act1-progress2" style="width:0%"></div>
        </div>
      </div>

      <div class="art-placeholder art-tall" style="margin-bottom:28px;">
        <div class="art-placeholder-icon">🎨</div>
        <div>[ Artwork Placeholder ]</div>
        <div style="font-size:10px; margin-top:4px; font-style:italic; color:var(--text-muted);">Your illustration of the young soldier here</div>
      </div>

      <p class="story-para">You look at your hands, calloused with training. They look far beyond the hands of a seventeen year old. It has been 5 years since you joined the Military Academy in District 2 following the annexation of your country. It wasn't the largest country in the world, so it didn't take long for the God Emperor to bring it to its knees — yet small enough for the Emperor to not consider it a true threat.</p>
      <p class="story-para">Your nation was the last one to become a part of the God Emperor's vast Kingdom. Your country became its <em>13th Province</em>. And like every province in the Empire, it was divided into 12 districts. Children from all districts, at the ripe age of 11, were recruited into an academy in District 2 — taught and trained to be a part of the military from a very young age.</p>

      <div class="art-placeholder art-tall">
        <div class="art-placeholder-icon">⚔</div>
        <div>[ Artwork Placeholder ]</div>
        <div style="font-size:10px; margin-top:4px; font-style:italic; color:var(--text-muted);">Your badass legion of soldiers illustration here</div>
      </div>

      <div class="zone-tense" id="zone-tense" style="position:relative; padding: 10px 0;">
        <div class="mood-label">⸻ ⚔ TENSION ⚔ ⸻</div>
        <p class="story-para">Next year you will have to take a test that will evaluate all your capabilities and determine if you are fit to be a part of the Royal Army — which carries a reputation to be the finest in the entire world. Neither the <em>Shadows from Nihon-Ja</em>, nor the <em>Berserkers of Slavia</em> could match the full might of the God Emperor's legions of trained soldiers, led by the most lethal Squadrons of Aetherbounds known as the…</p>
        <div class="knights-banner" id="knights-banner">
          <div class="knights-banner-bg"></div>
          <div class="knights-glyphs" aria-hidden="true">⸸ ᛞ ⚔ ᚠ 🗡 ᛟ ✦ ᚹ ⸸ ᛞ ⚔ ᚠ 🗡 ᛟ ✦ ᚹ ⸸ ᛞ ⚔ ᚠ 🗡 ᛟ ✦ ᚹ ⸸ ᛞ ⚔ ᚠ 🗡 ᛟ ✦ ᚹ</div>
          <div class="knights-title">Knights of Inquisition</div>
          <div class="knights-sub">⸻ Hover to Invoke the Aether ⸻</div>
        </div>
        <p class="story-para">You will also be tested for your affinity to Aether. If found positive, you will be initiated into the Knights as a Squire and trained into a <em>living, walking, breathing weapon.</em></p>
        <div class="sep">· · · ⸸ · · ·</div>
        <p class="story-para" style="text-align:center; font-style:italic;">"You shake these thoughts out of your mind…"</p>
      </div>

      <div class="zone-cozy" id="zone-cozy" style="position:relative; padding: 10px 0;">
        <div class="mood-label">⸻ 🍂 WARMTH 🍂 ⸻</div>
        <div style="text-align:center; font-size: 26px; margin: 10px 0;">
          <span class="cozy-icon">🍁</span><span class="cozy-icon">🕯</span><span class="cozy-icon">🍂</span><span class="cozy-icon">☕</span><span class="cozy-icon">🌿</span>
        </div>
        <p class="story-para">All that may or may not happen… Besides, it's not all as bad as it sounds. Sure, the academy is strict — but it's also <em>fun.</em> You have made so many friends here. And you are all well taken care of. Your village was a very remote settlement, so things could get rough sometimes. But here you are well fed, well sheltered, and you have a <em>purpose.</em></p>
        <p class="story-para">You have heard the tyrannical rumours about the God King — but the perks of being such a distant province are that his grip is lighter around here. You can get away with many things you wouldn't dare attempt in, say, the <em>3rd Province…</em></p>
        <p class="story-para" style="text-align:center; font-style:italic; font-size: 20px; color: var(--text);">"Life is good."</p>
      </div>

      <div class="zone-tavern" id="zone-tavern" style="position:relative; padding: 10px 0;">
        <div class="mood-label">⸻ 🍺 THE FLASK & SWORD ⸻</div>
        <div style="text-align:center; font-size: 24px; margin: 10px 0;">
          <span class="cozy-icon">🍺</span><span class="cozy-icon">🕯</span><span class="cozy-icon">🔥</span><span class="cozy-icon">📜</span><span class="cozy-icon">🍺</span>
        </div>
        <p class="story-para">You look up and see Jacob walking towards you. <em>"Heyy <span class="player-name-first">—</span>, I want to tell you something important… come."</em></p>
        <p class="story-para">You walk away from the academy to a local tavern — <em>The Flask and the Sword.</em> It's one of the few places where imperial soldiers don't frequent, where the citizens can have a truly safe place to discuss… <em>things.</em></p>
        <p class="story-para" style="font-style:italic; text-align:center;">"Is this about the… Rebellion?"</p>
        <div class="art-placeholder art-medium">
          <div class="art-placeholder-icon">🍺</div>
          <div>[ Artwork Placeholder ]</div>
        </div>
        <p class="story-para">Jacob's face darkened. You guessed it right. You feel a conflict brewing inside of you. Life was <em>smooth.</em> Jacob was a few years senior to you. He had lost his family during the annexation. He took his aptitude test at 18 and couldn't get into the military — instead finding work as a tutor of history in the Academy at District 2. If anyone would care about a rebellion, it would be a history teacher who had <em>lost everything</em> to the Empire.</p>
        <p class="story-para" style="font-style:italic; text-align:center; font-size:18px; color:var(--text);">"You have to make a choice, <span class="player-name-first">—</span>… Between what is right and what is easy."</p>
      </div>

      <div class="zone-war" id="zone-war" style="position:relative; padding: 10px 0;">
        <div class="mood-label" style="color: #c04040;">⸻ ⚔ CHOOSE YOUR PATH ⚔ ⸻</div>
        <div class="choice-section" id="choice-section">
          <div class="choice-prompt">◈ A CHOICE STANDS BEFORE YOU ◈</div>
          <button class="choice-btn" onclick="makeChoice(1)">
            <strong>Persuade Jacob — urge him to stand down.</strong>
            <span class="choice-dc">Charisma check — DC 8 (your CHA: +1 modifier)</span>
          </button>
          <button class="choice-btn" onclick="makeChoice(2)">
            <strong>Agree with Jacob. Stand beside him.</strong>
            <span class="choice-dc">No check required — this path is chosen freely.</span>
          </button>
        </div>
        <div id="dice-section" style="display:none; text-align:center; margin: 20px 0;">
          <div class="roll-result" id="roll-flavor" style="margin-bottom:12px;">Rolling your Charisma check…</div>
          <div class="dice-display" id="dice-num">?</div>
          <div class="roll-result" id="roll-verdict"></div>
        </div>
        <div id="outcome-section">
          <div id="outcome-mood-label" class="mood-label"></div>
          <div class="outcome-text" id="outcome-text"></div>
        </div>
      </div>
    </div>
  </div>

  <div id="section-author" class="site-section">
    <div style="text-align:center; margin-bottom: 40px;">
      <div class="title-ornament">✦ The Written Realms ✦</div>
    </div>
    
    <div class="author-grid">
      <div class="author-card">
        <h3>World Building</h3>
        <p class="name-hint">Lore, maps, and histories of the 13th Province and beyond.</p>
      </div>
      <div class="author-card">
        <h3>Vael Morren Extended Universe</h3>
        <p class="name-hint">Short stories and mythos exploring the wider world.</p>
      </div>
      <div class="author-card">
        <h3>Novel 1 WIP</h3>
        <p class="name-hint">The main saga unfolding within Vael Morren.</p>
      </div>
    </div>
  </div>

</div>

<script>
// ============================================================
// MAIN SITE NAVIGATION
// ============================================================

function goHome(btn) {
  switchMainSection('section-landing', btn);
  resetPortfolio();
}

function resetPortfolio() {
  const textEl = document.getElementById('i-love-art');
  const descEl = document.getElementById('portfolio-desc');
  const sub = document.getElementById('portfolio-subsections');
  
  if(textEl) {
    textEl.style.display = 'inline-block';
    textEl.style.opacity = '1';
    textEl.style.pointerEvents = 'auto';
  }
  if(descEl) {
    descEl.style.display = 'block';
    setTimeout(() => descEl.style.opacity = '1', 10);
  }
  if(sub) {
    sub.style.display = 'none';
    sub.style.animation = '';
  }
}

function switchMainSection(id, btn) {
  document.querySelectorAll('.site-section').forEach(sec => sec.classList.remove('active'));
  document.querySelectorAll('.nav-btn').forEach(b => b.classList.remove('active'));
  document.getElementById(id).classList.add('active');
  if (btn) btn.classList.add('active');

  // Manage Game HUD visibility globally
  const hud = document.getElementById('hud');
  if(id === 'section-gamedev' && playerFirst !== '') {
    hud.classList.add('visible');
  } else {
    hud.classList.remove('visible');
  }
}

// LANDING GRID CARD REDIRECTION
function navigateToSection(id, btnIndex) {
  const btns = document.querySelectorAll('#main-nav .nav-btn');
  switchMainSection(id, btns[btnIndex]);
}

// ============================================================
// THEME
// ============================================================
function setTheme(mode, btn) {
  document.body.className = '';
  if (mode === 'light') document.body.classList.add('light');
  if (mode === 'neutral') document.body.classList.add('neutral');
  document.querySelectorAll('.theme-btn').forEach(b => b.classList.remove('active'));
  btn.classList.add('active');
  initParticles(); // Restart background particles with new color
}

// ============================================================
// INTERACTIVE ASCII CAT STATE MACHINE
// ============================================================
const cat = document.getElementById('ascii-cat');
let mouseX = window.innerWidth / 2;
let mouseY = window.innerHeight / 2;
let catX = window.innerWidth - 180;
let catY = window.innerHeight - 160;

const catFaces = {
  normal: " /\\_/\\ \n( o.o )\n > ^ < ",
  happy: " /\\_/\\ \n( ^.^ )\n > * < ",
  shocked: " /\\_/\\ \n( O.O )\n > 0 < ",
  sleeping: " /\\_/\\ \n( -.- )\n > z Z ",
  blinking: " /\\_/\\ \n( o.- )\n > ^ < ",
  curious: " /\\_/\\ \n( ◉.◉ )\n > ▱ < "
};

let catState = 'sitting'; // 'sitting', 'following', 'chasing'
let stateCountdown = 200; 
let expressionCountdown = 120;
let currentFace = 'normal';

document.addEventListener('mousemove', (e) => {
  const speed = Math.abs(e.clientX - mouseX) + Math.abs(e.clientY - mouseY);
  mouseX = e.clientX;
  mouseY = e.clientY;

  if (catState !== 'chasing' && speed > 80) {
    currentFace = 'shocked';
    expressionCountdown = 40; 
  }
});

cat.addEventListener('mousedown', (e) => {
  e.stopPropagation();
  catState = 'chasing';
  stateCountdown = 450; // Chase around for approx 7.5 seconds
  currentFace = 'happy';
  expressionCountdown = 90;
});

function animateCat() {
  // State Transitions
  stateCountdown--;
  if (stateCountdown <= 0) {
    if (catState === 'sitting') {
      if (Math.random() < 0.4) {
        catState = 'following';
        stateCountdown = 300 + Math.random() * 150; // Tracking time
        currentFace = 'curious';
      } else {
        stateCountdown = 200 + Math.random() * 200; // Extend sit time
      }
    } else {
      catState = 'sitting';
      stateCountdown = 300 + Math.random() * 300;
      currentFace = 'normal';
    }
  }

  // Periodic Expression Modulation
  expressionCountdown--;
  if (expressionCountdown <= 0) {
    if (catState === 'sitting') {
      const choices = ['normal', 'sleeping', 'blinking', 'normal', 'curious'];
      currentFace = choices[Math.floor(Math.random() * choices.length)];
      expressionCountdown = 120 + Math.random() * 180;
    } else if (catState === 'following') {
      currentFace = Math.random() < 0.5 ? 'normal' : 'curious';
      expressionCountdown = 60 + Math.random() * 60;
    } else if (catState === 'chasing') {
      currentFace = Math.random() < 0.6 ? 'happy' : 'shocked';
      expressionCountdown = 30 + Math.random() * 40;
    }
  }

  // Eased Positional Interpolation with an 80px buffer offset
  const distX = mouseX - (catX + 40);
  const distY = mouseY - (catY + 40);
  const distance = Math.sqrt(distX * distX + distY * distY);
  
  let targetX = mouseX - 40;
  let targetY = mouseY - 40;

  if (distance < 80 && (catState === 'following' || catState === 'chasing')) {
      const angle = Math.atan2(distY, distX);
      targetX = mouseX - Math.cos(angle) * 80 - 40;
      targetY = mouseY - Math.sin(angle) * 80 - 40;
  }

  if (catState === 'following') {
    catX += (targetX - catX) * 0.02;
    catY += (targetY - catY) * 0.02;
  } else if (catState === 'chasing') {
    catX += (targetX - catX) * 0.09;
    catY += (targetY - catY) * 0.09;
  } else {
    // Idle soft float bobbing
    catY += Math.sin(Date.now() / 400) * 0.15;
  }

  // Boundaries restraint
  if (catX < 15) catX = 15;
  if (catY < 15) catY = 15;
  if (catX > window.innerWidth - 140) catX = window.innerWidth - 140;
  if (catY > window.innerHeight - 100) catY = window.innerHeight - 100;

  cat.innerHTML = catFaces[currentFace];
  cat.style.transform = `translate(${catX}px, ${catY}px)`;

  requestAnimationFrame(animateCat);
}
animateCat();

// ============================================================
// PORTFOLIO TEXT EXPLOSION
// ============================================================
function explodePortfolioText() {
  const textEl = document.getElementById('i-love-art');
  const descEl = document.getElementById('portfolio-desc');
  const canvas = document.getElementById('burst-canvas');
  const ctx = canvas.getContext('2d');
  
  // Set dimensions
  const rect = textEl.getBoundingClientRect();
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;

  // Hide text and desc
  textEl.style.opacity = '0';
  textEl.style.pointerEvents = 'none';
  descEl.style.opacity = '0';
  descEl.style.transition = 'opacity 0.5s';

  // Create burst particles
  let particlesList = [];
  const colors = ['#c9a84c', '#a8924a', '#ffffff', '#6b8e6e'];
  for(let i = 0; i < 80; i++) {
    particlesList.push({
      x: rect.left + rect.width / 2,
      y: rect.top + rect.height / 2,
      vx: (Math.random() - 0.5) * 20,
      vy: (Math.random() - 0.5) * 20,
      size: Math.random() * 4 + 1,
      color: colors[Math.floor(Math.random() * colors.length)],
      life: 1
    });
  }

  function renderBurst() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    let allDead = true;
    particlesList.forEach(p => {
      if(p.life <= 0) return;
      allDead = false;
      ctx.fillStyle = p.color;
      ctx.globalAlpha = p.life;
      ctx.beginPath();
      ctx.arc(p.x, p.y, p.size, 0, Math.PI * 2);
      ctx.fill();
      
      p.x += p.vx;
      p.y += p.vy;
      p.life -= 0.02; // fade out speed
    });

    if(!allDead) {
      requestAnimationFrame(renderBurst);
    } else {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      textEl.style.display = 'none';
      descEl.style.display = 'none';
      
      // Show subsections
      const sub = document.getElementById('portfolio-subsections');
      sub.style.display = 'flex';
      sub.style.animation = 'fadeSlide 1s ease both';
    }
  }
  renderBurst();
}

// ============================================================
// GAME DEV LOGIC
// ============================================================
function toggleDevNotes() {
  const area = document.getElementById('dev-notes-area');
  area.style.display = area.style.display === 'block' ? 'none' : 'block';
}

let playerFirst = '';
let playerLast = '';
let act1Progress = 0;

function updateNamePreview() {
  const f = document.getElementById('inp-first').value.trim();
  const l = document.getElementById('inp-last').value.trim();
  const prev = document.getElementById('name-preview');
  if (f || l) {
    prev.innerHTML = `<em>Your name shall be known as: <strong>${f || '…'} ${l || '…'}</strong></em>`;
  } else {
    prev.innerHTML = '';
  }
}

function beginCampaign() {
  const f = document.getElementById('inp-first').value.trim();
  const l = document.getElementById('inp-last').value.trim();
  if (!f || !l) {
    alert('Please enter both your first and family name before your campaign begins.');
    return;
  }
  playerFirst = f;
  playerLast = l;

  document.getElementById('camp-player-name').textContent = `${f} ${l}`;
  document.getElementById('hud-name').textContent = `${f} ${l}`;
  document.querySelectorAll('.player-name-first').forEach(el => el.textContent = playerFirst);

  crossfadeGameScreen('screen-title', 'screen-campaign');
  document.getElementById('hud').classList.add('visible');
  setTimeout(() => { document.getElementById('act1-progress').style.width = '2%'; }, 600);
}

function crossfadeGameScreen(fromId, toId) {
  const from = document.getElementById(fromId);
  const to = document.getElementById(toId);
  from.style.opacity = '0';
  setTimeout(() => {
    from.classList.remove('visible');
    to.classList.add('visible');
    to.style.opacity = '1';
  }, 300);
}

function switchGameTab(id, btn) {
  document.querySelectorAll('.tab-panel').forEach(p => p.classList.remove('active'));
  document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
  document.getElementById('tab-' + id).classList.add('active');
  btn.classList.add('active');
}

function goToAct1() {
  crossfadeGameScreen('screen-campaign', 'screen-act1');
  initEmbers('zone-tense', 12, 'spark');
  initEmbers('zone-war', 16, 'war');
  updateAct1Progress(5);
}

function backToCampaign() { crossfadeGameScreen('screen-act1', 'screen-campaign'); }
function updateAct1Progress(pct) {
  act1Progress = pct;
  document.getElementById('act1-progress').style.width = pct + '%';
  document.getElementById('act1-progress2').style.width = pct + '%';
}

function makeChoice(choice) {
  document.getElementById('choice-section').style.display = 'none';
  if (choice === 2) { playOutcome('A2'); return; }

  document.getElementById('dice-section').style.display = 'block';
  document.getElementById('roll-flavor').textContent = 'Rolling your Charisma check…';
  document.getElementById('roll-verdict').textContent = '';
  document.getElementById('dice-num').textContent = '?';

  let ticks = 0;
  const interval = setInterval(() => {
    document.getElementById('dice-num').textContent = Math.ceil(Math.random() * 20);
    ticks++;
    if (ticks >= 14) {
      clearInterval(interval);
      const roll = Math.ceil(Math.random() * 20);
      const total = roll + 1;
      document.getElementById('dice-num').textContent = roll;
      const success = total >= 8;
      const vEl = document.getElementById('roll-verdict');
      vEl.textContent = `Roll: ${roll} + 1 (CHA) = ${total} vs DC 8 — ${success ? 'SUCCESS' : 'FAILURE'}`;
      vEl.className = 'roll-result ' + (success ? 'roll-success' : 'roll-fail');
      setTimeout(() => playOutcome(success ? 'A1' : 'A2'), 1200);
    }
  }, 80);
}

function playOutcome(branch) {
  const el = document.getElementById('outcome-section');
  const txt = document.getElementById('outcome-text');
  const lbl = document.getElementById('outcome-mood-label');
  el.classList.add('visible');
  updateAct1Progress(100);

  if (branch === 'A1') {
    lbl.textContent = '⸻ ⚔ PATH A1: THE COST OF PEACE ⸻';
    lbl.style.color = '#c08040';
    txt.innerHTML = `
      <p style="margin-bottom:14px;"><em>"Jacob looks at you disappointedly…"</em></p>
      <p style="margin-bottom:14px;">Of course you would say this. You're privileged enough to have everything you want from life…</p>
      <p style="margin-bottom:14px;">He walks away. You don't turn back as he leaves the Tavern, leaving you alone with your own thoughts.</p>
      <p style="margin-bottom:14px;">Then — you hear a <strong>massive explosion</strong> outside.</p>
      <p>Ears ringing, you rush outside to see what happened. There is only a massive crater in front of you — and the severed body of what was unmistakably <strong>Jacob.</strong></p>
    `;
    addWarParticles('outcome-section', '#e07030', '#c04040');
  } else {
    lbl.textContent = '⸻ 💀 PATH A2: THE PRICE OF LOYALTY ⸻';
    lbl.style.color = '#c04040';
    txt.innerHTML = `
      <p style="margin-bottom:14px;"><em>"I knew you would come around — you are sensible,"</em> Jacob says, a rare warmth crossing his face.</p>
      <p style="margin-bottom:14px;">Then the tavern door swings open. A tall, cloaked figure steps inside.</p>
      <p style="margin-bottom:14px;">Before you can process anything — <em>something small and shiny streaks across the room.</em></p>
      <p style="margin-bottom:14px;">Warm red liquid splashes across your face. You taste metal. Jacob slumps motionless onto the table.</p>
      <p style="color: var(--text-muted); font-style:italic;">And the cloaked figure turns to look at you…</p>
    `;
    addWarParticles('outcome-section', '#c04040', '#800020');
  }
  el.scrollIntoView({ behavior: 'smooth', block: 'start' });
}

// ============================================================
// PARTICLE SYSTEMS (In-game Environment elements)
// ============================================================
function initEmbers(zoneId, count, type) {
  const zone = document.getElementById(zoneId);
  if (!zone) return;
  for (let i = 0; i < count; i++) {
    const e = document.createElement('div');
    if (type === 'war') {
      e.className = 'war-particle';
      const colors = ['#e04020', '#c04040', '#e07030', '#c08020'];
      e.style.cssText = `width:${3 + Math.random()*4}px; height:${3 + Math.random()*4}px; background:${colors[Math.floor(Math.random()*colors.length)]}; left:${Math.random()*100}%; bottom:${Math.random()*40}px; --dur:${3 + Math.random()*4}s; --dx:${(Math.random()-0.5)*60}px; animation-delay:${Math.random()*4}s;`;
    } else {
      e.className = 'ember';
      e.style.cssText = `left:${Math.random()*100}%; bottom:0; --dur:${3 + Math.random()*3}s; --dx:${(Math.random()-0.5)*50}px; animation-delay:${Math.random()*3}s;`;
    }
    zone.appendChild(e);
  }
}

function addWarParticles(containerId, c1, c2) {
  const el = document.getElementById(containerId);
  el.style.position = 'relative'; el.style.overflow = 'hidden';
  for (let i = 0; i < 20; i++) {
    const p = document.createElement('div');
    p.className = 'war-particle';
    p.style.cssText = `position:absolute; width:${2+Math.random()*5}px; height:${2+Math.random()*5}px; background:${Math.random()>0.5?c1:c2}; left:${Math.random()*100}%; bottom:0; --dur:${3+Math.random()*4}s; --dx:${(Math.random()-0.5)*80}px; animation-delay:${Math.random()*3}s;`;
    el.appendChild(p);
  }
}

// ============================================================
// GLOBAL HIGH-FANTASY BACKGROUND CANVAS ATMOSPHERE
// ============================================================
let particles = [];
let raf;
function initParticles() {
  cancelAnimationFrame(raf);
  particles = [];
  const canvas = document.getElementById('particle-canvas');
  if (!canvas) return;
  const ctx = canvas.getContext('2d');
  canvas.width = window.innerWidth; canvas.height = window.innerHeight;

  const isDark = !document.body.classList.contains('light') && !document.body.classList.contains('neutral');
  const isLight = document.body.classList.contains('light');
  const baseColor = isDark ? [201,168,76] : isLight ? [120,90,50] : [140,160,180];

  const runesList = ['ᚠ', 'ᚢ', 'ᚦ', 'ᚨ', 'ᚱ', 'ᛞ', 'ᛟ', 'ᚹ', 'ᛗ', 'ᛒ', 'ᛉ', 'ᚺ'];
  const particleTypes = ['dust', 'ember', 'leaf', 'petal', 'rune'];

  // Higher density ecosystem of environment particles
  for (let i = 0; i < 160; i++) {
    const type = particleTypes[Math.floor(Math.random() * particleTypes.length)];
    let p = {
      x: Math.random() * canvas.width,
      y: Math.random() * canvas.height,
      type: type,
      opacity: Math.random() * 0.45 + 0.15,
      size: Math.random() * 2.5 + 1,
      speedX: (Math.random() - 0.5) * 0.5,
      speedY: -Math.random() * 0.5 - 0.2,
      angle: Math.random() * Math.PI * 2,
      spin: (Math.random() - 0.5) * 0.025,
      baseColor: baseColor
    };

    if (type === 'ember') {
      p.color = isDark ? [235, 95, 30] : isLight ? [190, 80, 40] : [195, 125, 60];
      p.speedY = -Math.random() * 0.7 - 0.3;
      p.size = Math.random() * 2.2 + 0.8;
    } else if (type === 'leaf') {
      p.color = isDark ? [107, 142, 110] : isLight ? [125, 145, 115] : [110, 125, 140];
      p.speedY = Math.random() * 0.35 + 0.15; // Falls downwards
      p.speedX = (Math.random() - 0.35) * 0.4;
      p.size = Math.random() * 4 + 3;
    } else if (type === 'petal') {
      p.color = isDark ? [185, 85, 105] : isLight ? [195, 115, 125] : [155, 135, 145];
      p.speedY = Math.random() * 0.45 + 0.15; // Falls downwards
      p.speedX = (Math.random() - 0.4) * 0.5;
      p.size = Math.random() * 3.5 + 2.5;
    } else if (type === 'rune') {
      p.rune = runesList[Math.floor(Math.random() * runesList.length)];
      p.size = Math.random() * 5 + 9;
      p.speedY = -Math.random() * 0.3 - 0.1;
      p.opacity = Math.random() * 0.25 + 0.08; // Keep script runes soft
    }

    particles.push(p);
  }

  function draw() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    
    for (const p of particles) {
      ctx.save();
      ctx.globalAlpha = p.opacity;

      if (p.type === 'dust' || p.type === 'ember') {
        ctx.beginPath();
        ctx.arc(p.x, p.y, p.size, 0, Math.PI * 2);
        const col = p.color || p.baseColor;
        ctx.fillStyle = `rgba(${col[0]},${col[1]},${col[2]},${p.opacity})`;
        if (p.type === 'ember') {
          ctx.shadowBlur = 5;
          ctx.shadowColor = `rgba(${col[0]},${col[1]},${col[2]},0.5)`;
          
          // Subtle ember sparkle variation
          p.opacity += (Math.random() - 0.5) * 0.04;
          if (p.opacity < 0.1) p.opacity = 0.1;
          if (p.opacity > 0.65) p.opacity = 0.65;
        }
        ctx.fill();

        p.x += p.speedX;
        p.y += p.speedY;

        if (p.y < -10) { p.y = canvas.height + 10; p.x = Math.random() * canvas.width; }
      } 
      else if (p.type === 'leaf' || p.type === 'petal') {
        p.angle += p.spin;
        p.x += p.speedX + Math.sin(p.angle) * 0.25;
        p.y += p.speedY;

        ctx.translate(p.x, p.y);
        ctx.rotate(p.angle);
        ctx.beginPath();
        ctx.fillStyle = `rgba(${p.color[0]},${p.color[1]},${p.color[2]},${p.opacity})`;
        ctx.ellipse(0, 0, p.size, p.size * 0.5, 0, 0, Math.PI * 2);
        ctx.fill();

        if (p.y > canvas.height + 10) { p.y = -10; p.x = Math.random() * canvas.width; }
      } 
      else if (p.type === 'rune') {
        p.x += p.speedX;
        p.y += p.speedY;
        
        ctx.font = `${p.size}px serif`;
        ctx.fillStyle = `rgba(${p.baseColor[0]},${p.baseColor[1]},${p.baseColor[2]},${p.opacity})`;
        ctx.fillText(p.rune, p.x, p.y);

        if (p.y < -20) { p.y = canvas.height + 20; p.x = Math.random() * canvas.width; }
      }

      if (p.x < -20) p.x = canvas.width + 20;
      if (p.x > canvas.width + 20) p.x = -20;

      ctx.restore();
    }
    raf = requestAnimationFrame(draw);
  }
  draw();
}
window.addEventListener('resize', () => { initParticles(); });
initParticles();
</script>
</body>
</html>
