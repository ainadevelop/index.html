<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>SENTINEL Hub</title>
<link href="https://fonts.googleapis.com/css2?family=DM+Mono:wght@300;400;500&family=Syne:wght@400;600;700;800&family=Noto+Sans+JP:wght@300;400;500&display=swap" rel="stylesheet">
<style>
:root {
  --bg: #080c12;
  --surface: #0e1420;
  --surface2: #131b28;
  --border: #1e2d42;
  --border2: #243347;
  --accent: #00d4ff;
  --accent2: #ff3d5a;
  --accent3: #00ff9d;
  --accent4: #ffb800;
  --text: #e2eaf4;
  --text2: #7a90aa;
  --text3: #3d5270;
  --mono: 'DM Mono', monospace;
  --display: 'Syne', sans-serif;
  --body: 'Noto Sans JP', sans-serif;
}

* { margin: 0; padding: 0; box-sizing: border-box; }

body {
  background: var(--bg);
  color: var(--text);
  font-family: var(--body);
  font-size: 13px;
  min-height: 100vh;
  overflow-x: hidden;
}

/* Animated grid background */
body::before {
  content: '';
  position: fixed;
  inset: 0;
  background-image:
    linear-gradient(rgba(0,212,255,0.03) 1px, transparent 1px),
    linear-gradient(90deg, rgba(0,212,255,0.03) 1px, transparent 1px);
  background-size: 40px 40px;
  pointer-events: none;
  z-index: 0;
}

/* Glow orbs */
body::after {
  content: '';
  position: fixed;
  top: -200px;
  left: -200px;
  width: 600px;
  height: 600px;
  background: radial-gradient(circle, rgba(0,212,255,0.06) 0%, transparent 70%);
  pointer-events: none;
  z-index: 0;
}

.layout {
  display: grid;
  grid-template-columns: 220px 1fr;
  min-height: 100vh;
  position: relative;
  z-index: 1;
}

/* ── SIDEBAR ── */
.sidebar {
  background: var(--surface);
  border-right: 1px solid var(--border);
  padding: 0;
  display: flex;
  flex-direction: column;
  position: sticky;
  top: 0;
  height: 100vh;
  overflow: hidden;
}

.sidebar-logo {
  padding: 20px 18px 16px;
  border-bottom: 1px solid var(--border);
  display: flex;
  align-items: center;
  gap: 10px;
}

.logo-icon {
  width: 34px;
  height: 34px;
  background: linear-gradient(135deg, #00d4ff20, #00d4ff40);
  border: 1px solid var(--accent);
  border-radius: 6px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
  box-shadow: 0 0 12px rgba(0,212,255,0.2);
}

.logo-icon svg { width: 18px; height: 18px; }

.logo-text {
  font-family: var(--display);
  font-size: 17px;
  font-weight: 800;
  letter-spacing: 0.5px;
  color: var(--text);
}

.logo-version {
  font-family: var(--mono);
  font-size: 9px;
  color: var(--accent);
  letter-spacing: 1px;
  margin-top: 1px;
}

.sidebar-section {
  padding: 16px 12px 6px;
}

.sidebar-section-label {
  font-family: var(--mono);
  font-size: 9px;
  letter-spacing: 2px;
  color: var(--text3);
  text-transform: uppercase;
  padding: 0 6px;
  margin-bottom: 4px;
}

.nav-item {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 9px 10px;
  border-radius: 6px;
  cursor: pointer;
  transition: all 0.15s;
  margin-bottom: 2px;
  position: relative;
  font-size: 12.5px;
  color: var(--text2);
}

.nav-item:hover {
  background: var(--surface2);
  color: var(--text);
}

.nav-item.active {
  background: rgba(0,212,255,0.08);
  color: var(--accent);
  border: 1px solid rgba(0,212,255,0.15);
}

.nav-item.active::before {
  content: '';
  position: absolute;
  left: 0;
  top: 20%;
  height: 60%;
  width: 2px;
  background: var(--accent);
  border-radius: 2px;
  box-shadow: 0 0 6px var(--accent);
}

.nav-icon { font-size: 14px; width: 18px; text-align: center; }

.nav-badge {
  margin-left: auto;
  background: var(--accent2);
  color: white;
  font-family: var(--mono);
  font-size: 9px;
  padding: 2px 6px;
  border-radius: 10px;
  font-weight: 500;
}

.sidebar-spacer { flex: 1; }

.sidebar-bottom {
  padding: 12px;
  border-top: 1px solid var(--border);
}

.user-card {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 8px;
  border-radius: 6px;
  background: var(--surface2);
}

.user-avatar {
  width: 30px;
  height: 30px;
  border-radius: 50%;
  background: linear-gradient(135deg, #00d4ff, #0080ff);
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: var(--display);
  font-size: 12px;
  font-weight: 700;
  color: white;
  flex-shrink: 0;
}

.user-name { font-size: 12px; font-weight: 500; }
.user-role { font-size: 10px; color: var(--text2); }

/* ── MAIN ── */
.main {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

/* TOP BAR */
.topbar {
  background: var(--surface);
  border-bottom: 1px solid var(--border);
  padding: 0 24px;
  height: 56px;
  display: flex;
  align-items: center;
  gap: 16px;
  position: sticky;
  top: 0;
  z-index: 10;
}

.topbar-title {
  font-family: var(--display);
  font-size: 16px;
  font-weight: 700;
}

.topbar-sub {
  font-family: var(--mono);
  font-size: 10px;
  color: var(--text2);
}

.topbar-spacer { flex: 1; }

.topbar-location {
  display: flex;
  align-items: center;
  gap: 6px;
  font-family: var(--mono);
  font-size: 11px;
  color: var(--text2);
  background: var(--surface2);
  border: 1px solid var(--border);
  padding: 5px 12px;
  border-radius: 6px;
  cursor: pointer;
}

.status-dot {
  width: 7px;
  height: 7px;
  border-radius: 50%;
  background: var(--accent3);
  box-shadow: 0 0 6px var(--accent3);
  animation: pulse 2s infinite;
}

@keyframes pulse {
  0%, 100% { opacity: 1; transform: scale(1); }
  50% { opacity: 0.6; transform: scale(0.85); }
}

.topbar-alert {
  position: relative;
  width: 34px;
  height: 34px;
  background: var(--surface2);
  border: 1px solid var(--border);
  border-radius: 6px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  font-size: 15px;
}

.alert-count {
  position: absolute;
  top: -4px;
  right: -4px;
  background: var(--accent2);
  color: white;
  font-family: var(--mono);
  font-size: 8px;
  width: 14px;
  height: 14px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 700;
}

/* CONTENT */
.content {
  padding: 20px 24px;
  flex: 1;
}

/* STATS ROW */
.stats-row {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 12px;
  margin-bottom: 20px;
}

.stat-card {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 8px;
  padding: 16px;
  position: relative;
  overflow: hidden;
  cursor: default;
  transition: border-color 0.2s;
  animation: fadeUp 0.4s ease both;
}

.stat-card:nth-child(1) { animation-delay: 0.05s; }
.stat-card:nth-child(2) { animation-delay: 0.1s; }
.stat-card:nth-child(3) { animation-delay: 0.15s; }
.stat-card:nth-child(4) { animation-delay: 0.2s; }

@keyframes fadeUp {
  from { opacity: 0; transform: translateY(10px); }
  to { opacity: 1; transform: translateY(0); }
}

.stat-card:hover { border-color: var(--border2); }

.stat-card::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  height: 2px;
}

.stat-card.cyan::after { background: linear-gradient(90deg, transparent, var(--accent), transparent); }
.stat-card.red::after { background: linear-gradient(90deg, transparent, var(--accent2), transparent); }
.stat-card.green::after { background: linear-gradient(90deg, transparent, var(--accent3), transparent); }
.stat-card.yellow::after { background: linear-gradient(90deg, transparent, var(--accent4), transparent); }

.stat-label {
  font-family: var(--mono);
  font-size: 9.5px;
  letter-spacing: 1.5px;
  text-transform: uppercase;
  color: var(--text2);
  margin-bottom: 8px;
}

.stat-value {
  font-family: var(--display);
  font-size: 30px;
  font-weight: 800;
  line-height: 1;
  margin-bottom: 6px;
}

.stat-card.cyan .stat-value { color: var(--accent); }
.stat-card.red .stat-value { color: var(--accent2); }
.stat-card.green .stat-value { color: var(--accent3); }
.stat-card.yellow .stat-value { color: var(--accent4); }

.stat-change {
  font-family: var(--mono);
  font-size: 10px;
  color: var(--text2);
}

.stat-change span { color: var(--accent3); }

/* GRID 2+1 */
.grid-main {
  display: grid;
  grid-template-columns: 1fr 340px;
  gap: 12px;
  margin-bottom: 16px;
}

/* CAMERA FEED */
.camera-grid {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 8px;
  overflow: hidden;
  animation: fadeUp 0.4s 0.25s ease both;
}

.panel-header {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 12px 16px;
  border-bottom: 1px solid var(--border);
}

.panel-title {
  font-family: var(--display);
  font-size: 13px;
  font-weight: 700;
}

.panel-sub {
  font-family: var(--mono);
  font-size: 10px;
  color: var(--text2);
  margin-left: auto;
}

.cameras {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1px;
  background: var(--border);
}

.cam {
  background: #040810;
  aspect-ratio: 16/10;
  position: relative;
  overflow: hidden;
  cursor: pointer;
}

.cam:hover .cam-overlay { opacity: 1; }

.cam-bg {
  width: 100%;
  height: 100%;
  position: relative;
}

/* Simulated camera feeds with CSS */
.cam-1 .cam-bg {
  background: radial-gradient(ellipse at 60% 40%, #1a2a1a 0%, #050b05 100%);
}
.cam-2 .cam-bg {
  background: radial-gradient(ellipse at 40% 60%, #1a1a2a 0%, #05050b 100%);
}
.cam-3 .cam-bg {
  background: radial-gradient(ellipse at 50% 30%, #2a1a1a 0%, #0b0505 100%);
}
.cam-4 .cam-bg {
  background: radial-gradient(ellipse at 30% 70%, #1a2a2a 0%, #050b0b 100%);
}

/* Scan line effect */
.cam-bg::before {
  content: '';
  position: absolute;
  inset: 0;
  background: repeating-linear-gradient(
    0deg,
    transparent,
    transparent 2px,
    rgba(0,0,0,0.15) 2px,
    rgba(0,0,0,0.15) 4px
  );
  pointer-events: none;
}

/* Moving scan line */
.cam-bg::after {
  content: '';
  position: absolute;
  left: 0;
  right: 0;
  height: 2px;
  background: linear-gradient(90deg, transparent, rgba(0,212,255,0.4), transparent);
  animation: scan 4s linear infinite;
  opacity: 0.6;
}

.cam-1 .cam-bg::after { animation-delay: 0s; }
.cam-2 .cam-bg::after { animation-delay: 1s; }
.cam-3 .cam-bg::after { animation-delay: 2s; }
.cam-4 .cam-bg::after { animation-delay: 3s; }

@keyframes scan {
  0% { top: -2px; }
  100% { top: 100%; }
}

.cam-info {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  padding: 6px 8px;
  background: linear-gradient(transparent, rgba(0,0,0,0.8));
  display: flex;
  align-items: center;
  gap: 6px;
}

.cam-name {
  font-family: var(--mono);
  font-size: 9px;
  color: rgba(255,255,255,0.8);
  letter-spacing: 1px;
}

.cam-live {
  font-family: var(--mono);
  font-size: 8px;
  color: var(--accent3);
  margin-left: auto;
  display: flex;
  align-items: center;
  gap: 3px;
}

.cam-live::before {
  content: '';
  width: 5px;
  height: 5px;
  border-radius: 50%;
  background: var(--accent3);
  box-shadow: 0 0 4px var(--accent3);
  animation: pulse 1.5s infinite;
}

.cam-alert-badge {
  position: absolute;
  top: 6px;
  right: 6px;
  background: var(--accent2);
  color: white;
  font-family: var(--mono);
  font-size: 8px;
  padding: 2px 6px;
  border-radius: 3px;
  font-weight: 700;
  animation: blink 1s infinite;
}

@keyframes blink {
  0%, 100% { opacity: 1; }
  50% { opacity: 0.4; }
}

.cam-overlay {
  position: absolute;
  inset: 0;
  background: rgba(0,212,255,0.05);
  border: 1px solid rgba(0,212,255,0.3);
  opacity: 0;
  transition: opacity 0.2s;
  display: flex;
  align-items: center;
  justify-content: center;
}

.cam-overlay span {
  font-family: var(--mono);
  font-size: 9px;
  color: var(--accent);
  letter-spacing: 1px;
  background: rgba(0,0,0,0.7);
  padding: 4px 10px;
  border: 1px solid rgba(0,212,255,0.3);
}

/* Person detection simulation */
.person-box {
  position: absolute;
  border: 1.5px solid var(--accent3);
  box-shadow: 0 0 6px rgba(0,255,157,0.3);
}

.person-label {
  position: absolute;
  top: -16px;
  left: 0;
  font-family: var(--mono);
  font-size: 7px;
  color: var(--accent3);
  background: rgba(0,0,0,0.8);
  padding: 1px 4px;
  white-space: nowrap;
}

/* ACTIVITY FEED */
.activity {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 8px;
  overflow: hidden;
  animation: fadeUp 0.4s 0.3s ease both;
}

.activity-list {
  padding: 6px 0;
  max-height: 280px;
  overflow-y: auto;
}

.activity-list::-webkit-scrollbar { width: 3px; }
.activity-list::-webkit-scrollbar-track { background: transparent; }
.activity-list::-webkit-scrollbar-thumb { background: var(--border2); border-radius: 2px; }

.activity-item {
  display: flex;
  gap: 10px;
  padding: 8px 16px;
  border-bottom: 1px solid rgba(30,45,66,0.5);
  transition: background 0.15s;
  cursor: default;
}

.activity-item:hover { background: var(--surface2); }
.activity-item:last-child { border-bottom: none; }

.activity-dot {
  width: 7px;
  height: 7px;
  border-radius: 50%;
  flex-shrink: 0;
  margin-top: 4px;
}

.dot-green { background: var(--accent3); box-shadow: 0 0 5px var(--accent3); }
.dot-red { background: var(--accent2); box-shadow: 0 0 5px var(--accent2); }
.dot-cyan { background: var(--accent); box-shadow: 0 0 5px var(--accent); }
.dot-yellow { background: var(--accent4); box-shadow: 0 0 5px var(--accent4); }

.activity-text {
  flex: 1;
  font-size: 11.5px;
  line-height: 1.4;
}

.activity-name { font-weight: 500; color: var(--text); }
.activity-desc { color: var(--text2); font-size: 10.5px; }
.activity-time {
  font-family: var(--mono);
  font-size: 9px;
  color: var(--text3);
  flex-shrink: 0;
  margin-top: 2px;
}

/* BOTTOM GRID */
.grid-bottom {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  gap: 12px;
}

/* MEMBERS TABLE */
.members {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 8px;
  overflow: hidden;
  animation: fadeUp 0.4s 0.35s ease both;
  grid-column: span 2;
}

.member-table {
  width: 100%;
  border-collapse: collapse;
  font-size: 11.5px;
}

.member-table th {
  font-family: var(--mono);
  font-size: 9px;
  letter-spacing: 1.5px;
  text-transform: uppercase;
  color: var(--text3);
  padding: 8px 16px;
  text-align: left;
  border-bottom: 1px solid var(--border);
  background: var(--surface2);
}

.member-table td {
  padding: 9px 16px;
  border-bottom: 1px solid rgba(30,45,66,0.4);
  vertical-align: middle;
}

.member-table tr:last-child td { border-bottom: none; }
.member-table tr:hover td { background: var(--surface2); }

.member-avatar-sm {
  width: 24px;
  height: 24px;
  border-radius: 50%;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  font-family: var(--display);
  font-size: 10px;
  font-weight: 700;
  color: white;
  margin-right: 8px;
  vertical-align: middle;
}

.status-tag {
  font-family: var(--mono);
  font-size: 9px;
  padding: 3px 8px;
  border-radius: 4px;
  font-weight: 500;
  letter-spacing: 0.5px;
}

.tag-in {
  background: rgba(0,255,157,0.12);
  color: var(--accent3);
  border: 1px solid rgba(0,255,157,0.2);
}

.tag-out {
  background: rgba(255,61,90,0.1);
  color: var(--accent2);
  border: 1px solid rgba(255,61,90,0.2);
}

.tag-reserved {
  background: rgba(0,212,255,0.1);
  color: var(--accent);
  border: 1px solid rgba(0,212,255,0.2);
}

/* INTEGRATIONS */
.integrations {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 8px;
  overflow: hidden;
  animation: fadeUp 0.4s 0.4s ease both;
}

.integration-item {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 10px 16px;
  border-bottom: 1px solid rgba(30,45,66,0.4);
  transition: background 0.15s;
}

.integration-item:last-child { border-bottom: none; }
.integration-item:hover { background: var(--surface2); }

.integration-icon {
  width: 28px;
  height: 28px;
  border-radius: 5px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 13px;
  flex-shrink: 0;
}

.integration-name { font-size: 12px; font-weight: 500; }
.integration-status { font-family: var(--mono); font-size: 9px; color: var(--text2); }

.integration-toggle {
  margin-left: auto;
  width: 32px;
  height: 17px;
  border-radius: 10px;
  cursor: pointer;
  position: relative;
  transition: background 0.2s;
  flex-shrink: 0;
}

.integration-toggle.on { background: var(--accent3); }
.integration-toggle.off { background: var(--border2); }

.integration-toggle::after {
  content: '';
  position: absolute;
  top: 2px;
  width: 13px;
  height: 13px;
  border-radius: 50%;
  background: white;
  transition: left 0.2s;
}

.integration-toggle.on::after { left: 17px; }
.integration-toggle.off::after { left: 2px; }

/* TABS */
.tab-bar {
  display: flex;
  gap: 0;
  border-bottom: 1px solid var(--border);
  padding: 0 16px;
}

.tab {
  font-family: var(--mono);
  font-size: 10px;
  letter-spacing: 1px;
  padding: 10px 14px;
  cursor: pointer;
  color: var(--text2);
  border-bottom: 2px solid transparent;
  transition: all 0.15s;
  white-space: nowrap;
}

.tab:hover { color: var(--text); }
.tab.active { color: var(--accent); border-bottom-color: var(--accent); }

/* LOCK STATUS */
.lock-status {
  padding: 14px 16px;
}

.lock-item {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 8px 10px;
  background: var(--surface2);
  border-radius: 6px;
  margin-bottom: 8px;
  border: 1px solid var(--border);
  cursor: pointer;
  transition: all 0.15s;
}

.lock-item:hover { border-color: var(--border2); }
.lock-item:last-child { margin-bottom: 0; }

.lock-icon {
  font-size: 18px;
  width: 30px;
  text-align: center;
}

.lock-name { font-size: 12px; font-weight: 500; flex: 1; }
.lock-location { font-size: 10px; color: var(--text2); }

.lock-btn {
  font-family: var(--mono);
  font-size: 9px;
  padding: 4px 10px;
  border-radius: 4px;
  border: none;
  cursor: pointer;
  font-weight: 700;
  letter-spacing: 0.5px;
  transition: all 0.15s;
}

.lock-btn.locked {
  background: rgba(255,61,90,0.15);
  color: var(--accent2);
  border: 1px solid rgba(255,61,90,0.3);
}

.lock-btn.unlocked {
  background: rgba(0,255,157,0.12);
  color: var(--accent3);
  border: 1px solid rgba(0,255,157,0.2);
}

.lock-btn:hover { filter: brightness(1.3); transform: scale(1.03); }

/* MINI CHART */
.mini-chart {
  padding: 10px 16px 14px;
}

.chart-bars {
  display: flex;
  align-items: flex-end;
  gap: 4px;
  height: 50px;
}

.bar {
  flex: 1;
  border-radius: 2px 2px 0 0;
  background: rgba(0,212,255,0.2);
  transition: all 0.3s;
  cursor: pointer;
  position: relative;
}

.bar:hover { background: rgba(0,212,255,0.5); }
.bar.highlight { background: var(--accent); }

.chart-labels {
  display: flex;
  gap: 4px;
  margin-top: 4px;
}

.chart-label {
  flex: 1;
  font-family: var(--mono);
  font-size: 8px;
  color: var(--text3);
  text-align: center;
}

/* SCROLLABLE TAB CONTENT */
.tab-content { display: none; }
.tab-content.active { display: block; }

/* ALERT BANNER */
.alert-banner {
  margin: 0 24px 16px;
  background: rgba(255,61,90,0.08);
  border: 1px solid rgba(255,61,90,0.25);
  border-radius: 6px;
  padding: 10px 14px;
  display: flex;
  align-items: center;
  gap: 10px;
  animation: fadeUp 0.3s ease both;
  cursor: pointer;
}

.alert-icon { font-size: 16px; flex-shrink: 0; }
.alert-text { flex: 1; font-size: 12px; }
.alert-text strong { color: var(--accent2); }
.alert-dismiss {
  font-family: var(--mono);
  font-size: 9px;
  color: var(--text2);
  cursor: pointer;
  padding: 3px 8px;
  border: 1px solid var(--border2);
  border-radius: 3px;
  flex-shrink: 0;
}

.alert-dismiss:hover { color: var(--text); }
</style>
</head>
<body>

<div class="layout">

  <!-- SIDEBAR -->
  <aside class="sidebar">
    <div class="sidebar-logo">
      <div class="logo-icon">
        <svg viewBox="0 0 24 24" fill="none" stroke="#00d4ff" stroke-width="1.8">
          <path d="M12 2L3 7v5c0 5.25 3.75 10.15 9 11.35C17.25 22.15 21 17.25 21 12V7L12 2z"/>
          <circle cx="12" cy="12" r="2.5" fill="#00d4ff" stroke="none"/>
        </svg>
      </div>
      <div>
        <div class="logo-text">SENTINEL</div>
        <div class="logo-version">HUB v1.0</div>
      </div
