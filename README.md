<!DOCTYPE html>

<html lang="ko">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
<title>워드로그 · WordLog</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Gowun+Batang:wght@400;700&family=Gowun+Dodum&family=Fraunces:ital,opsz,wght@0,9..144,400;0,9..144,500;0,9..144,600;1,9..144,400;1,9..144,500&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #FFF6EE;
    --coral: #FF7B6B;
    --coral-deep: #E85A4A;
    --peach: #FFB591;
    --sky: #7EC8F5;
    --sky-soft: #B8E0F7;
    --sunny: #FFD93D;
    --mint: #A8E6CF;
    --lavender: #C9B6F0;
    --ink: #3D2B25;
    --ink-soft: #6B564C;
    --muted: #A89488;
    --paper: #FFFCF7;
    --line: rgba(61, 43, 37, 0.1);
  }
  * { margin: 0; padding: 0; box-sizing: border-box; -webkit-tap-highlight-color: transparent; }
  html, body { height: 100%; overflow-x: hidden; }
  body {
    font-family: 'Gowun Dodum', sans-serif;
    background: var(--bg); color: var(--ink);
    -webkit-font-smoothing: antialiased;
    background-image:
      radial-gradient(at 15% 5%, rgba(255, 181, 145, 0.35) 0%, transparent 45%),
      radial-gradient(at 85% 10%, rgba(126, 200, 245, 0.25) 0%, transparent 45%),
      radial-gradient(at 50% 95%, rgba(255, 217, 61, 0.2) 0%, transparent 50%);
  }
  .app {
    max-width: 480px; margin: 0 auto;
    min-height: 100vh;
    display: flex; flex-direction: column;
    position: relative;
  }
  .deco { position: absolute; pointer-events: none; z-index: 0; animation: bob 6s ease-in-out infinite; }
  .deco.star1 { top: 60px; right: 30px; font-size: 16px; color: var(--sunny); }
  .deco.star2 { top: 140px; left: 18px; font-size: 12px; color: var(--coral); animation-delay: 1.5s; }
  .deco.heart1 { top: 90px; left: 30px; font-size: 14px; color: var(--coral); animation-delay: 0.8s; opacity: 0.7; }
  @keyframes bob { 0%,100%{transform:translateY(0) rotate(0deg);} 50%{transform:translateY(-6px) rotate(8deg);} }
  .header {
    padding: 20px 22px 16px;
    display: flex; justify-content: space-between; align-items: center;
    position: relative; z-index: 1;
  }
  .logo-wrap { display: flex; align-items: center; gap: 8px; }
  .logo-mark {
    width: 36px; height: 36px;
    background: linear-gradient(135deg, var(--coral), var(--peach));
    border-radius: 12px;
    display: flex; align-items: center; justify-content: center;
    color: white;
    font-family: 'Fraunces', serif;
    font-weight: 600; font-style: italic; font-size: 18px;
    box-shadow: 0 4px 12px -2px rgba(255, 123, 107, 0.5);
    transform: rotate(-4deg);
  }
  .logo-text { font-family: 'Fraunces', serif; font-size: 22px; font-weight: 500; font-style: italic; color: var(--ink); }
  .logo-text .accent { color: var(--coral); }
  .logo-kr { font-size: 10px; letter-spacing: 3px; color: var(--muted); margin-top: 1px; }
  .time-badge {
    font-family: 'Fraunces', serif; font-size: 14px;
    background: white; border: 1.5px solid var(--line);
    padding: 8px 14px; border-radius: 100px;
    display: flex; align-items: center; gap: 7px;
    box-shadow: 0 2px 8px -2px rgba(61, 43, 37, 0.08);
  }
  .time-dot { width: 7px; height: 7px; background: var(--coral); border-radius: 50%; animation: pulse 2s infinite; }
  @keyframes pulse { 0%,100% { opacity: 1; } 50% { opacity: 0.6; } }

.tabs { display: flex; padding: 8px 22px; gap: 6px; position: relative; z-index: 1; }
.tab {
flex: 1; text-align: center; padding: 10px 0;
font-size: 13px; color: var(–muted);
cursor: pointer; border-radius: 100px; transition: all 0.3s;
}
.tab.active { color: var(–ink); background: white; font-weight: 700; box-shadow: 0 2px 8px -2px rgba(61, 43, 37, 0.1); }

.page { display: none; position: relative; z-index: 1; }
.page.active { display: block; animation: pageIn 0.3s ease-out; }
@keyframes pageIn { from { opacity: 0; transform: translateY(8px); } to { opacity: 1; transform: translateY(0); } }

.top-bar { margin: 4px 22px 0; display: flex; gap: 8px; }
.group-selector {
flex: 1; background: white;
border: 1.5px solid var(–line); border-radius: 14px;
padding: 9px 13px;
display: flex; align-items: center; gap: 8px;
cursor: pointer;
}
.group-avatar {
width: 26px; height: 26px; border-radius: 50%;
background: linear-gradient(135deg, var(–coral), var(–peach));
color: white;
display: flex; align-items: center; justify-content: center;
font-size: 12px; font-weight: 700; flex-shrink: 0;
}
.group-info { flex: 1; min-width: 0; }
.group-name { font-size: 12px; font-weight: 700; color: var(–ink); overflow: hidden; text-overflow: ellipsis; white-space: nowrap; }
.group-meta { font-size: 10px; color: var(–muted); margin-top: 1px; display: flex; align-items: center; gap: 4px; }
.privacy-pill { padding: 1px 6px; border-radius: 100px; font-size: 9px; font-weight: 700; }
.privacy-pill.private { background: rgba(126, 200, 245, 0.25); color: #2D7AB5; }
.privacy-pill.public { background: rgba(255, 217, 61, 0.35); color: #8B6F00; }
.group-chevron { color: var(–muted); font-size: 14px; }

.interval-toggle { background: white; border: 1.5px solid var(–line); border-radius: 14px; padding: 4px; display: flex; gap: 2px; }
.interval-btn { padding: 6px 10px; background: transparent; border: none; border-radius: 10px; font-family: inherit; font-size: 11px; font-weight: 700; color: var(–muted); cursor: pointer; }
.interval-btn.active { background: linear-gradient(135deg, var(–coral), var(–peach)); color: white; box-shadow: 0 2px 6px -1px rgba(255, 123, 107, 0.4); }

/* MODE TOGGLE (Photo/Video) + Filter strip */
.mode-filter-bar {
margin: 10px 22px 0;
display: flex;
gap: 8px;
align-items: center;
}
.mode-toggle {
background: white; border: 1.5px solid var(–line);
border-radius: 14px; padding: 4px;
display: flex; gap: 2px;
flex-shrink: 0;
}
.mode-btn {
padding: 7px 11px; background: transparent; border: none;
border-radius: 10px; font-family: inherit;
font-size: 11px; font-weight: 700; color: var(–muted);
cursor: pointer;
display: flex; align-items: center; gap: 4px;
}
.mode-btn svg { width: 13px; height: 13px; }
.mode-btn.active { background: linear-gradient(135deg, var(–coral), var(–peach)); color: white; box-shadow: 0 2px 6px -1px rgba(255, 123, 107, 0.4); }

.filter-strip {
flex: 1;
display: flex; gap: 6px;
overflow-x: auto; -webkit-overflow-scrolling: touch;
scrollbar-width: none;
padding: 2px 0;
}
.filter-strip::-webkit-scrollbar { display: none; }
.filter-chip {
flex-shrink: 0; padding: 6px 11px;
background: white; border: 1.5px solid var(–line);
border-radius: 100px; font-size: 11px; color: var(–ink-soft);
cursor: pointer; white-space: nowrap;
box-shadow: 0 2px 6px -2px rgba(61, 43, 37, 0.08);
transition: all 0.2s;
}
.filter-chip.active {
background: var(–ink); color: white; border-color: var(–ink);
}

/* VIEWFINDER */
.viewfinder {
position: relative; margin: 12px 22px 0;
aspect-ratio: 3/4; border-radius: 28px;
overflow: hidden; background: #1a1816;
box-shadow: 0 20px 40px -15px rgba(255, 123, 107, 0.25);
cursor: pointer;
}
.viewfinder.live { cursor: default; }
.demo-bg {
position: absolute; inset: 0;
background:
linear-gradient(180deg, rgba(255, 200, 150, 0.15) 0%, transparent 40%, rgba(120, 80, 100, 0.3) 100%),
linear-gradient(135deg, #FFB591 0%, #FFC9A1 25%, #FFAEC8 55%, #C9B6F0 85%, #9BB8E8 100%);
animation: shift 16s ease-in-out infinite alternate;
}
.demo-bg::after { content: ‘’; position: absolute; inset: 0;
background-image:
radial-gradient(ellipse at 25% 25%, rgba(255, 245, 220, 0.55) 0%, transparent 45%),
radial-gradient(ellipse at 75% 70%, rgba(255, 180, 200, 0.4) 0%, transparent 45%);
animation: float 12s ease-in-out infinite alternate;
}
@keyframes shift { 0% { filter: hue-rotate(0deg); } 100% { filter: hue-rotate(20deg); } }
@keyframes float { 0% { transform: translate(0,0); } 100% { transform: translate(-3%,3%); } }

/* Filter layer wrap — actual filters applied here */
.filter-layer {
position: absolute; inset: 0;
transition: filter 0.3s;
}

#cameraStream {
position: absolute; inset: 0;
width: 100%; height: 100%; object-fit: cover;
display: none; background: #000;
}
#cameraStream.mirrored { transform: scaleX(-1); }
.viewfinder.live #cameraStream { display: block; }
.viewfinder.live .demo-bg { display: none; }
#snapshotImg {
position: absolute; inset: 0;
width: 100%; height: 100%; object-fit: cover; display: none;
}
.viewfinder.snapshot #snapshotImg { display: block; }
.viewfinder.snapshot #cameraStream, .viewfinder.snapshot .demo-bg { display: none; }

.start-overlay {
position: absolute; inset: 0; z-index: 4;
display: flex; flex-direction: column; align-items: center; justify-content: center;
background: rgba(0, 0, 0, 0.45); backdrop-filter: blur(2px);
color: white; text-align: center; padding: 30px;
cursor: pointer;
}
.viewfinder.live .start-overlay,
.viewfinder.snapshot .start-overlay,
.viewfinder.cam-loading .start-overlay { display: none; }
.start-icon {
width: 80px; height: 80px; border-radius: 50%;
background: linear-gradient(135deg, var(–coral), var(–peach));
display: flex; align-items: center; justify-content: center;
box-shadow: 0 10px 30px -5px rgba(255, 123, 107, 0.7);
animation: pulse-grow 2s ease-in-out infinite; margin-bottom: 18px;
}
.start-icon svg { width: 36px; height: 36px; color: white; }
@keyframes pulse-grow { 0%,100% { transform: scale(1); } 50% { transform: scale(1.08); } }
.start-title { font-size: 18px; font-weight: 700; margin-bottom: 6px; text-shadow: 0 2px 6px rgba(0,0,0,0.5); }
.start-sub { font-size: 12px; color: rgba(255,255,255,0.85); text-shadow: 0 1px 3px rgba(0,0,0,0.5); }
.cam-loading-msg {
position: absolute; inset: 0;
display: none; align-items: center; justify-content: center;
color: white; font-size: 13px; z-index: 4;
background: rgba(0,0,0,0.4); backdrop-filter: blur(2px);
}
.viewfinder.cam-loading .cam-loading-msg { display: flex; }
.cam-loading-msg::before { content: ‘’; width: 24px; height: 24px; border: 2px solid rgba(255,255,255,0.3); border-top-color: white; border-radius: 50%; animation: spin 0.8s linear infinite; margin-right: 10px; }
@keyframes spin { to { transform: rotate(360deg); } }

.mode-badge {
position: absolute; top: 16px; right: 16px;
display: flex; align-items: center; gap: 6px;
color: white; font-size: 10px; letter-spacing: 1.5px; z-index: 2;
padding: 5px 11px;
background: rgba(255, 255, 255, 0.25);
border-radius: 100px; backdrop-filter: blur(8px);
border: 1px solid rgba(255,255,255,0.3);
}
.mode-dot { width: 6px; height: 6px; border-radius: 50%; background: var(–sunny); }
.viewfinder.live .mode-dot { background: #FF5544; animation: pulse 1.2s infinite; }
.viewfinder.live .mode-text::after { content: ‘LIVE’; }
.viewfinder:not(.live) .mode-text::after { content: ‘PREVIEW’; }
.viewfinder.recording .mode-text::after { content: ‘REC’; }
.viewfinder.recording .mode-dot { background: #FF1100; }

.vf-meta {
position: absolute; top: 16px; left: 16px;
font-family: ‘Fraunces’, serif; color: white;
font-size: 11px; letter-spacing: 1.5px;
text-shadow: 0 1px 3px rgba(0,0,0,0.3); z-index: 2;
padding: 5px 10px;
background: rgba(255,255,255,0.2);
border-radius: 100px; backdrop-filter: blur(8px);
}

/* Recording timer */
.rec-timer {
position: absolute;
top: 48px; left: 50%; transform: translateX(-50%);
font-family: ‘Fraunces’, serif;
color: white; font-size: 13px;
padding: 4px 12px;
background: rgba(255, 17, 0, 0.85);
border-radius: 100px;
z-index: 4;
display: none;
box-shadow: 0 4px 12px rgba(255, 17, 0, 0.4);
}
.viewfinder.recording .rec-timer { display: block; }

.verse-overlay {
position: absolute; inset: 0;
display: flex; flex-direction: column;
justify-content: center; align-items: center;
padding: 50px 36px; z-index: 3;
}
.verse-sparkle { font-size: 16px; margin-bottom: 8px; filter: drop-shadow(0 1px 3px rgba(0,0,0,0.3)); animation: twinkle 2.5s ease-in-out infinite; }
@keyframes twinkle { 0%,100% { opacity: 1; transform: scale(1) rotate(0deg); } 50% { opacity: 0.7; transform: scale(1.15) rotate(15deg); } }
.verse-text {
font-family: ‘Gowun Batang’, serif;
font-weight: 400; font-size: 17px; line-height: 1.9;
color: #ffffff; text-align: center;
text-shadow: 0 2px 12px rgba(60, 30, 50, 0.5), 0 1px 3px rgba(60, 30, 50, 0.7);
word-break: keep-all; max-width: 320px;
cursor: pointer; transition: opacity 0.3s;
pointer-events: auto;
}
.verse-text.en { font-family: ‘Fraunces’, serif; font-style: italic; font-size: 16px; line-height: 1.7; }
.verse-text.fading { opacity: 0; }
.verse-ref {
font-family: ‘Fraunces’, serif; font-style: italic;
font-size: 13px; color: rgba(255, 255, 255, 0.95);
margin-top: 16px; letter-spacing: 1.5px;
text-shadow: 0 1px 6px rgba(60, 30, 50, 0.5);
padding: 4px 12px;
background: rgba(255,255,255,0.2);
border-radius: 100px; backdrop-filter: blur(4px);
}
.lang-hint { margin-top: 10px; font-size: 9px; color: rgba(255,255,255,0.7); letter-spacing: 1.5px; padding: 3px 8px; background: rgba(0,0,0,0.15); border-radius: 100px; backdrop-filter: blur(4px); }
.flash { position: absolute; inset: 0; background: white; opacity: 0; pointer-events: none; z-index: 5; }
.flash.fire { animation: flash 0.4s ease-out; }
@keyframes flash { 0% { opacity: 0; } 20% { opacity: 0.85; } 100% { opacity: 0; } }

.controls {
padding: 18px 22px 14px;
display: flex; align-items: center; justify-content: space-between; gap: 16px;
}
.ctrl-side { flex: 1; display: flex; align-items: center; }
.ctrl-side.right { justify-content: flex-end; }
.icon-btn {
width: 50px; height: 50px; border-radius: 18px;
background: white; border: none;
display: flex; align-items: center; justify-content: center;
cursor: pointer; color: var(–ink-soft);
box-shadow: 0 4px 12px -3px rgba(61, 43, 37, 0.15);
}
.icon-btn:active { transform: scale(0.9); }
.icon-btn svg { width: 22px; height: 22px; }
.icon-btn.accent { background: linear-gradient(135deg, var(–sky), var(–sky-soft)); color: white; }

.shutter {
width: 80px; height: 80px; border-radius: 50%;
background: white; border: none;
display: flex; align-items: center; justify-content: center;
cursor: pointer; position: relative;
box-shadow: 0 6px 20px -4px rgba(255, 123, 107, 0.45);
transition: all 0.2s;
}
.shutter:active { transform: scale(0.92); }
.shutter-inner {
width: 60px; height: 60px; border-radius: 50%;
background: linear-gradient(135deg, var(–coral) 0%, var(–peach) 60%, var(–sunny) 100%);
transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1);
}
.shutter.video .shutter-inner {
background: #FF1100;
border-radius: 12px;
width: 32px; height: 32px;
}
.shutter.recording .shutter-inner {
background: #FF1100;
border-radius: 8px;
width: 24px; height: 24px;
}
.shutter::after {
content: ‘’; position: absolute; inset: -6px;
border-radius: 50%; border: 2px solid var(–coral); opacity: 0.3;
}
.shutter.recording::after {
border-color: #FF1100;
animation: rec-ring 1.5s ease-in-out infinite;
}
@keyframes rec-ring {
0%, 100% { opacity: 0.3; transform: scale(1); }
50% { opacity: 0.7; transform: scale(1.05); }
}

.photo-hint { text-align: center; font-size: 11px; color: var(–muted); padding: 0 22px 12px; }
.photo-hint .em { color: var(–coral); font-weight: 700; }

.themes { padding: 6px 22px 16px; display: flex; gap: 8px; overflow-x: auto; -webkit-overflow-scrolling: touch; scrollbar-width: none; }
.themes::-webkit-scrollbar { display: none; }
.theme-chip { flex-shrink: 0; padding: 9px 16px; border-radius: 100px; font-size: 13px; color: var(–ink); background: white; cursor: pointer; white-space: nowrap; box-shadow: 0 2px 6px -2px rgba(61, 43, 37, 0.1); }
.theme-chip:nth-child(1).active { background: linear-gradient(135deg, var(–coral), var(–peach)); color: white; }
.theme-chip:nth-child(2).active { background: linear-gradient(135deg, var(–sky), var(–lavender)); color: white; }
.theme-chip:nth-child(3).active { background: linear-gradient(135deg, var(–sunny), var(–peach)); color: var(–ink); }
.theme-chip:nth-child(4).active { background: linear-gradient(135deg, var(–mint), var(–sky-soft)); color: var(–ink); }
.theme-chip:nth-child(5).active { background: linear-gradient(135deg, var(–lavender), var(–coral)); color: white; }
.theme-chip:nth-child(6).active { background: linear-gradient(135deg, var(–peach), var(–coral)); color: white; }

.info-strip { padding: 0 22px 12px; text-align: center; }
.info-line { color: var(–ink); font-size: 13px; margin-bottom: 3px; }
.info-line .em { color: var(–coral); font-weight: 700; }
.info-sub { font-family: ‘Fraunces’, serif; font-style: italic; font-size: 11px; color: var(–muted); letter-spacing: 1.5px; }

/* FEED */
.feed-header { margin: 6px 22px 14px; background: white; border: 1.5px solid var(–line); border-radius: 16px; padding: 12px 16px; display: flex; align-items: center; gap: 10px; }
.feed-header .group-avatar { width: 36px; height: 36px; font-size: 14px; }
.feed-header-info { flex: 1; }
.feed-header-name { font-size: 14px; font-weight: 700; color: var(–ink); }
.feed-header-sub { font-size: 11px; color: var(–muted); margin-top: 2px; }
.feed-header-action { font-size: 12px; color: var(–coral); font-weight: 700; padding: 6px 10px; border-radius: 100px; background: rgba(255,123,107,0.1); }

/* GRID FEED */
.feed { padding: 0 14px 20px; }
.feed-time-label { font-family: ‘Fraunces’, serif; font-style: italic; font-size: 12px; color: var(–muted); letter-spacing: 1.5px; text-align: center; margin: 14px 0 10px; position: relative; }
.feed-time-label::before, .feed-time-label::after { content: ‘’; position: absolute; top: 50%; width: 30px; height: 1px; background: var(–line); }
.feed-time-label::before { left: 50%; transform: translateX(-90px); }
.feed-time-label::after { right: 50%; transform: translateX(90px); }
.feed-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 8px; }
.grid-card {
position: relative;
aspect-ratio: 3/4;
border-radius: 14px;
overflow: hidden;
cursor: pointer;
box-shadow: 0 4px 14px -6px rgba(61, 43, 37, 0.2);
transition: transform 0.2s;
}
.grid-card:active { transform: scale(0.97); }
.grid-card-bg { position: absolute; inset: 0; }
.grid-card-verse {
position: absolute; inset: 0;
display: flex; flex-direction: column;
justify-content: center; align-items: center;
padding: 14px; text-align: center;
}
.grid-card-verse-text {
font-family: ‘Gowun Batang’, serif;
font-size: 10px; line-height: 1.6;
color: white; word-break: keep-all;
text-shadow: 0 1px 4px rgba(60, 30, 50, 0.5), 0 1px 2px rgba(60, 30, 50, 0.7);
}
.grid-card-verse-ref {
font-family: ‘Fraunces’, serif; font-style: italic;
font-size: 8px; color: rgba(255,255,255,0.95);
margin-top: 6px; letter-spacing: 1px;
padding: 2px 6px;
background: rgba(255,255,255,0.22);
border-radius: 100px;
backdrop-filter: blur(4px);
}
.grid-card-avatar {
position: absolute; top: 7px; left: 7px;
width: 22px; height: 22px; border-radius: 50%;
display: flex; align-items: center; justify-content: center;
color: white; font-size: 10px; font-weight: 700;
border: 1.5px solid white;
box-shadow: 0 2px 6px rgba(0,0,0,0.2);
}
.grid-card-stamp {
position: absolute; bottom: 7px; left: 7px;
font-family: ‘Fraunces’, serif; font-style: italic;
color: white; font-size: 9px;
text-shadow: 0 1px 3px rgba(0,0,0,0.5);
}
.grid-card-likes {
position: absolute; bottom: 7px; right: 7px;
display: flex; align-items: center; gap: 3px;
color: white; font-size: 9px; font-weight: 700;
text-shadow: 0 1px 3px rgba(0,0,0,0.5);
}
.grid-card-likes svg { width: 10px; height: 10px; fill: white; }
.grid-card-vidbadge {
position: absolute; top: 7px; right: 7px;
padding: 2px 5px;
background: rgba(0,0,0,0.5);
color: white; font-size: 8px;
border-radius: 100px;
display: flex; align-items: center; gap: 2px;
backdrop-filter: blur(4px);
}
.grid-card-vidbadge svg { width: 7px; height: 7px; fill: white; }

.feed-empty { text-align: center; padding: 40px 22px; color: var(–muted); font-size: 13px; line-height: 1.6; }
.feed-empty-icon { font-size: 32px; margin-bottom: 10px; }

/* DETAIL MODAL */
.detail-modal {
position: fixed; inset: 0;
background: rgba(20, 12, 16, 0.95);
backdrop-filter: blur(20px);
z-index: 110;
display: none;
overflow-y: auto;
}
.detail-modal.show { display: block; animation: fadeIn 0.3s; }
.detail-wrap {
max-width: 480px; margin: 0 auto;
min-height: 100vh;
display: flex; flex-direction: column;
padding: 14px 18px 24px;
}
.detail-topbar {
display: flex; align-items: center; justify-content: space-between;
margin-bottom: 14px;
}
.detail-close {
width: 38px; height: 38px;
border-radius: 50%;
background: rgba(255,255,255,0.15);
border: none;
color: white; font-size: 20px;
cursor: pointer;
display: flex; align-items: center; justify-content: center;
backdrop-filter: blur(8px);
}
.detail-close:active { transform: scale(0.9); }
.detail-user {
display: flex; align-items: center; gap: 9px;
color: white;
flex: 1; margin-left: 12px;
}
.detail-user-avatar {
width: 34px; height: 34px; border-radius: 50%;
display: flex; align-items: center; justify-content: center;
color: white; font-size: 13px; font-weight: 700;
}
.detail-user-name { font-size: 13px; font-weight: 700; }
.detail-user-time { font-size: 10px; opacity: 0.7; margin-top: 2px; }

.detail-card {
aspect-ratio: 3/4;
border-radius: 24px;
overflow: hidden;
position: relative;
margin-bottom: 16px;
box-shadow: 0 20px 50px -10px rgba(0,0,0,0.5);
animation: detailIn 0.5s cubic-bezier(0.16, 1, 0.3, 1);
}
@keyframes detailIn {
from { transform: scale(0.92); opacity: 0; }
to { transform: scale(1); opacity: 1; }
}
.detail-card-bg { position: absolute; inset: 0; }
.detail-card-verse {
position: absolute; inset: 0;
display: flex; flex-direction: column;
justify-content: center; align-items: center;
padding: 40px 28px; text-align: center;
}
.detail-card-verse::before {
content: ‘✦’; font-size: 18px;
color: rgba(255,255,255,0.95); margin-bottom: 10px;
filter: drop-shadow(0 1px 3px rgba(0,0,0,0.3));
}
.detail-card-verse-text {
font-family: ‘Gowun Batang’, serif;
font-size: 19px; line-height: 1.85;
color: white; word-break: keep-all;
text-shadow: 0 2px 12px rgba(60, 30, 50, 0.5), 0 1px 3px rgba(60, 30, 50, 0.7);
max-width: 320px;
}
.detail-card-verse-ref {
font-family: ‘Fraunces’, serif; font-style: italic;
font-size: 13px; color: rgba(255,255,255,0.95);
margin-top: 16px; letter-spacing: 1.5px;
padding: 4px 12px;
background: rgba(255,255,255,0.22);
border-radius: 100px;
backdrop-filter: blur(4px);
}
.detail-card-stamp {
position: absolute; top: 16px; left: 16px;
font-family: ‘Fraunces’, serif; font-style: italic;
color: white; font-size: 12px;
padding: 4px 10px;
background: rgba(255,255,255,0.2);
border-radius: 100px;
backdrop-filter: blur(4px);
}

.detail-pills {
display: flex; gap: 5px; flex-wrap: wrap;
margin-bottom: 14px;
}
.detail-pill {
font-size: 10px; padding: 4px 10px;
border-radius: 100px; font-weight: 700;
}
.detail-pill.private { background: rgba(126, 200, 245, 0.25); color: #B3DBF5; border: 1px solid rgba(126, 200, 245, 0.4); }
.detail-pill.public { background: rgba(255, 217, 61, 0.25); color: #FFE07A; border: 1px solid rgba(255, 217, 61, 0.4); }
.detail-pill.cell { background: rgba(168, 230, 207, 0.25); color: #B5E8D0; border: 1px solid rgba(168, 230, 207, 0.4); }

.detail-actions {
display: flex; align-items: center; gap: 18px;
padding: 8px 4px 16px;
border-bottom: 1px solid rgba(255,255,255,0.1);
margin-bottom: 14px;
}
.detail-act {
display: flex; align-items: center; gap: 6px;
color: white; font-size: 14px; font-weight: 600;
cursor: pointer;
}
.detail-act svg { width: 24px; height: 24px; }
.detail-act.liked { color: var(–coral); }
.detail-act.liked svg { fill: var(–coral); }
.detail-share {
margin-left: auto;
color: white;
cursor: pointer;
display: flex; align-items: center;
}
.detail-share svg { width: 22px; height: 22px; }

.detail-comments-label {
color: rgba(255,255,255,0.7);
font-size: 11px; font-weight: 700;
letter-spacing: 0.5px; margin-bottom: 10px;
}
.detail-comment {
display: flex; gap: 9px; padding: 8px 0;
color: white;
}
.detail-comment-avatar {
width: 28px; height: 28px; border-radius: 50%;
display: flex; align-items: center; justify-content: center;
color: white; font-size: 11px; font-weight: 700;
flex-shrink: 0;
}
.detail-comment-body { flex: 1; }
.detail-comment-name { font-size: 12px; font-weight: 700; }
.detail-comment-text { font-size: 13px; line-height: 1.5; margin-top: 2px; }
.detail-comment-empty { color: rgba(255,255,255,0.5); font-size: 12px; text-align: center; padding: 16px 0; font-style: italic; }

/* SHEET */
.sheet { position: fixed; inset: 0; background: rgba(60, 30, 50, 0.6); backdrop-filter: blur(8px); z-index: 90; display: none; align-items: flex-end; justify-content: center; }
.sheet.show { display: flex; animation: fadeIn 0.3s; }
.sheet-content { background: var(–paper); width: 100%; max-width: 480px; border-radius: 28px 28px 0 0; padding: 14px 22px 28px; animation: slideUp 0.35s cubic-bezier(0.16, 1, 0.3, 1); max-height: 85vh; overflow-y: auto; }
@keyframes slideUp { from { transform: translateY(100%); } to { transform: translateY(0); } }
.sheet-handle { width: 40px; height: 4px; background: var(–line); border-radius: 100px; margin: 0 auto 14px; }
.sheet-title { font-weight: 700; font-size: 16px; color: var(–ink); text-align: center; margin-bottom: 6px; }
.sheet-sub { font-size: 11px; color: var(–muted); text-align: center; margin-bottom: 16px; }
.group-list { display: flex; flex-direction: column; gap: 8px; margin-bottom: 14px; }
.group-item { background: white; border: 1.5px solid var(–line); border-radius: 16px; padding: 12px; display: flex; align-items: center; gap: 10px; cursor: pointer; }
.group-item.selected { border-color: var(–coral); background: rgba(255, 123, 107, 0.06); }
.group-item .group-avatar { width: 36px; height: 36px; font-size: 14px; }
.group-item.public .group-avatar { background: linear-gradient(135deg, var(–sunny), var(–peach)); }
.group-item.solo .group-avatar { background: linear-gradient(135deg, var(–sky), var(–lavender)); }
.group-item.cell .group-avatar { background: linear-gradient(135deg, var(–mint), var(–sky-soft)); color: var(–ink); }
.group-item-info { flex: 1; }
.group-item-name { font-size: 14px; font-weight: 700; color: var(–ink); }
.group-item-meta { font-size: 11px; color: var(–muted); margin-top: 2px; }
.group-item-check { width: 22px; height: 22px; border-radius: 50%; border: 1.5px solid var(–line); display: flex; align-items: center; justify-content: center; color: white; font-size: 13px; flex-shrink: 0; }
.group-item.selected .group-item-check { background: var(–coral); border-color: var(–coral); }
.sheet-actions { display: flex; gap: 8px; position: sticky; bottom: 0; background: var(–paper); padding-top: 8px; }
.sheet-btn { flex: 1; padding: 12px; border: 1.5px solid var(–line); background: white; border-radius: 100px; font-family: inherit; font-size: 13px; font-weight: 700; color: var(–ink); cursor: pointer; }
.sheet-btn.primary { background: linear-gradient(135deg, var(–coral), var(–peach)); color: white; border-color: transparent; box-shadow: 0 4px 12px -2px rgba(255, 123, 107, 0.4); }

/* MODAL */
.modal { position: fixed; inset: 0; background: rgba(60, 30, 50, 0.75); backdrop-filter: blur(10px); z-index: 100; display: none; align-items: center; justify-content: center; padding: 20px; }
.modal.show { display: flex; animation: fadeIn 0.4s; }
@keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
.card { background: var(–paper); width: 100%; max-width: 360px; padding: 22px 20px 18px; border-radius: 28px; box-shadow: 0 40px 80px -20px rgba(0,0,0,0.5); animation: cardIn 0.6s cubic-bezier(0.34, 1.56, 0.64, 1); max-height: 90vh; overflow-y: auto; }
@keyframes cardIn { from { transform: translateY(30px) scale(0.92); opacity: 0; } to { transform: translateY(0) scale(1); opacity: 1; } }
.card-img { aspect-ratio: 3/4; border-radius: 20px; overflow: hidden; position: relative; margin-bottom: 14px; background: #2a2622; }
#cardCapturedImg, #cardCapturedVideo { position: absolute; inset: 0; width: 100%; height: 100%; object-fit: cover; }
#cardCapturedVideo { display: none; }
.card.video #cardCapturedImg { display: none; }
.card.video #cardCapturedVideo { display: block; }
.card-meta-line { font-family: ‘Fraunces’, serif; font-style: italic; font-size: 12px; color: var(–ink); text-align: center; margin-bottom: 14px; }
.post-section-label { font-size: 11px; font-weight: 700; color: var(–ink-soft); margin-bottom: 8px; letter-spacing: 0.5px; display: flex; align-items: center; gap: 6px; }
.post-section-label .count { display: inline-block; padding: 1px 7px; background: var(–coral); color: white; border-radius: 100px; font-size: 10px; }
.post-groups { display: flex; flex-direction: column; gap: 6px; margin-bottom: 12px; }
.post-group-item { background: white; border: 1.5px solid var(–line); border-radius: 14px; padding: 10px 12px; display: flex; align-items: center; gap: 9px; cursor: pointer; }
.post-group-item.selected { border-color: var(–coral); background: rgba(255, 123, 107, 0.06); }
.post-group-item .group-avatar { width: 28px; height: 28px; font-size: 12px; }
.post-group-item.public .group-avatar { background: linear-gradient(135deg, var(–sunny), var(–peach)); }
.post-group-item.solo .group-avatar { background: linear-gradient(135deg, var(–sky), var(–lavender)); }
.post-group-item.cell .group-avatar { background: linear-gradient(135deg, var(–mint), var(–sky-soft)); color: var(–ink); }
.post-group-info { flex: 1; min-width: 0; }
.post-group-name { font-size: 13px; font-weight: 700; color: var(–ink); }
.post-group-meta { font-size: 10px; color: var(–muted); margin-top: 1px; }
.post-group-check { width: 20px; height: 20px; border-radius: 6px; border: 1.5px solid var(–line); display: flex; align-items: center; justify-content: center; color: white; font-size: 12px; flex-shrink: 0; }
.post-group-item.selected .post-group-check { background: var(–coral); border-color: var(–coral); }

/* Download button */
.download-row {
background: rgba(126, 200, 245, 0.1);
border: 1.5px solid rgba(126, 200, 245, 0.3);
border-radius: 14px;
padding: 10px 14px;
margin-bottom: 12px;
display: flex; align-items: center; gap: 10px;
cursor: pointer;
}
.download-row:active { transform: scale(0.98); }
.download-icon {
width: 36px; height: 36px; border-radius: 10px;
background: linear-gradient(135deg, var(–sky), var(–sky-soft));
color: white;
display: flex; align-items: center; justify-content: center;
flex-shrink: 0;
}
.download-icon svg { width: 18px; height: 18px; }
.download-info { flex: 1; }
.download-title { font-size: 13px; font-weight: 700; color: var(–ink); }
.download-sub { font-size: 10px; color: var(–muted); margin-top: 1px; }
.download-arrow { color: var(–muted); font-size: 14px; }

.card-actions { display: flex; gap: 8px; margin-top: 4px; }
.btn { flex: 1; padding: 13px; border: none; background: rgba(255, 123, 107, 0.1); color: var(–ink); font-family: inherit; font-size: 13px; cursor: pointer; border-radius: 100px; font-weight: 700; }
.btn.primary { background: linear-gradient(135deg, var(–coral), var(–peach)); color: white; box-shadow: 0 4px 12px -2px rgba(255, 123, 107, 0.5); }
.btn.primary:disabled { opacity: 0.4; box-shadow: none; cursor: not-allowed; }

#fileInput { display: none; }

/* Toast */
.toast {
position: fixed; bottom: 30px; left: 50%;
transform: translateX(-50%) translateY(80px);
background: var(–ink); color: white;
padding: 12px 20px; border-radius: 100px;
font-size: 13px; font-weight: 700;
box-shadow: 0 8px 24px rgba(0,0,0,0.3);
z-index: 200;
opacity: 0; transition: all 0.3s;
display: flex; align-items: center; gap: 8px;
}
.toast.show { opacity: 1; transform: translateX(-50%) translateY(0); }
.toast .check {
width: 18px; height: 18px;
background: var(–mint); color: var(–ink);
border-radius: 50%;
display: flex; align-items: center; justify-content: center;
font-size: 11px; font-weight: 700;
}

.hint { text-align: center; font-size: 11px; color: var(–muted); padding: 4px 22px 22px; letter-spacing: 1.5px; font-family: ‘Fraunces’, serif; font-style: italic; }
.hint .heart { color: var(–coral); }
</style>

</head>
<body>

<div class="app">
  <span class="deco star1">✦</span>
  <span class="deco star2">✦</span>
  <span class="deco heart1">♥</span>

  <div class="header">
    <div class="logo-wrap">
      <div class="logo-mark">W</div>
      <div>
        <div class="logo-text">Word<span class="accent">·</span>Log</div>
        <div class="logo-kr">워 드 로 그</div>
      </div>
    </div>
    <div class="time-badge">
      <span class="time-dot"></span>
      <span id="currentTime">11:00</span>
    </div>
  </div>

  <div class="tabs">
    <div class="tab active" data-page="camera" onclick="switchTab('camera')">오늘의 말씀</div>
    <div class="tab" data-page="feed" onclick="switchTab('feed')">우리 로그</div>
    <div class="tab" data-page="public" onclick="switchTab('public')">전체</div>
  </div>

  <!-- CAMERA PAGE -->

  <div class="page active" id="page-camera">
    <div class="top-bar">
      <div class="group-selector" onclick="openGroupSheet()">
        <div class="group-avatar" id="groupAvatar">우</div>
        <div class="group-info">
          <div class="group-name" id="groupName">우리 가족</div>
          <div class="group-meta">
            <span class="privacy-pill private" id="privacyPill">비공개</span>
            <span id="groupMembers">4명</span>
          </div>
        </div>
        <div class="group-chevron">▾</div>
      </div>
      <div class="interval-toggle">
        <button class="interval-btn active" onclick="changeInterval(this, 1)">1시간</button>
        <button class="interval-btn" onclick="changeInterval(this, 3)">3시간</button>
      </div>
    </div>

```
<!-- Mode toggle + filter -->
<div class="mode-filter-bar">
  <div class="mode-toggle">
    <button class="mode-btn active" onclick="setMode(this, 'photo')">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
        <path d="M23 19a2 2 0 0 1-2 2H3a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h4l2-3h6l2 3h4a2 2 0 0 1 2 2z"/>
        <circle cx="12" cy="13" r="4"/>
      </svg>
      사진
    </button>
    <button class="mode-btn" onclick="setMode(this, 'video')">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
        <polygon points="23 7 16 12 23 17 23 7"/>
        <rect x="1" y="5" width="15" height="14" rx="2" ry="2"/>
      </svg>
      영상
    </button>
  </div>
  <div class="filter-strip" id="filterStrip">
    <div class="filter-chip active" data-filter="none" onclick="setFilter(this)">원본</div>
    <div class="filter-chip" data-filter="warm" onclick="setFilter(this)">따뜻하게</div>
    <div class="filter-chip" data-filter="cool" onclick="setFilter(this)">시원하게</div>
    <div class="filter-chip" data-filter="vintage" onclick="setFilter(this)">빈티지</div>
    <div class="filter-chip" data-filter="bw" onclick="setFilter(this)">흑백</div>
    <div class="filter-chip" data-filter="dreamy" onclick="setFilter(this)">몽환</div>
    <div class="filter-chip" data-filter="bright" onclick="setFilter(this)">화사</div>
  </div>
</div>

<div class="viewfinder" id="viewfinder" onclick="onViewfinderTap()">
  <div class="filter-layer" id="filterLayer">
    <div class="demo-bg"></div>
    <video id="cameraStream" autoplay playsinline muted></video>
    <img id="snapshotImg" alt="" />
  </div>

  <div class="vf-meta" id="vfTime">11:00 · 5.15</div>
  <div class="mode-badge">
    <span class="mode-dot"></span>
    <span class="mode-text"></span>
  </div>

  <div class="rec-timer" id="recTimer">● 00:00</div>

  <div class="verse-overlay">
    <div class="verse-sparkle">✦</div>
    <div class="verse-text" id="verseText">
      너희는 먼저 그의 나라와 그의 의를 구하라<br>
      그리하면 이 모든 것을 너희에게 더하시리라
    </div>
    <div class="verse-ref" id="verseRef">MATTHEW 6 : 33</div>
    <div class="lang-hint" id="langHint">탭하면 EN ▸</div>
  </div>

  <div class="start-overlay" id="startOverlay">
    <div class="start-icon">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
        <path d="M23 19a2 2 0 0 1-2 2H3a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h4l2-3h6l2 3h4a2 2 0 0 1 2 2z"/>
        <circle cx="12" cy="13" r="4"/>
      </svg>
    </div>
    <div class="start-title">탭해서 카메라 시작</div>
    <div class="start-sub">실시간 카메라 화면 위에 말씀이 떠요</div>
  </div>
  <div class="cam-loading-msg">카메라 켜는 중…</div>
  <div class="flash" id="flash"></div>
</div>

<div class="photo-hint" id="photoHint">
  풍경 · 셀카 · 일상 · <span class="em">무엇이든</span> 자유롭게
</div>

<div class="controls">
  <div class="ctrl-side">
    <button class="icon-btn" onclick="event.stopPropagation(); document.getElementById('fileInput').click()" title="갤러리">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
        <rect x="3" y="5" width="18" height="14" rx="3"/>
        <circle cx="8.5" cy="10.5" r="1.5"/>
        <path d="M21 16l-5-5L5 19"/>
      </svg>
    </button>
  </div>
  <button class="shutter" id="shutterBtn" onclick="event.stopPropagation(); handleShutter()">
    <div class="shutter-inner"></div>
  </button>
  <div class="ctrl-side right">
    <button class="icon-btn accent" onclick="event.stopPropagation(); flipCamera()" title="카메라 전환">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
        <path d="M15 7h3a2 2 0 0 1 2 2v8a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V9a2 2 0 0 1 2-2h3"/>
        <path d="M9 7l3-3 3 3"/>
        <circle cx="12" cy="13" r="3"/>
      </svg>
    </button>
  </div>
</div>

<div class="themes">
  <div class="theme-chip active" onclick="setTheme(this)">🌸 봄, 새로움</div>
  <div class="theme-chip" onclick="setTheme(this)">☁️ 쉼과 안식</div>
  <div class="theme-chip" onclick="setTheme(this)">✨ 믿음의 시작</div>
  <div class="theme-chip" onclick="setTheme(this)">🌿 감사</div>
  <div class="theme-chip" onclick="setTheme(this)">💜 소망</div>
  <div class="theme-chip" onclick="setTheme(this)">🧡 사랑</div>
</div>

<div class="info-strip">
  <div class="info-line">매 <span class="em" id="intervalLabel">1시간</span>마다 말씀이 찾아와요</div>
  <div class="info-sub">next · <span id="nextTime">12 : 00</span></div>
</div>
```

  </div>

  <!-- FEED -->

  <div class="page" id="page-feed">
    <div class="feed-header" onclick="openGroupSheet()">
      <div class="group-avatar" id="feedHeaderAvatar">우</div>
      <div class="feed-header-info">
        <div class="feed-header-name" id="feedHeaderName">우리 가족</div>
        <div class="feed-header-sub" id="feedHeaderSub">4명 · 오늘 3개의 묵상</div>
      </div>
      <div class="feed-header-action">전환 ▾</div>
    </div>
    <div class="feed" id="feedContainer"></div>
  </div>

  <!-- PUBLIC -->

  <div class="page" id="page-public">
    <div class="feed-header">
      <div class="group-avatar" style="background: linear-gradient(135deg, var(--sunny), var(--peach));">✦</div>
      <div class="feed-header-info">
        <div class="feed-header-name">전체 피드</div>
        <div class="feed-header-sub">모든 사용자의 공개 묵상 🌍</div>
      </div>
    </div>
    <div class="feed" id="publicContainer"></div>
  </div>

  <div class="hint">— made with <span class="heart">♥</span> for the word —</div>
</div>

<input type="file" id="fileInput" accept="image/*" onchange="loadImage(event)" />
<canvas id="captureCanvas" style="display:none"></canvas>

<div class="sheet" id="groupSheet" onclick="if(event.target===this) closeGroupSheet()">
  <div class="sheet-content">
    <div class="sheet-handle"></div>
    <div class="sheet-title">로그 전환</div>
    <div class="sheet-sub">어떤 그룹의 묵상을 볼까요?</div>
    <div class="group-list" id="groupList"></div>
    <div class="sheet-actions">
      <button class="sheet-btn" onclick="closeGroupSheet()">취소</button>
      <button class="sheet-btn primary" onclick="confirmGroup()">선택 ✨</button>
    </div>
  </div>
</div>

<div class="modal" id="modal">
  <div class="card" id="modalCard">
    <div class="card-img">
      <img id="cardCapturedImg" alt="" />
      <video id="cardCapturedVideo" controls playsinline loop></video>
    </div>
    <div class="card-meta-line" id="cardTime">11 : 00 · MAY 15</div>

```
<div class="download-row" onclick="downloadCapture()">
  <div class="download-icon">
    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
      <path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/>
      <polyline points="7 10 12 15 17 10"/>
      <line x1="12" y1="15" x2="12" y2="3"/>
    </svg>
  </div>
  <div class="download-info">
    <div class="download-title">📷 갤러리에 저장</div>
    <div class="download-sub" id="downloadSub">사진을 내 갤러리에 다운로드</div>
  </div>
  <div class="download-arrow">→</div>
</div>

<div class="post-section-label">
  어디에 게시할까요?
  <span class="count" id="postCount">1</span>
</div>
<div class="post-groups" id="postGroups"></div>

<div class="card-actions">
  <button class="btn" onclick="closeModal()">다시 찍기</button>
  <button class="btn primary" id="saveBtn" onclick="saveAndClose()">저장</button>
</div>
```

  </div>
</div>

<div class="toast" id="toast">
  <span class="check">✓</span>
  <span id="toastMsg">저장됐어요</span>
</div>

<!-- DETAIL MODAL (full view of a post) -->

<div class="detail-modal" id="detailModal" onclick="if(event.target===this) closeDetailModal()"></div>

<script>
  // VERSES
  const verses = [
    { kr: '너희는 먼저 그의 나라와 그의 의를 구하라<br>그리하면 이 모든 것을 너희에게 더하시리라', en: 'But seek first the Kingdom of God,<br>and his righteousness;<br>and all these things will be given to you as well.', ref: 'MATTHEW 6 : 33' },
    { kr: '오직 여호와를 앙망하는 자는 새 힘을 얻으리니<br>독수리가 날개치며 올라감 같을 것이요', en: 'But those who wait for Yahweh<br>will renew their strength.<br>They will mount up with wings like eagles.', ref: 'ISAIAH 40 : 31' },
    { kr: '여호와는 나의 목자시니<br>내게 부족함이 없으리로다', en: 'Yahweh is my shepherd;<br>I shall lack nothing.', ref: 'PSALM 23 : 1' },
    { kr: '수고하고 무거운 짐 진 자들아 다 내게로 오라<br>내가 너희를 쉬게 하리라', en: 'Come to me, all you who labor<br>and are heavily burdened,<br>and I will give you rest.', ref: 'MATTHEW 11 : 28' },
    { kr: '항상 기뻐하라<br>쉬지 말고 기도하라<br>범사에 감사하라', en: 'Rejoice always.<br>Pray without ceasing.<br>In everything give thanks.', ref: '1 THESS 5 : 16-18' }
  ];
  let currentIndex = 0;
  let currentLang = 'kr';

  // GROUPS
  const groups = [
    { id: 'family', name: '우리 가족', icon: '우', members: 4, type: 'private', desc: '엄마, 아빠, 동생' },
    { id: 'cell', name: '청년부 셀모임', icon: '청', members: 6, type: 'cell', desc: '매주 토요일' },
    { id: 'solo', name: '나의 묵상 노트', icon: '나', members: 1, type: 'solo', desc: '나만 보기' }
  ];
  let currentGroupId = 'family';
  let pendingGroupId = 'family';

  // MOCK POSTS (omitted some for brevity, same as before)
  const bgPalettes = [
    ['#FFB591', '#FFC9A1', '#FFAEC8'],
    ['#7EC8F5', '#B8E0F7', '#FFAEC8'],
    ['#A8E6CF', '#B8E0F7', '#C9B6F0'],
    ['#FFD93D', '#FFB591', '#FF7B6B'],
    ['#C9B6F0', '#9BB8E8', '#7EC8F5'],
    ['#FFAEC8', '#FFB591', '#FFD93D']
  ];
  const avatarColors = [
    'linear-gradient(135deg, #FF7B6B, #FFB591)',
    'linear-gradient(135deg, #7EC8F5, #C9B6F0)',
    'linear-gradient(135deg, #A8E6CF, #7EC8F5)',
    'linear-gradient(135deg, #FFD93D, #FFB591)',
    'linear-gradient(135deg, #C9B6F0, #FF7B6B)'
  ];
  const posts = [
    { author: '엄마', avatar: '엄', avatarColor: avatarColors[0], time: '오늘 08:00', verse: verses[0], bg: bgPalettes[0], groupIds: ['family'], isPublic: true, isVideo: false, likes: 12, liked: true, comments: 3 },
    { author: '아빠', avatar: '아', avatarColor: avatarColors[1], time: '오늘 06:30', verse: verses[1], bg: bgPalettes[1], groupIds: ['family'], isPublic: false, isVideo: false, likes: 5, liked: false, comments: 1 },
    { author: '나', avatar: '나', avatarColor: avatarColors[2], time: '오늘 11:00', verse: verses[2], bg: bgPalettes[2], groupIds: ['family', 'cell'], isPublic: false, isVideo: true, likes: 7, liked: false, comments: 2 },
    { author: '동생', avatar: '동', avatarColor: avatarColors[3], time: '어제 22:00', verse: verses[3], bg: bgPalettes[3], groupIds: ['family'], isPublic: false, isVideo: false, likes: 4, liked: false, comments: 0 },
    { author: '김지은', avatar: '지', avatarColor: avatarColors[4], time: '오늘 09:00', verse: verses[4], bg: bgPalettes[4], groupIds: ['cell'], isPublic: true, isVideo: false, likes: 8, liked: false, comments: 4 },
    { author: '박민서', avatar: '박', avatarColor: avatarColors[0], time: '오늘 07:00', verse: verses[0], bg: bgPalettes[5], groupIds: ['cell'], isPublic: false, isVideo: true, likes: 6, liked: true, comments: 1 },
    { author: '@grace_kr', avatar: 'G', avatarColor: avatarColors[3], time: '오늘 10:00', verse: verses[1], bg: bgPalettes[2], groupIds: [], isPublic: true, isVideo: false, likes: 234, liked: false, comments: 18 },
    { author: '@daily_word', avatar: 'D', avatarColor: avatarColors[4], time: '오늘 08:00', verse: verses[3], bg: bgPalettes[0], groupIds: [], isPublic: true, isVideo: true, likes: 156, liked: false, comments: 12 },
    { author: '@morning_grace', avatar: 'M', avatarColor: avatarColors[1], time: '오늘 06:00', verse: verses[2], bg: bgPalettes[5], groupIds: [], isPublic: true, isVideo: false, likes: 89, liked: false, comments: 7 }
  ];

  // ===== TAB =====
  function switchTab(pageId) {
    document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
    document.querySelector(`.tab[data-page="${pageId}"]`).classList.add('active');
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    document.getElementById(`page-${pageId}`).classList.add('active');
    if (pageId === 'feed') renderFeed();
    if (pageId === 'public') renderPublic();
  }

  function renderFeed() {
    const g = groups.find(x => x.id === currentGroupId);
    document.getElementById('feedHeaderAvatar').textContent = g.icon;
    document.getElementById('feedHeaderName').textContent = g.name;
    const list = posts.filter(p => p.groupIds.includes(currentGroupId));
    document.getElementById('feedHeaderSub').textContent = `${g.members}명 · 오늘 ${list.filter(p=>p.time.includes('오늘')).length}개의 묵상`;
    renderPostsInto('feedContainer', list);
  }
  function renderPublic() {
    renderPostsInto('publicContainer', posts.filter(p => p.isPublic));
  }

  function renderPostsInto(containerId, list) {
    const container = document.getElementById(containerId);
    container.innerHTML = '';
    if (list.length === 0) {
      container.innerHTML = `<div class="feed-empty"><div class="feed-empty-icon">✦</div>아직 묵상이 없어요<br>첫 번째 말씀을 남겨보세요</div>`;
      return;
    }
    // Group by 오늘/어제, each group → time label + grid
    const byLabel = {};
    list.forEach(p => {
      const label = p.time.includes('오늘') ? '오늘' : '어제';
      if (!byLabel[label]) byLabel[label] = [];
      byLabel[label].push(p);
    });
    ['오늘', '어제'].forEach(label => {
      if (!byLabel[label]) return;
      const ld = document.createElement('div');
      ld.className = 'feed-time-label';
      ld.textContent = label;
      container.appendChild(ld);
      const grid = document.createElement('div');
      grid.className = 'feed-grid';
      byLabel[label].forEach(p => grid.appendChild(createGridCard(p)));
      container.appendChild(grid);
    });
  }

  function createGridCard(p) {
    const card = document.createElement('div');
    card.className = 'grid-card';
    const bgStyle = `background: linear-gradient(135deg, ${p.bg[0]} 0%, ${p.bg[1]} 50%, ${p.bg[2]} 100%);`;
    const timeOnly = p.time.split(' ')[1] || p.time;
    const vidBadge = p.isVideo
      ? `<div class="grid-card-vidbadge"><svg viewBox="0 0 24 24"><polygon points="5 3 19 12 5 21 5 3"/></svg></div>`
      : '';
    // Truncate verse for grid view
    const versePreview = p.verse.kr.split('<br>')[0];
    card.innerHTML = `
      <div class="grid-card-bg" style="${bgStyle}"></div>
      <div class="grid-card-avatar" style="background: ${p.avatarColor};">${p.avatar}</div>
      ${vidBadge}
      <div class="grid-card-verse">
        <div class="grid-card-verse-text">${versePreview}</div>
        <div class="grid-card-verse-ref">${p.verse.ref.split(' : ')[0]}</div>
      </div>
      <div class="grid-card-stamp">${timeOnly}</div>
      <div class="grid-card-likes">
        <svg viewBox="0 0 24 24"><path d="M20.84 4.61a5.5 5.5 0 0 0-7.78 0L12 5.67l-1.06-1.06a5.5 5.5 0 0 0-7.78 7.78l1.06 1.06L12 21.23l7.78-7.78 1.06-1.06a5.5 5.5 0 0 0 0-7.78z"/></svg>
        ${p.likes}
      </div>
    `;
    card.onclick = () => openPostDetail(p);
    return card;
  }

  function toggleLike(el, e) {
    e.stopPropagation();
    el.classList.toggle('liked');
    const svg = el.querySelector('svg');
    const countEl = el.querySelector('span');
    let n = parseInt(countEl.textContent);
    if (el.classList.contains('liked')) {
      svg.setAttribute('fill', 'currentColor');
      countEl.textContent = (n + 1).toString();
    } else {
      svg.setAttribute('fill', 'none');
      countEl.textContent = (n - 1).toString();
    }
  }

  function openPostDetail(p) {
    let pillsHtml = '';
    p.groupIds.forEach(gid => {
      const g = groups.find(x => x.id === gid);
      if (g) {
        let cls = g.type === 'cell' ? 'cell' : 'private';
        pillsHtml += `<span class="detail-pill ${cls}">${g.name}</span>`;
      }
    });
    if (p.isPublic) pillsHtml += `<span class="detail-pill public">🌍 전체 공개</span>`;

    const bgStyle = `background: linear-gradient(135deg, ${p.bg[0]} 0%, ${p.bg[1]} 50%, ${p.bg[2]} 100%);`;
    const timeOnly = p.time.split(' ')[1] || p.time;

    // Sample comments based on count
    const sampleComments = [
      { name: '엄마', avatar: '엄', text: '오늘도 은혜로운 말씀이네 ♥', color: 'linear-gradient(135deg, #FF7B6B, #FFB591)' },
      { name: '아빠', avatar: '아', text: '아멘. 좋은 하루 보내자', color: 'linear-gradient(135deg, #7EC8F5, #C9B6F0)' },
      { name: '김지은', avatar: '지', text: '저도 오늘 이 말씀 묵상했어요!', color: 'linear-gradient(135deg, #C9B6F0, #FF7B6B)' }
    ];
    let commentsHtml = '';
    if (p.comments > 0) {
      for (let i = 0; i < Math.min(p.comments, 3); i++) {
        const c = sampleComments[i % sampleComments.length];
        commentsHtml += `
          <div class="detail-comment">
            <div class="detail-comment-avatar" style="background:${c.color}">${c.avatar}</div>
            <div class="detail-comment-body">
              <div class="detail-comment-name">${c.name}</div>
              <div class="detail-comment-text">${c.text}</div>
            </div>
          </div>
        `;
      }
    } else {
      commentsHtml = `<div class="detail-comment-empty">첫 번째 묵상 댓글을 남겨보세요</div>`;
    }

    const modal = document.getElementById('detailModal');
    modal.innerHTML = `
      <div class="detail-wrap">
        <div class="detail-topbar">
          <button class="detail-close" onclick="closeDetailModal()">✕</button>
          <div class="detail-user">
            <div class="detail-user-avatar" style="background:${p.avatarColor}">${p.avatar}</div>
            <div>
              <div class="detail-user-name">${p.author}</div>
              <div class="detail-user-time">${p.time}</div>
            </div>
          </div>
        </div>

        <div class="detail-card">
          <div class="detail-card-bg" style="${bgStyle}"></div>
          <div class="detail-card-stamp">${timeOnly}</div>
          <div class="detail-card-verse">
            <div class="detail-card-verse-text">${p.verse.kr}</div>
            <div class="detail-card-verse-ref">${p.verse.ref}</div>
          </div>
        </div>

        <div class="detail-pills">${pillsHtml}</div>

        <div class="detail-actions">
          <div class="detail-act ${p.liked ? 'liked' : ''}" onclick="toggleDetailLike(this)">
            <svg viewBox="0 0 24 24" fill="${p.liked ? 'currentColor' : 'none'}" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
              <path d="M20.84 4.61a5.5 5.5 0 0 0-7.78 0L12 5.67l-1.06-1.06a5.5 5.5 0 0 0-7.78 7.78l1.06 1.06L12 21.23l7.78-7.78 1.06-1.06a5.5 5.5 0 0 0 0-7.78z"/>
            </svg>
            <span>${p.likes}</span>
          </div>
          <div class="detail-act">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
              <path d="M21 11.5a8.38 8.38 0 0 1-.9 3.8 8.5 8.5 0 0 1-7.6 4.7 8.38 8.38 0 0 1-3.8-.9L3 21l1.9-5.7a8.38 8.38 0 0 1-.9-3.8 8.5 8.5 0 0 1 4.7-7.6 8.38 8.38 0 0 1 3.8-.9h.5a8.48 8.48 0 0 1 8 8v.5z"/>
            </svg>
            <span>${p.comments}</span>
          </div>
          <div class="detail-share">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
              <path d="M4 12v8a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2v-8"/>
              <polyline points="16 6 12 2 8 6"/>
              <line x1="12" y1="2" x2="12" y2="15"/>
            </svg>
          </div>
        </div>

        <div class="detail-comments-label">댓글 ${p.comments}개</div>
        ${commentsHtml}
      </div>
    `;
    modal.classList.add('show');
  }

  function closeDetailModal() {
    document.getElementById('detailModal').classList.remove('show');
  }

  function toggleDetailLike(el) {
    el.classList.toggle('liked');
    const svg = el.querySelector('svg');
    const countEl = el.querySelector('span');
    let n = parseInt(countEl.textContent);
    if (el.classList.contains('liked')) {
      svg.setAttribute('fill', 'currentColor');
      countEl.textContent = (n + 1).toString();
    } else {
      svg.setAttribute('fill', 'none');
      countEl.textContent = (n - 1).toString();
    }
  }

  // ===== CAMERA + FILTER + VIDEO =====
  let stream = null;
  let facingMode = 'environment';
  let lastUploadedImg = null;
  let currentMode = 'photo';  // 'photo' or 'video'
  let currentFilter = 'none';
  let mediaRecorder = null;
  let recordChunks = [];
  let recordedVideoUrl = null;
  let recordStartTime = null;
  let recordTimerInterval = null;
  let lastCapture = null; // { type: 'image'|'video', dataUrl: '...' }

  const viewfinder = document.getElementById('viewfinder');
  const video = document.getElementById('cameraStream');
  const snapshot = document.getElementById('snapshotImg');
  const filterLayer = document.getElementById('filterLayer');

  const FILTERS = {
    none: '',
    warm: 'saturate(1.15) sepia(0.18) brightness(1.05) contrast(1.05)',
    cool: 'saturate(1.1) hue-rotate(-12deg) brightness(1.02) contrast(1.05)',
    vintage: 'sepia(0.45) saturate(0.85) contrast(1.05) brightness(0.95)',
    bw: 'grayscale(1) contrast(1.1) brightness(1.05)',
    dreamy: 'saturate(1.2) brightness(1.1) contrast(0.95) blur(0.3px)',
    bright: 'saturate(1.3) brightness(1.1) contrast(1.1)'
  };

  function setFilter(el) {
    document.querySelectorAll('.filter-chip').forEach(c => c.classList.remove('active'));
    el.classList.add('active');
    currentFilter = el.dataset.filter;
    filterLayer.style.filter = FILTERS[currentFilter] || '';
  }

  function setMode(btn, mode) {
    document.querySelectorAll('.mode-btn').forEach(b => b.classList.remove('active'));
    btn.classList.add('active');
    currentMode = mode;
    const shutter = document.getElementById('shutterBtn');
    if (mode === 'video') {
      shutter.classList.add('video');
      document.getElementById('photoHint').innerHTML = '🎥 길게 누르거나 탭해서 짧은 영상 (최대 5초)';
    } else {
      shutter.classList.remove('video');
      document.getElementById('photoHint').innerHTML = '풍경 · 셀카 · 일상 · <span class="em">무엇이든</span> 자유롭게';
    }
  }

  function onViewfinderTap() {
    if (viewfinder.classList.contains('live')) return;
    if (viewfinder.classList.contains('cam-loading')) return;
    tryCamera();
  }

  async function tryCamera() {
    if (!navigator.mediaDevices || !navigator.mediaDevices.getUserMedia) {
      alert('이 브라우저는 카메라를 지원하지 않아요 😢');
      return;
    }
    viewfinder.classList.add('cam-loading');
    try {
      if (stream) stream.getTracks().forEach(t => t.stop());
      stream = await navigator.mediaDevices.getUserMedia({
        video: { facingMode: { ideal: facingMode } },
        audio: currentMode === 'video'
      });
      video.srcObject = stream;
      video.classList.toggle('mirrored', facingMode === 'user');
      await video.play();
      viewfinder.classList.remove('snapshot', 'cam-loading');
      viewfinder.classList.add('live');
    } catch (err) {
      viewfinder.classList.remove('cam-loading');
      let msg = '카메라를 켤 수 없어요 😢';
      if (err.name === 'NotAllowedError') msg = '카메라 권한이 거부되었어요.';
      else if (err.name === 'NotFoundError') msg = '카메라를 찾을 수 없어요.';
      alert(msg + '\n갤러리 버튼으로 사진을 올려도 돼요!');
    }
  }

  async function flipCamera() {
    if (!viewfinder.classList.contains('live')) { tryCamera(); return; }
    facingMode = (facingMode === 'environment') ? 'user' : 'environment';
    await tryCamera();
  }

  function loadImage(event) {
    const file = event.target.files[0];
    if (!file) return;
    const reader = new FileReader();
    reader.onload = (e) => {
      lastUploadedImg = e.target.result;
      snapshot.src = e.target.result;
      viewfinder.classList.remove('live', 'cam-loading');
      viewfinder.classList.add('snapshot');
    };
    reader.readAsDataURL(file);
  }

  // ===== SHUTTER =====
  function handleShutter() {
    if (currentMode === 'photo') {
      capturePhoto();
    } else {
      toggleRecording();
    }
  }

  function capturePhoto() {
    const flash = document.getElementById('flash');
    flash.classList.remove('fire');
    void flash.offsetWidth;
    flash.classList.add('fire');

    const canvas = document.getElementById('captureCanvas');
    const ctx = canvas.getContext('2d');
    const W = 900, H = 1200;
    canvas.width = W; canvas.height = H;

    const finish = () => {
      drawOverlay(ctx, W, H);
      const dataUrl = canvas.toDataURL('image/jpeg', 0.92);
      lastCapture = { type: 'image', dataUrl };
      showCard();
    };

    // Apply filter to canvas
    ctx.filter = FILTERS[currentFilter] || 'none';

    if (viewfinder.classList.contains('live') && video.videoWidth) {
      drawCover(ctx, video, W, H, facingMode === 'user');
      ctx.filter = 'none';
      finish();
    } else if (viewfinder.classList.contains('snapshot') && lastUploadedImg) {
      const img = new Image();
      img.onload = () => {
        drawCover(ctx, img, W, H, false);
        ctx.filter = 'none';
        finish();
      };
      img.src = lastUploadedImg;
    } else {
      const grad = ctx.createLinearGradient(0, 0, W, H);
      grad.addColorStop(0, '#FFB591'); grad.addColorStop(0.3, '#FFC9A1');
      grad.addColorStop(0.6, '#FFAEC8'); grad.addColorStop(0.85, '#C9B6F0');
      grad.addColorStop(1, '#9BB8E8');
      ctx.fillStyle = grad; ctx.fillRect(0, 0, W, H);
      ctx.filter = 'none';
      finish();
    }
  }

  // ===== VIDEO RECORDING =====
  function toggleRecording() {
    if (mediaRecorder && mediaRecorder.state === 'recording') {
      stopRecording();
    } else {
      startRecording();
    }
  }

  function startRecording() {
    if (!stream || !viewfinder.classList.contains('live')) {
      alert('먼저 카메라를 켜주세요!');
      return;
    }
    recordChunks = [];
    try {
      const mimeType = MediaRecorder.isTypeSupported('video/webm;codecs=vp9')
        ? 'video/webm;codecs=vp9'
        : MediaRecorder.isTypeSupported('video/webm')
        ? 'video/webm'
        : 'video/mp4';
      mediaRecorder = new MediaRecorder(stream, { mimeType });
    } catch (e) {
      mediaRecorder = new MediaRecorder(stream);
    }
    mediaRecorder.ondataavailable = (e) => {
      if (e.data.size > 0) recordChunks.push(e.data);
    };
    mediaRecorder.onstop = () => {
      const blob = new Blob(recordChunks, { type: mediaRecorder.mimeType });
      recordedVideoUrl = URL.createObjectURL(blob);
      lastCapture = { type: 'video', blob, url: recordedVideoUrl };
      const v = document.getElementById('cardCapturedVideo');
      v.src = recordedVideoUrl;
      document.getElementById('modalCard').classList.add('video');
      showCardMeta();
      setTimeout(() => document.getElementById('modal').classList.add('show'), 200);
    };
    mediaRecorder.start();
    viewfinder.classList.add('recording');
    document.getElementById('shutterBtn').classList.add('recording');
    recordStartTime = Date.now();
    updateRecTimer();
    recordTimerInterval = setInterval(updateRecTimer, 100);
    // Auto-stop at 5 sec
    setTimeout(() => {
      if (mediaRecorder && mediaRecorder.state === 'recording') {
        stopRecording();
      }
    }, 5000);
  }

  function stopRecording() {
    if (mediaRecorder && mediaRecorder.state === 'recording') {
      mediaRecorder.stop();
    }
    viewfinder.classList.remove('recording');
    document.getElementById('shutterBtn').classList.remove('recording');
    clearInterval(recordTimerInterval);
  }

  function updateRecTimer() {
    const elapsed = (Date.now() - recordStartTime) / 1000;
    const secs = elapsed.toFixed(1);
    document.getElementById('recTimer').textContent = `● ${secs}s / 5s`;
  }

  function drawCover(ctx, src, dw, dh, mirror) {
    const sw = src.videoWidth || src.naturalWidth;
    const sh = src.videoHeight || src.naturalHeight;
    const srcRatio = sw / sh, dstRatio = dw / dh;
    let sx, sy, sWidth, sHeight;
    if (srcRatio > dstRatio) {
      sHeight = sh; sWidth = sh * dstRatio;
      sx = (sw - sWidth) / 2; sy = 0;
    } else {
      sWidth = sw; sHeight = sw / dstRatio;
      sx = 0; sy = (sh - sHeight) / 2;
    }
    ctx.save();
    if (mirror) { ctx.translate(dw, 0); ctx.scale(-1, 1); }
    ctx.drawImage(src, sx, sy, sWidth, sHeight, 0, 0, dw, dh);
    ctx.restore();
  }

  function drawOverlay(ctx, W, H) {
    ctx.filter = 'none';
    const v = verses[currentIndex];
    const text = currentLang === 'kr' ? v.kr : v.en;
    const vg = ctx.createRadialGradient(W/2, H/2, H*0.3, W/2, H/2, H*0.75);
    vg.addColorStop(0, 'rgba(0,0,0,0)');
    vg.addColorStop(1, 'rgba(60,30,50,0.25)');
    ctx.fillStyle = vg; ctx.fillRect(0, 0, W, H);
    ctx.fillStyle = '#fff';
    ctx.textAlign = 'center';
    ctx.textBaseline = 'middle';
    ctx.shadowColor = 'rgba(60,30,50,0.6)';
    const lines = text.split('<br>');
    const lineHeight = currentLang === 'kr' ? 66 : 58;
    const totalH = lines.length * lineHeight;
    const startY = H/2 - totalH/2 + lineHeight/2 - 10;
    ctx.font = '32px sans-serif';
    ctx.shadowBlur = 10;
    ctx.fillText('✦', W/2, startY - lineHeight/2 - 50);
    ctx.font = currentLang === 'kr' ? '400 38px "Gowun Batang", serif' : 'italic 400 36px "Fraunces", serif';
    ctx.shadowBlur = 14;
    ctx.shadowOffsetY = 2;
    lines.forEach((line, i) => ctx.fillText(line, W/2, startY + i * lineHeight));
    ctx.shadowBlur = 0; ctx.shadowOffsetY = 0;
    const refY = startY + totalH + 40;
    ctx.font = 'italic 26px "Fraunces", serif';
    const refWidth = ctx.measureText(v.ref).width;
    const pillW = refWidth + 36;
    ctx.fillStyle = 'rgba(255,255,255,0.22)';
    roundRect(ctx, W/2 - pillW/2, refY - 21, pillW, 42, 21);
    ctx.fill();
    ctx.fillStyle = '#fff';
    ctx.shadowColor = 'rgba(60,30,50,0.5)';
    ctx.shadowBlur = 6;
    ctx.fillText(v.ref, W/2, refY);
    ctx.shadowBlur = 0;
    const now = new Date();
    const hh = String(now.getHours()).padStart(2, '0');
    const mm = String(now.getMinutes()).padStart(2, '0');
    ctx.font = 'italic 20px "Fraunces", serif';
    ctx.fillStyle = 'rgba(255,255,255,0.95)';
    ctx.textAlign = 'left';
    ctx.shadowColor = 'rgba(60,30,50,0.6)';
    ctx.shadowBlur = 6;
    ctx.fillText(`${hh}:${mm} · ${now.getMonth()+1}.${now.getDate()}`, 60, 56);
    ctx.shadowBlur = 0;
  }

  function roundRect(ctx, x, y, w, h, r) {
    ctx.beginPath();
    ctx.moveTo(x + r, y);
    ctx.arcTo(x + w, y, x + w, y + h, r);
    ctx.arcTo(x + w, y + h, x, y + h, r);
    ctx.arcTo(x, y + h, x, y, r);
    ctx.arcTo(x, y, x + w, y, r);
    ctx.closePath();
  }

  function showCardMeta() {
    const now = new Date();
    const hh = String(now.getHours() % 12 || 12).padStart(2, '0');
    const mm = String(now.getMinutes()).padStart(2, '0');
    const months = ['JAN','FEB','MAR','APR','MAY','JUN','JUL','AUG','SEP','OCT','NOV','DEC'];
    document.getElementById('cardTime').textContent =
      `${hh} : ${mm} · ${months[now.getMonth()]} ${now.getDate()}`;
    document.getElementById('downloadSub').textContent =
      lastCapture && lastCapture.type === 'video'
        ? '영상을 내 갤러리에 다운로드'
        : '사진을 내 갤러리에 다운로드';
    document.getElementById('downloadRow') ? null : null;
    postSelection = new Set([currentGroupId]);
    renderPostGroups();
    updatePostCount();
  }

  function showCard() {
    document.getElementById('modalCard').classList.remove('video');
    document.getElementById('cardCapturedImg').src = lastCapture.dataUrl;
    showCardMeta();
    setTimeout(() => document.getElementById('modal').classList.add('show'), 300);
  }

  function closeModal() {
    document.getElementById('modal').classList.remove('show');
    const v = document.getElementById('cardCapturedVideo');
    v.pause();
  }

  // DOWNLOAD
  function downloadCapture() {
    if (!lastCapture) return;
    const a = document.createElement('a');
    const stamp = new Date().toISOString().replace(/[:.]/g, '-').slice(0, 19);
    if (lastCapture.type === 'image') {
      a.href = lastCapture.dataUrl;
      a.download = `wordlog-${stamp}.jpg`;
    } else {
      a.href = lastCapture.url;
      a.download = `wordlog-${stamp}.webm`;
    }
    document.body.appendChild(a);
    a.click();
    document.body.removeChild(a);
    showToast(lastCapture.type === 'image' ? '📷 갤러리에 저장됐어요!' : '🎥 영상이 저장됐어요!');
  }

  function showToast(msg) {
    document.getElementById('toastMsg').textContent = msg;
    const t = document.getElementById('toast');
    t.classList.add('show');
    setTimeout(() => t.classList.remove('show'), 2200);
  }

  // POST GROUPS
  let postSelection = new Set();
  function renderPostGroups() {
    const wrap = document.getElementById('postGroups');
    wrap.innerHTML = '';
    groups.forEach(g => {
      const item = document.createElement('div');
      const isSelected = postSelection.has(g.id);
      item.className = 'post-group-item' + (isSelected ? ' selected' : '') + ` ${g.type}`;
      item.onclick = () => {
        if (postSelection.has(g.id)) postSelection.delete(g.id);
        else postSelection.add(g.id);
        renderPostGroups();
        updatePostCount();
      };
      item.innerHTML = `
        <div class="group-avatar">${g.icon}</div>
        <div class="post-group-info">
          <div class="post-group-name">${g.name}</div>
          <div class="post-group-meta">${g.members}명 · ${g.desc}</div>
        </div>
        <div class="post-group-check">${isSelected ? '✓' : ''}</div>
      `;
      wrap.appendChild(item);
    });
    const pubItem = document.createElement('div');
    const isPubSelected = postSelection.has('public');
    pubItem.className = 'post-group-item public' + (isPubSelected ? ' selected' : '');
    pubItem.onclick = () => {
      if (postSelection.has('public')) postSelection.delete('public');
      else postSelection.add('public');
      renderPostGroups();
      updatePostCount();
    };
    pubItem.innerHTML = `
      <div class="group-avatar">🌍</div>
      <div class="post-group-info">
        <div class="post-group-name">전체 피드</div>
        <div class="post-group-meta">모든 워드로그 사용자가 봐요</div>
      </div>
      <div class="post-group-check">${isPubSelected ? '✓' : ''}</div>
    `;
    wrap.appendChild(pubItem);
  }
  function updatePostCount() {
    const n = postSelection.size;
    document.getElementById('postCount').textContent = n;
    const btn = document.getElementById('saveBtn');
    btn.disabled = n === 0;
    btn.textContent = n === 0 ? '선택해주세요' : `${n}곳에 저장 ✨`;
  }

  function saveAndClose() {
    if (postSelection.size === 0) return;
    const names = [];
    postSelection.forEach(id => {
      if (id === 'public') names.push('전체 피드');
      else {
        const g = groups.find(x => x.id === id);
        if (g) names.push(g.name);
      }
    });
    closeModal();
    setTimeout(() => showToast(`✨ ${names.join(', ')}에 저장!`), 200);
  }

  // VERSE LANG
  function renderVerse() {
    const v = verses[currentIndex];
    const t = document.getElementById('verseText');
    t.classList.add('fading');
    setTimeout(() => {
      if (currentLang === 'kr') {
        t.innerHTML = v.kr;
        t.classList.remove('en');
        document.getElementById('langHint').innerHTML = '탭하면 EN ▸';
      } else {
        t.innerHTML = v.en;
        t.classList.add('en');
        document.getElementById('langHint').innerHTML = '◂ KR 탭';
      }
      document.getElementById('verseRef').textContent = v.ref;
      t.classList.remove('fading');
    }, 200);
  }
  document.getElementById('verseText').addEventListener('click', (e) => {
    e.stopPropagation();
    currentLang = (currentLang === 'kr') ? 'en' : 'kr';
    renderVerse();
  });

  // INTERVAL
  function changeInterval(btn, hours) {
    document.querySelectorAll('.interval-btn').forEach(b => b.classList.remove('active'));
    btn.classList.add('active');
    document.getElementById('intervalLabel').textContent = hours + '시간';
    updateNextTime(hours);
  }
  function updateNextTime(hours) {
    const now = new Date();
    const next = new Date(now);
    next.setHours(now.getHours() + (hours || 1), 0, 0, 0);
    const hh = String(next.getHours()).padStart(2, '0');
    document.getElementById('nextTime').textContent = `${hh} : 00`;
  }

  // GROUP SHEET
  function renderGroupList() {
    const list = document.getElementById('groupList');
    list.innerHTML = '';
    groups.forEach(g => {
      const item = document.createElement('div');
      item.className = 'group-item' + (g.id === pendingGroupId ? ' selected' : '') + ` ${g.type}`;
      item.onclick = () => { pendingGroupId = g.id; renderGroupList(); };
      let pillHtml = g.type === 'solo' ? '<span class="privacy-pill private">나만</span>' : '<span class="privacy-pill private">비공개</span>';
      item.innerHTML = `
        <div class="group-avatar">${g.icon}</div>
        <div class="group-item-info">
          <div class="group-item-name">${g.name}</div>
          <div class="group-item-meta">
            ${pillHtml}
            <span>${g.members}명</span>
            <span>· ${g.desc}</span>
          </div>
        </div>
        <div class="group-item-check">${g.id === pendingGroupId ? '✓' : ''}</div>
      `;
      list.appendChild(item);
    });
  }
  function openGroupSheet() {
    pendingGroupId = currentGroupId;
    renderGroupList();
    document.getElementById('groupSheet').classList.add('show');
  }
  function closeGroupSheet() { document.getElementById('groupSheet').classList.remove('show'); }
  function confirmGroup() {
    currentGroupId = pendingGroupId;
    const g = groups.find(x => x.id === currentGroupId);
    document.getElementById('groupAvatar').textContent = g.icon;
    document.getElementById('groupName').textContent = g.name;
    const pill = document.getElementById('privacyPill');
    pill.className = 'privacy-pill private';
    pill.textContent = g.type === 'solo' ? '나만 보기' : '비공개';
    document.getElementById('groupMembers').textContent = g.members + '명';
    closeGroupSheet();
    if (document.getElementById('page-feed').classList.contains('active')) renderFeed();
  }

  function setTheme(el) {
    document.querySelectorAll('.theme-chip').forEach(c => c.classList.remove('active'));
    el.classList.add('active');
  }
  function updateTime() {
    const now = new Date();
    const hh = now.getHours();
    const h12 = hh % 12 || 12;
    const mm = String(now.getMinutes()).padStart(2, '0');
    document.getElementById('currentTime').textContent = `${String(h12).padStart(2,'0')}:${mm}`;
    document.getElementById('vfTime').textContent = `${String(hh).padStart(2,'0')}:${mm} · ${now.getMonth()+1}.${now.getDate()}`;
  }
  updateTime();
  window.setInterval(updateTime, 1000);
  updateNextTime(1);

  window.addEventListener('load', () => {
    setTimeout(() => { tryCamera().catch(() => {}); }, 300);
  });
</script>

</body>
</html>