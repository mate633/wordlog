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
    --bg-warm: #FFEDDB;
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
    background: var(--bg);
    color: var(--ink);
    -webkit-font-smoothing: antialiased;
    background-image:
      radial-gradient(at 15% 5%, rgba(255, 181, 145, 0.35) 0%, transparent 45%),
      radial-gradient(at 85% 10%, rgba(126, 200, 245, 0.25) 0%, transparent 45%),
      radial-gradient(at 50% 95%, rgba(255, 217, 61, 0.2) 0%, transparent 50%);
  }
  .app {
    max-width: 480px;
    margin: 0 auto;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    position: relative;
  }

.deco {
position: absolute;
pointer-events: none;
z-index: 0;
animation: bob 6s ease-in-out infinite;
}
.deco.star1 { top: 60px; right: 30px; font-size: 16px; color: var(–sunny); animation-delay: 0s; }
.deco.star2 { top: 140px; left: 18px; font-size: 12px; color: var(–coral); animation-delay: 1.5s; }
.deco.heart1 { top: 90px; left: 30px; font-size: 14px; color: var(–coral); animation-delay: 0.8s; opacity: 0.7; }
@keyframes bob {
0%, 100% { transform: translateY(0) rotate(0deg); }
50% { transform: translateY(-6px) rotate(8deg); }
}

.header {
padding: 20px 22px 16px;
display: flex;
justify-content: space-between;
align-items: center;
position: relative;
z-index: 1;
}
.logo-wrap { display: flex; align-items: center; gap: 8px; }
.logo-mark {
width: 36px; height: 36px;
background: linear-gradient(135deg, var(–coral) 0%, var(–peach) 100%);
border-radius: 12px;
display: flex;
align-items: center;
justify-content: center;
color: white;
font-family: ‘Fraunces’, serif;
font-weight: 600;
font-style: italic;
font-size: 18px;
box-shadow: 0 4px 12px -2px rgba(255, 123, 107, 0.5);
transform: rotate(-4deg);
}
.logo-text {
font-family: ‘Fraunces’, serif;
font-size: 22px;
font-weight: 500;
font-style: italic;
color: var(–ink);
letter-spacing: -0.3px;
}
.logo-text .accent { color: var(–coral); }
.logo-kr {
font-size: 10px;
letter-spacing: 3px;
color: var(–muted);
margin-top: 1px;
}
.time-badge {
font-family: ‘Fraunces’, serif;
font-size: 14px;
color: var(–ink);
background: white;
border: 1.5px solid var(–line);
padding: 8px 14px;
border-radius: 100px;
display: flex;
align-items: center;
gap: 7px;
box-shadow: 0 2px 8px -2px rgba(61, 43, 37, 0.08);
}
.time-dot {
width: 7px; height: 7px;
background: var(–coral);
border-radius: 50%;
animation: pulse 2s infinite;
}
@keyframes pulse {
0%, 100% { opacity: 1; box-shadow: 0 0 0 0 rgba(255, 123, 107, 0.5); }
50% { opacity: 0.6; box-shadow: 0 0 0 6px rgba(255, 123, 107, 0); }
}

.tabs {
display: flex;
padding: 8px 22px 8px;
gap: 6px;
position: relative;
z-index: 1;
}
.tab {
flex: 1;
text-align: center;
padding: 10px 0;
font-size: 13px;
color: var(–muted);
cursor: pointer;
border-radius: 100px;
transition: all 0.3s;
}
.tab.active {
color: var(–ink);
background: white;
font-weight: 700;
box-shadow: 0 2px 8px -2px rgba(61, 43, 37, 0.1);
}

/* –– TOP BAR: Group + Interval –– */
.top-bar {
margin: 4px 22px 0;
display: flex;
gap: 8px;
position: relative;
z-index: 1;
}
.group-selector {
flex: 1;
background: white;
border: 1.5px solid var(–line);
border-radius: 14px;
padding: 9px 13px;
display: flex;
align-items: center;
gap: 8px;
cursor: pointer;
transition: all 0.2s;
}
.group-selector:active { transform: scale(0.98); }
.group-avatar {
width: 26px; height: 26px;
border-radius: 50%;
background: linear-gradient(135deg, var(–coral), var(–peach));
color: white;
display: flex;
align-items: center;
justify-content: center;
font-size: 12px;
font-weight: 700;
flex-shrink: 0;
}
.group-info { flex: 1; min-width: 0; }
.group-name {
font-size: 12px;
font-weight: 700;
color: var(–ink);
line-height: 1.2;
overflow: hidden;
text-overflow: ellipsis;
white-space: nowrap;
}
.group-meta {
font-size: 10px;
color: var(–muted);
margin-top: 1px;
display: flex;
align-items: center;
gap: 4px;
}
.privacy-pill {
padding: 1px 6px;
border-radius: 100px;
font-size: 9px;
font-weight: 700;
letter-spacing: 0.3px;
}
.privacy-pill.private { background: rgba(126, 200, 245, 0.25); color: #2D7AB5; }
.privacy-pill.public { background: rgba(255, 217, 61, 0.35); color: #8B6F00; }
.group-chevron { color: var(–muted); font-size: 14px; }

.interval-toggle {
background: white;
border: 1.5px solid var(–line);
border-radius: 14px;
padding: 4px;
display: flex;
gap: 2px;
}
.interval-btn {
padding: 6px 10px;
background: transparent;
border: none;
border-radius: 10px;
font-family: inherit;
font-size: 11px;
font-weight: 700;
color: var(–muted);
cursor: pointer;
transition: all 0.2s;
}
.interval-btn.active {
background: linear-gradient(135deg, var(–coral), var(–peach));
color: white;
box-shadow: 0 2px 6px -1px rgba(255, 123, 107, 0.4);
}

/* VIEWFINDER */
.viewfinder {
position: relative;
margin: 12px 22px 0;
aspect-ratio: 3/4;
border-radius: 28px;
overflow: hidden;
background: #1a1816;
box-shadow:
0 20px 40px -15px rgba(255, 123, 107, 0.25),
0 8px 16px -8px rgba(61, 43, 37, 0.15);
z-index: 1;
}
.demo-bg {
position: absolute;
inset: 0;
background:
linear-gradient(180deg, rgba(255, 200, 150, 0.15) 0%, transparent 40%, rgba(120, 80, 100, 0.3) 100%),
linear-gradient(135deg, #FFB591 0%, #FFC9A1 25%, #FFAEC8 55%, #C9B6F0 85%, #9BB8E8 100%);
animation: shift 16s ease-in-out infinite alternate;
}
.demo-bg::after {
content: ‘’;
position: absolute;
inset: 0;
background-image:
radial-gradient(ellipse at 25% 25%, rgba(255, 245, 220, 0.55) 0%, transparent 45%),
radial-gradient(ellipse at 75% 70%, rgba(255, 180, 200, 0.4) 0%, transparent 45%);
animation: float 12s ease-in-out infinite alternate;
}
@keyframes shift {
0% { filter: hue-rotate(0deg) saturate(1); }
100% { filter: hue-rotate(20deg) saturate(1.1); }
}
@keyframes float {
0% { transform: translate(0, 0) scale(1); }
100% { transform: translate(-3%, 3%) scale(1.05); }
}
#cameraStream {
position: absolute;
inset: 0;
width: 100%; height: 100%;
object-fit: cover;
display: none;
background: #000;
}
#cameraStream.mirrored { transform: scaleX(-1); }
.viewfinder.live #cameraStream { display: block; }
.viewfinder.live .demo-bg { display: none; }
#snapshotImg {
position: absolute;
inset: 0;
width: 100%; height: 100%;
object-fit: cover;
display: none;
}
.viewfinder.snapshot #snapshotImg { display: block; }
.viewfinder.snapshot #cameraStream,
.viewfinder.snapshot .demo-bg { display: none; }

.mode-badge {
position: absolute;
top: 16px;
right: 16px;
display: flex;
align-items: center;
gap: 6px;
color: white;
font-size: 10px;
letter-spacing: 1.5px;
z-index: 2;
padding: 5px 11px;
background: rgba(255, 255, 255, 0.25);
border-radius: 100px;
backdrop-filter: blur(8px);
border: 1px solid rgba(255,255,255,0.3);
}
.mode-dot {
width: 6px; height: 6px;
border-radius: 50%;
background: var(–sunny);
}
.viewfinder.live .mode-dot { background: #FF5544; animation: pulse 1.2s infinite; }
.viewfinder.live .mode-text::after { content: ‘LIVE’; }
.viewfinder:not(.live) .mode-text::after { content: ‘PREVIEW’; }

.vf-meta {
position: absolute;
top: 16px;
left: 16px;
font-family: ‘Fraunces’, serif;
color: white;
font-size: 11px;
letter-spacing: 1.5px;
text-shadow: 0 1px 3px rgba(0,0,0,0.3);
z-index: 2;
padding: 5px 10px;
background: rgba(255,255,255,0.2);
border-radius: 100px;
backdrop-filter: blur(8px);
}

.verse-overlay {
position: absolute;
inset: 0;
display: flex;
flex-direction: column;
justify-content: center;
align-items: center;
padding: 50px 36px;
z-index: 3;
}
.verse-sparkle {
font-size: 16px;
margin-bottom: 8px;
filter: drop-shadow(0 1px 3px rgba(0,0,0,0.3));
animation: twinkle 2.5s ease-in-out infinite;
}
@keyframes twinkle {
0%, 100% { opacity: 1; transform: scale(1) rotate(0deg); }
50% { opacity: 0.7; transform: scale(1.15) rotate(15deg); }
}
.verse-text {
font-family: ‘Gowun Batang’, serif;
font-weight: 400;
font-size: 17px;
line-height: 1.9;
color: #ffffff;
text-align: center;
text-shadow: 0 2px 12px rgba(60, 30, 50, 0.5), 0 1px 3px rgba(60, 30, 50, 0.7);
letter-spacing: 0.2px;
word-break: keep-all;
max-width: 320px;
cursor: pointer;
transition: opacity 0.3s;
}
.verse-text.en {
font-family: ‘Fraunces’, serif;
font-style: italic;
font-size: 16px;
line-height: 1.7;
}
.verse-text.fading {
opacity: 0;
}
.verse-ref {
font-family: ‘Fraunces’, serif;
font-style: italic;
font-size: 13px;
color: rgba(255, 255, 255, 0.95);
margin-top: 16px;
letter-spacing: 1.5px;
text-shadow: 0 1px 6px rgba(60, 30, 50, 0.5);
padding: 4px 12px;
background: rgba(255,255,255,0.2);
border-radius: 100px;
backdrop-filter: blur(4px);
}
.lang-hint {
margin-top: 10px;
font-size: 9px;
color: rgba(255,255,255,0.7);
letter-spacing: 1.5px;
padding: 3px 8px;
background: rgba(0,0,0,0.15);
border-radius: 100px;
backdrop-filter: blur(4px);
}

.flash {
position: absolute;
inset: 0;
background: white;
opacity: 0;
pointer-events: none;
z-index: 5;
}
.flash.fire { animation: flash 0.4s ease-out; }
@keyframes flash {
0% { opacity: 0; }
20% { opacity: 0.85; }
100% { opacity: 0; }
}
.demo-hint {
position: absolute;
bottom: 14px;
left: 50%;
transform: translateX(-50%);
z-index: 2;
font-size: 11px;
color: white;
padding: 6px 14px;
background: rgba(255, 123, 107, 0.85);
border-radius: 100px;
backdrop-filter: blur(4px);
white-space: nowrap;
animation: bounce 2s ease-in-out infinite;
}
@keyframes bounce {
0%, 100% { transform: translateX(-50%) translateY(0); }
50% { transform: translateX(-50%) translateY(-4px); }
}
.viewfinder.live .demo-hint,
.viewfinder.snapshot .demo-hint { display: none; }

.controls {
padding: 18px 22px 14px;
display: flex;
align-items: center;
justify-content: space-between;
gap: 16px;
position: relative;
z-index: 1;
}
.ctrl-side {
flex: 1;
display: flex;
align-items: center;
}
.ctrl-side.right { justify-content: flex-end; }
.icon-btn {
width: 50px; height: 50px;
border-radius: 18px;
background: white;
border: none;
display: flex;
align-items: center;
justify-content: center;
cursor: pointer;
transition: transform 0.2s;
color: var(–ink-soft);
box-shadow: 0 4px 12px -3px rgba(61, 43, 37, 0.15);
position: relative;
}
.icon-btn:active { transform: scale(0.9) rotate(-5deg); }
.icon-btn svg { width: 22px; height: 22px; }
.icon-btn.accent { background: linear-gradient(135deg, var(–sky) 0%, var(–sky-soft) 100%); color: white; }

.shutter {
width: 80px; height: 80px;
border-radius: 50%;
background: white;
border: none;
display: flex;
align-items: center;
justify-content: center;
cursor: pointer;
position: relative;
transition: transform 0.15s;
box-shadow: 0 6px 20px -4px rgba(255, 123, 107, 0.45);
}
.shutter:active { transform: scale(0.92); }
.shutter-inner {
width: 60px; height: 60px;
border-radius: 50%;
background: linear-gradient(135deg, var(–coral) 0%, var(–peach) 60%, var(–sunny) 100%);
}
.shutter::after {
content: ‘’;
position: absolute;
inset: -6px;
border-radius: 50%;
border: 2px solid var(–coral);
opacity: 0.3;
}

.photo-hint {
text-align: center;
font-size: 11px;
color: var(–muted);
padding: 0 22px 12px;
}
.photo-hint .em { color: var(–coral); font-weight: 700; }

.themes {
padding: 6px 22px 16px;
display: flex;
gap: 8px;
overflow-x: auto;
-webkit-overflow-scrolling: touch;
scrollbar-width: none;
position: relative;
z-index: 1;
}
.themes::-webkit-scrollbar { display: none; }
.theme-chip {
flex-shrink: 0;
padding: 9px 16px;
border-radius: 100px;
font-size: 13px;
color: var(–ink);
background: white;
cursor: pointer;
white-space: nowrap;
transition: all 0.2s;
box-shadow: 0 2px 6px -2px rgba(61, 43, 37, 0.1);
border: 1.5px solid transparent;
}
.theme-chip:nth-child(1).active { background: linear-gradient(135deg, var(–coral), var(–peach)); color: white; }
.theme-chip:nth-child(2).active { background: linear-gradient(135deg, var(–sky), var(–lavender)); color: white; }
.theme-chip:nth-child(3).active { background: linear-gradient(135deg, var(–sunny), var(–peach)); color: var(–ink); }
.theme-chip:nth-child(4).active { background: linear-gradient(135deg, var(–mint), var(–sky-soft)); color: var(–ink); }
.theme-chip:nth-child(5).active { background: linear-gradient(135deg, var(–lavender), var(–coral)); color: white; }
.theme-chip:nth-child(6).active { background: linear-gradient(135deg, var(–peach), var(–coral)); color: white; }

.info-strip {
padding: 0 22px 12px;
text-align: center;
position: relative;
z-index: 1;
}
.info-line {
color: var(–ink);
font-size: 13px;
margin-bottom: 3px;
}
.info-line .em { color: var(–coral); font-weight: 700; }
.info-sub {
font-family: ‘Fraunces’, serif;
font-style: italic;
font-size: 11px;
color: var(–muted);
letter-spacing: 1.5px;
}

/* SHEET (group selector) */
.sheet {
position: fixed;
inset: 0;
background: rgba(60, 30, 50, 0.6);
backdrop-filter: blur(8px);
z-index: 90;
display: none;
align-items: flex-end;
justify-content: center;
}
.sheet.show {
display: flex;
animation: fadeIn 0.3s;
}
.sheet-content {
background: var(–paper);
width: 100%;
max-width: 480px;
border-radius: 28px 28px 0 0;
padding: 14px 22px 28px;
animation: slideUp 0.35s cubic-bezier(0.16, 1, 0.3, 1);
}
@keyframes slideUp {
from { transform: translateY(100%); }
to { transform: translateY(0); }
}
.sheet-handle {
width: 40px; height: 4px;
background: var(–line);
border-radius: 100px;
margin: 0 auto 14px;
}
.sheet-title {
font-weight: 700;
font-size: 16px;
color: var(–ink);
text-align: center;
margin-bottom: 6px;
}
.sheet-sub {
font-size: 11px;
color: var(–muted);
text-align: center;
margin-bottom: 16px;
}
.group-list {
display: flex;
flex-direction: column;
gap: 8px;
margin-bottom: 14px;
}
.group-item {
background: white;
border: 1.5px solid var(–line);
border-radius: 16px;
padding: 12px;
display: flex;
align-items: center;
gap: 10px;
cursor: pointer;
transition: all 0.2s;
}
.group-item:active { transform: scale(0.98); }
.group-item.selected {
border-color: var(–coral);
background: rgba(255, 123, 107, 0.06);
}
.group-item .group-avatar { width: 36px; height: 36px; font-size: 14px; }
.group-item.public .group-avatar { background: linear-gradient(135deg, var(–sunny), var(–peach)); }
.group-item.solo .group-avatar { background: linear-gradient(135deg, var(–sky), var(–lavender)); }
.group-item-info { flex: 1; }
.group-item-name { font-size: 14px; font-weight: 700; color: var(–ink); }
.group-item-meta { font-size: 11px; color: var(–muted); margin-top: 2px; display: flex; gap: 6px; align-items: center; }
.group-item-check {
width: 20px; height: 20px;
border-radius: 50%;
border: 1.5px solid var(–line);
display: flex; align-items: center; justify-content: center;
color: white;
font-size: 12px;
}
.group-item.selected .group-item-check {
background: var(–coral);
border-color: var(–coral);
}
.sheet-actions {
display: flex;
gap: 8px;
margin-top: 6px;
}
.sheet-btn {
flex: 1;
padding: 12px;
border: 1.5px solid var(–line);
background: white;
border-radius: 100px;
font-family: inherit;
font-size: 13px;
font-weight: 700;
color: var(–ink);
cursor: pointer;
}
.sheet-btn.primary {
background: linear-gradient(135deg, var(–coral), var(–peach));
color: white;
border-color: transparent;
box-shadow: 0 4px 12px -2px rgba(255, 123, 107, 0.45);
}

/* Captured card modal */
.modal {
position: fixed;
inset: 0;
background: rgba(60, 30, 50, 0.75);
backdrop-filter: blur(10px);
z-index: 100;
display: none;
align-items: center;
justify-content: center;
padding: 24px;
}
.modal.show { display: flex; animation: fadeIn 0.4s; }
@keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

.card {
background: var(–paper);
width: 100%;
max-width: 360px;
padding: 24px 22px 20px;
border-radius: 28px;
box-shadow: 0 40px 80px -20px rgba(0,0,0,0.5);
animation: cardIn 0.6s cubic-bezier(0.34, 1.56, 0.64, 1);
}
@keyframes cardIn {
from { transform: translateY(30px) scale(0.92) rotate(-2deg); opacity: 0; }
to { transform: translateY(0) scale(1) rotate(0deg); opacity: 1; }
}
.card-img {
aspect-ratio: 3/4;
border-radius: 20px;
overflow: hidden;
position: relative;
margin-bottom: 14px;
background: #2a2622;
}
#cardCapturedImg {
position: absolute; inset: 0;
width: 100%; height: 100%;
object-fit: cover;
}
.card-meta {
display: flex;
justify-content: space-between;
align-items: center;
padding: 0 6px;
margin-bottom: 12px;
gap: 8px;
}
.card-meta-left {
font-family: ‘Fraunces’, serif;
font-style: italic;
font-size: 13px;
color: var(–ink);
letter-spacing: 1px;
}
.card-group-badge {
font-size: 11px;
color: var(–ink);
font-weight: 700;
padding: 3px 10px;
border-radius: 100px;
}
.card-group-badge.private { background: rgba(126, 200, 245, 0.25); color: #2D7AB5; }
.card-group-badge.public { background: rgba(255, 217, 61, 0.4); color: #8B6F00; }

/* Public toggle row in modal */
.publish-row {
background: rgba(255, 123, 107, 0.06);
border: 1.5px solid rgba(255, 123, 107, 0.15);
border-radius: 16px;
padding: 12px 14px;
margin-bottom: 12px;
display: flex;
align-items: center;
gap: 10px;
}
.publish-info {
flex: 1;
}
.publish-title {
font-size: 12px;
font-weight: 700;
color: var(–ink);
}
.publish-sub {
font-size: 10px;
color: var(–muted);
margin-top: 1px;
}
/* Toggle switch */
.switch {
position: relative;
width: 44px; height: 24px;
background: var(–line);
border-radius: 100px;
cursor: pointer;
transition: background 0.2s;
flex-shrink: 0;
}
.switch::after {
content: ‘’;
position: absolute;
top: 2px; left: 2px;
width: 20px; height: 20px;
background: white;
border-radius: 50%;
transition: transform 0.2s;
box-shadow: 0 2px 4px rgba(0,0,0,0.2);
}
.switch.on { background: linear-gradient(135deg, var(–coral), var(–peach)); }
.switch.on::after { transform: translateX(20px); }

.card-actions {
display: flex;
gap: 8px;
}
.btn {
flex: 1;
padding: 14px;
border: none;
background: rgba(255, 123, 107, 0.1);
color: var(–ink);
font-family: inherit;
font-size: 14px;
cursor: pointer;
border-radius: 100px;
font-weight: 700;
transition: transform 0.15s;
}
.btn:active { transform: scale(0.95); }
.btn.primary {
background: linear-gradient(135deg, var(–coral) 0%, var(–peach) 100%);
color: white;
box-shadow: 0 4px 12px -2px rgba(255, 123, 107, 0.5);
}

#fileInput { display: none; }

.dev-note {
margin: 4px 22px 16px;
padding: 12px 16px;
background: linear-gradient(135deg, rgba(126, 200, 245, 0.15) 0%, rgba(255, 217, 61, 0.15) 100%);
border: 1.5px solid rgba(126, 200, 245, 0.3);
border-radius: 18px;
font-size: 12px;
color: var(–ink-soft);
line-height: 1.6;
position: relative;
z-index: 1;
}
.dev-note b { color: var(–coral-deep); }

.hint {
text-align: center;
font-size: 11px;
color: var(–muted);
padding: 4px 22px 22px;
letter-spacing: 1.5px;
font-family: ‘Fraunces’, serif;
font-style: italic;
position: relative;
z-index: 1;
}
.hint .heart { color: var(–coral); margin: 0 4px; }
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
    <div class="tab active">오늘의 말씀</div>
    <div class="tab">우리 로그</div>
    <div class="tab">전체</div>
  </div>

  <!-- TOP BAR: Group selector + Interval toggle -->

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
      <button class="interval-btn active" onclick="setInterval(this, 1)">1시간</button>
      <button class="interval-btn" onclick="setInterval(this, 3)">3시간</button>
    </div>
  </div>

  <div class="viewfinder" id="viewfinder">
    <div class="demo-bg"></div>
    <video id="cameraStream" autoplay playsinline muted></video>
    <img id="snapshotImg" alt="" />

```
<div class="vf-meta" id="vfTime">11:00 · 5.15</div>
<div class="mode-badge">
  <span class="mode-dot"></span>
  <span class="mode-text"></span>
</div>

<div class="verse-overlay">
  <div class="verse-sparkle">✦</div>
  <div class="verse-text" id="verseText">
    너희는 먼저 그의 나라와 그의 의를 구하라<br>
    그리하면 이 모든 것을 너희에게 더하시리라
  </div>
  <div class="verse-ref" id="verseRef">MATTHEW 6 : 33</div>
  <div class="lang-hint" id="langHint">탭하면 EN ▸</div>
</div>

<div class="demo-hint">갤러리 버튼으로 사진을 올려보세요 ✨</div>
<div class="flash" id="flash"></div>
```

  </div>

  <div class="photo-hint">
    풍경 · 셀카 · 일상 · <span class="em">무엇이든</span> 자유롭게
  </div>

  <div class="controls">
    <div class="ctrl-side">
      <button class="icon-btn" onclick="document.getElementById('fileInput').click()" title="갤러리">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
          <rect x="3" y="5" width="18" height="14" rx="3"/>
          <circle cx="8.5" cy="10.5" r="1.5"/>
          <path d="M21 16l-5-5L5 19"/>
        </svg>
      </button>
    </div>
    <button class="shutter" id="shutterBtn" onclick="capture()">
      <div class="shutter-inner"></div>
    </button>
    <div class="ctrl-side right">
      <button class="icon-btn accent" onclick="tryCamera()" title="카메라 켜기">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round">
          <path d="M23 19a2 2 0 0 1-2 2H3a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h4l2-3h6l2 3h4a2 2 0 0 1 2 2z"/>
          <circle cx="12" cy="13" r="4"/>
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

  <div class="dev-note">
    <b>💡 새로 추가된 기능</b><br>
    • 매 시간/3시간 간격 선택 · 상단 토글<br>
    • 그룹 전환 + 비공개/공개 설정 · 상단 그룹 영역 탭<br>
    • 한↔영 말씀 토글 · 말씀 텍스트 탭<br>
    • 풍경·셀카·일상 자유롭게 · 카메라 전환은 우측 아이콘
  </div>

  <div class="hint">— made with <span class="heart">♥</span> for the word —</div>
</div>

<input type="file" id="fileInput" accept="image/*" onchange="loadImage(event)" />
<canvas id="captureCanvas" style="display:none"></canvas>

<!-- GROUP SELECTOR SHEET -->

<div class="sheet" id="groupSheet" onclick="if(event.target===this) closeGroupSheet()">
  <div class="sheet-content">
    <div class="sheet-handle"></div>
    <div class="sheet-title">로그 선택</div>
    <div class="sheet-sub">어떤 그룹에 묵상을 남길까요?</div>
    <div class="group-list" id="groupList"></div>
    <div class="sheet-actions">
      <button class="sheet-btn" onclick="closeGroupSheet()">취소</button>
      <button class="sheet-btn primary" onclick="confirmGroup()">선택 ✨</button>
    </div>
  </div>
</div>

<!-- CAPTURED CARD MODAL -->

<div class="modal" id="modal">
  <div class="card">
    <div class="card-img">
      <img id="cardCapturedImg" alt="" />
    </div>
    <div class="card-meta">
      <span class="card-meta-left" id="cardTime">11 : 00 · MAY 15</span>
      <span class="card-group-badge private" id="cardGroupBadge">우리 가족 · 비공개</span>
    </div>
    <div class="publish-row">
      <div class="publish-info">
        <div class="publish-title">전체 공개로 올릴까요? 🌍</div>
        <div class="publish-sub" id="publishSub">'전체' 피드의 모든 사람이 볼 수 있어요</div>
      </div>
      <div class="switch" id="publishSwitch" onclick="togglePublish()"></div>
    </div>
    <div class="card-actions">
      <button class="btn" onclick="closeModal()">다시 찍기</button>
      <button class="btn primary" onclick="saveAndClose()">로그에 저장</button>
    </div>
  </div>
</div>

<script>
  // === VERSES with KR + EN ===
  const verses = [
    {
      kr: '너희는 먼저 그의 나라와 그의 의를 구하라<br>그리하면 이 모든 것을 너희에게 더하시리라',
      en: 'But seek first the Kingdom of God,<br>and his righteousness;<br>and all these things will be given to you as well.',
      ref: 'MATTHEW 6 : 33'
    },
    {
      kr: '오직 여호와를 앙망하는 자는 새 힘을 얻으리니<br>독수리가 날개치며 올라감 같을 것이요',
      en: 'But those who wait for Yahweh<br>will renew their strength.<br>They will mount up with wings like eagles.',
      ref: 'ISAIAH 40 : 31'
    },
    {
      kr: '여호와는 나의 목자시니<br>내게 부족함이 없으리로다',
      en: 'Yahweh is my shepherd;<br>I shall lack nothing.',
      ref: 'PSALM 23 : 1'
    },
    {
      kr: '수고하고 무거운 짐 진 자들아 다 내게로 오라<br>내가 너희를 쉬게 하리라',
      en: 'Come to me, all you who labor<br>and are heavily burdened,<br>and I will give you rest.',
      ref: 'MATTHEW 11 : 28'
    },
    {
      kr: '항상 기뻐하라<br>쉬지 말고 기도하라<br>범사에 감사하라',
      en: 'Rejoice always.<br>Pray without ceasing.<br>In everything give thanks.',
      ref: '1 THESS 5 : 16-18'
    }
  ];
  let currentIndex = 0;
  let currentLang = 'kr'; // 'kr' or 'en'

  // === GROUPS ===
  const groups = [
    { id: 'family', name: '우리 가족', icon: '우', members: 4, type: 'private', desc: '엄마, 아빠, 동생과 함께' },
    { id: 'cell', name: '청년부 셀모임', icon: '청', members: 6, type: 'private', desc: '매주 토요일 셀원들' },
    { id: 'solo', name: '나의 묵상 노트', icon: '나', members: 1, type: 'solo', desc: '오직 나만 보는 공간' },
    { id: 'public', name: '전체 피드', icon: '✦', members: 0, type: 'public', desc: '모든 워드로그 사용자' }
  ];
  let currentGroupId = 'family';
  let pendingGroupId = 'family';

  let stream = null;
  let facingMode = 'environment';
  let lastUploadedImg = null;
  let isPublic = false;

  const viewfinder = document.getElementById('viewfinder');
  const video = document.getElementById('cameraStream');
  const snapshot = document.getElementById('snapshotImg');

  // === CAMERA ===
  async function tryCamera() {
    if (!navigator.mediaDevices || !navigator.mediaDevices.getUserMedia) {
      alert('이 환경은 카메라를 지원하지 않아요 😢\n폰 브라우저에서 직접 열면 켜져요!');
      return;
    }
    try {
      if (stream) stream.getTracks().forEach(t => t.stop());
      stream = await navigator.mediaDevices.getUserMedia({
        video: { facingMode: { ideal: facingMode } },
        audio: false
      });
      video.srcObject = stream;
      video.classList.toggle('mirrored', facingMode === 'user');
      await video.play();
      viewfinder.classList.remove('snapshot');
      viewfinder.classList.add('live');
    } catch (err) {
      alert('카메라가 차단되었어요 😢\n갤러리 버튼으로 사진을 올려보세요!');
    }
  }

  function loadImage(event) {
    const file = event.target.files[0];
    if (!file) return;
    const reader = new FileReader();
    reader.onload = (e) => {
      lastUploadedImg = e.target.result;
      snapshot.src = e.target.result;
      viewfinder.classList.remove('live');
      viewfinder.classList.add('snapshot');
    };
    reader.readAsDataURL(file);
  }

  // === LANGUAGE TOGGLE ===
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

  // === INTERVAL ===
  function setInterval(btn, hours) {
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

  // === GROUP SHEET ===
  function renderGroupList() {
    const list = document.getElementById('groupList');
    list.innerHTML = '';
    groups.forEach(g => {
      const item = document.createElement('div');
      item.className = 'group-item' + (g.id === pendingGroupId ? ' selected' : '') + ` ${g.type}`;
      item.onclick = () => {
        pendingGroupId = g.id;
        renderGroupList();
      };
      let pillHtml = '';
      if (g.type === 'private') pillHtml = '<span class="privacy-pill private">비공개</span>';
      else if (g.type === 'public') pillHtml = '<span class="privacy-pill public">전체 공개</span>';
      else pillHtml = '<span class="privacy-pill private">나만 보기</span>';
      item.innerHTML = `
        <div class="group-avatar">${g.icon}</div>
        <div class="group-item-info">
          <div class="group-item-name">${g.name}</div>
          <div class="group-item-meta">
            ${pillHtml}
            <span>${g.type === 'public' ? '모두에게' : (g.members + '명')}</span>
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
  function closeGroupSheet() {
    document.getElementById('groupSheet').classList.remove('show');
  }
  function confirmGroup() {
    currentGroupId = pendingGroupId;
    const g = groups.find(x => x.id === currentGroupId);
    document.getElementById('groupAvatar').textContent = g.icon;
    document.getElementById('groupName').textContent = g.name;
    const pill = document.getElementById('privacyPill');
    if (g.type === 'public') {
      pill.className = 'privacy-pill public';
      pill.textContent = '전체 공개';
      document.getElementById('groupMembers').textContent = '모두에게';
    } else if (g.type === 'solo') {
      pill.className = 'privacy-pill private';
      pill.textContent = '나만 보기';
      document.getElementById('groupMembers').textContent = '1명';
    } else {
      pill.className = 'privacy-pill private';
      pill.textContent = '비공개';
      document.getElementById('groupMembers').textContent = g.members + '명';
    }
    closeGroupSheet();
  }

  // === PUBLISH TOGGLE ===
  function togglePublish() {
    isPublic = !isPublic;
    const sw = document.getElementById('publishSwitch');
    sw.classList.toggle('on', isPublic);
    updateCardBadge();
  }
  function updateCardBadge() {
    const g = groups.find(x => x.id === currentGroupId);
    const badge = document.getElementById('cardGroupBadge');
    if (isPublic) {
      badge.className = 'card-group-badge public';
      badge.textContent = `${g.name} + 🌍 전체`;
    } else {
      badge.className = 'card-group-badge private';
      const status = g.type === 'public' ? '전체 공개' : (g.type === 'solo' ? '나만' : '비공개');
      badge.textContent = `${g.name} · ${status}`;
    }
  }

  // === CAPTURE ===
  function capture() {
    const flash = document.getElementById('flash');
    flash.classList.remove('fire');
    void flash.offsetWidth;
    flash.classList.add('fire');

    const canvas = document.getElementById('captureCanvas');
    const ctx = canvas.getContext('2d');
    const W = 900, H = 1200;
    canvas.width = W; canvas.height = H;

    if (viewfinder.classList.contains('live') && video.videoWidth) {
      drawCover(ctx, video, W, H, facingMode === 'user');
      drawOverlay(ctx, W, H);
      showCard(canvas.toDataURL('image/jpeg', 0.92));
    } else if (viewfinder.classList.contains('snapshot') && lastUploadedImg) {
      const img = new Image();
      img.onload = () => {
        drawCover(ctx, img, W, H, false);
        drawOverlay(ctx, W, H);
        showCard(canvas.toDataURL('image/jpeg', 0.92));
      };
      img.src = lastUploadedImg;
    } else {
      const grad = ctx.createLinearGradient(0, 0, W, H);
      grad.addColorStop(0, '#FFB591'); grad.addColorStop(0.3, '#FFC9A1');
      grad.addColorStop(0.6, '#FFAEC8'); grad.addColorStop(0.85, '#C9B6F0');
      grad.addColorStop(1, '#9BB8E8');
      ctx.fillStyle = grad; ctx.fillRect(0, 0, W, H);
      const rg = ctx.createRadialGradient(W*0.25, H*0.25, 0, W*0.25, H*0.25, W*0.55);
      rg.addColorStop(0, 'rgba(255,245,220,0.55)');
      rg.addColorStop(1, 'rgba(255,245,220,0)');
      ctx.fillStyle = rg; ctx.fillRect(0, 0, W, H);
      drawOverlay(ctx, W, H);
      showCard(canvas.toDataURL('image/jpeg', 0.92));
    }
  }

  function drawCover(ctx, src, dw, dh, mirror) {
    const sw = src.videoWidth || src.naturalWidth;
    const sh = src.videoHeight || src.naturalHeight;
    const srcRatio = sw / sh;
    const dstRatio = dw / dh;
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
    const v = verses[currentIndex];
    const text = currentLang === 'kr' ? v.kr : v.en;
    const vg = ctx.createRadialGradient(W/2, H/2, H*0.3, W/2, H/2, H*0.75);
    vg.addColorStop(0, 'rgba(0,0,0,0)');
    vg.addColorStop(1, 'rgba(60,30,50,0.25)');
    ctx.fillStyle = vg;
    ctx.fillRect(0, 0, W, H);

    ctx.fillStyle = '#fff';
    ctx.textAlign = 'center';
    ctx.textBaseline = 'middle';
    ctx.shadowColor = 'rgba(60,30,50,0.6)';

    const lines = text.split('<br>');
    if (currentLang === 'kr') {
      ctx.font = '400 38px "Gowun Batang", serif';
    } else {
      ctx.font = 'italic 400 36px "Fraunces", serif';
    }
    const lineHeight = currentLang === 'kr' ? 66 : 58;
    const totalH = lines.length * lineHeight;
    const startY = H/2 - totalH/2 + lineHeight/2 - 10;

    ctx.font = '32px sans-serif';
    ctx.shadowBlur = 10;
    ctx.fillText('✦', W/2, startY - lineHeight/2 - 50);

    if (currentLang === 'kr') {
      ctx.font = '400 38px "Gowun Batang", serif';
    } else {
      ctx.font = 'italic 400 36px "Fraunces", serif';
    }
    ctx.shadowBlur = 14;
    ctx.shadowOffsetY = 2;
    lines.forEach((line, i) => {
      ctx.fillText(line, W/2, startY + i * lineHeight);
    });

    ctx.shadowBlur = 0;
    ctx.shadowOffsetY = 0;
    const refY = startY + totalH + 40;
    const refText = v.ref;
    ctx.font = 'italic 26px "Fraunces", serif';
    const refWidth = ctx.measureText(refText).width;
    const pillW = refWidth + 36;
    const pillH = 42;
    ctx.fillStyle = 'rgba(255,255,255,0.22)';
    roundRect(ctx, W/2 - pillW/2, refY - pillH/2, pillW, pillH, 21);
    ctx.fill();
    ctx.fillStyle = '#fff';
    ctx.shadowColor = 'rgba(60,30,50,0.5)';
    ctx.shadowBlur = 6;
    ctx.fillText(refText, W/2, refY);
    ctx.shadowBlur = 0;

    const now = new Date();
    const hh = String(now.getHours()).padStart(2, '0');
    const mm = String(now.getMinutes()).padStart(2, '0');
    const month = now.getMonth() + 1;
    const day = now.getDate();
    ctx.font = 'italic 20px "Fraunces", serif';
    ctx.fillStyle = 'rgba(255,255,255,0.95)';
    ctx.textAlign = 'left';
    ctx.shadowColor = 'rgba(60,30,50,0.6)';
    ctx.shadowBlur = 6;
    ctx.fillText(`${hh}:${mm} · ${month}.${day}`, 60, 56);
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

  function showCard(dataUrl) {
    document.getElementById('cardCapturedImg').src = dataUrl;
    const now = new Date();
    const hh = String(now.getHours() % 12 || 12).padStart(2, '0');
    const mm = String(now.getMinutes()).padStart(2, '0');
    const months = ['JAN','FEB','MAR','APR','MAY','JUN','JUL','AUG','SEP','OCT','NOV','DEC'];
    document.getElementById('cardTime').textContent =
      `${hh} : ${mm} · ${months[now.getMonth()]} ${now.getDate()}`;
    // Reset publish toggle each capture
    isPublic = false;
    document.getElementById('publishSwitch').classList.remove('on');
    updateCardBadge();
    setTimeout(() => document.getElementById('modal').classList.add('show'), 300);
  }

  function closeModal() { document.getElementById('modal').classList.remove('show'); }
  function saveAndClose() {
    const g = groups.find(x => x.id === currentGroupId);
    const msg = isPublic
      ? `✨ "${g.name}"과 전체 피드에 저장되었어요!`
      : `✨ "${g.name}"에 저장되었어요!`;
    closeModal();
    setTimeout(() => alert(msg), 200);
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
    const month = now.getMonth() + 1;
    const day = now.getDate();
    document.getElementById('vfTime').textContent = `${String(hh).padStart(2,'0')}:${mm} · ${month}.${day}`;
  }
  updateTime();
  window.setInterval(updateTime, 1000);
  updateNextTime(1);
</script>

</body>
</html>