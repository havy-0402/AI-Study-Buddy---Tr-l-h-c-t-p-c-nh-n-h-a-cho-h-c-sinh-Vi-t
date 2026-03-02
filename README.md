<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>AI Study Buddy – Trợ lý học tập cá nhân hóa</title>
<link href="https://fonts.googleapis.com/css2?family=Nunito:wght@400;600;700;800;900&family=DM+Sans:wght@300;400;500;600&display=swap" rel="stylesheet">
<style>
:root {
  --blue: #4A90E2;
  --blue-light: #7BB3EE;
  --blue-pale: #EBF3FD;
  --orange: #FFA94D;
  --orange-light: #FFD4A3;
  --white: #FFFFFF;
  --gray-50: #F8FAFC;
  --gray-100: #F1F5F9;
  --gray-200: #E2E8F0;
  --gray-400: #94A3B8;
  --gray-600: #475569;
  --gray-800: #1E293B;
  --text: #1A2332;
}

* { margin: 0; padding: 0; box-sizing: border-box; }

body {
  font-family: 'DM Sans', sans-serif;
  color: var(--text);
  background: var(--white);
  overflow-x: hidden;
}

h1, h2, h3, h4 { font-family: 'Nunito', sans-serif; }

/* NAV */
nav {
  position: fixed; top: 0; left: 0; right: 0; z-index: 100;
  background: rgba(255,255,255,0.92);
  backdrop-filter: blur(20px);
  border-bottom: 1px solid rgba(74,144,226,0.1);
  padding: 0 5%;
  height: 68px;
  display: flex; align-items: center; justify-content: space-between;
}

.logo {
  display: flex; align-items: center; gap: 10px;
  font-family: 'Nunito', sans-serif; font-weight: 900; font-size: 1.2rem;
  color: var(--blue); text-decoration: none;
}

.logo-icon {
  width: 38px; height: 38px; background: linear-gradient(135deg, var(--blue), #6BA8ED);
  border-radius: 12px; display: flex; align-items: center; justify-content: center;
  font-size: 1.1rem; box-shadow: 0 4px 12px rgba(74,144,226,0.3);
}

.nav-links {
  display: flex; align-items: center; gap: 32px; list-style: none;
}

.nav-links a {
  text-decoration: none; color: var(--gray-600); font-weight: 500; font-size: 0.9rem;
  transition: color 0.2s;
}
.nav-links a:hover { color: var(--blue); }

.btn-login {
  background: var(--blue); color: white !important;
  padding: 8px 22px; border-radius: 100px;
  font-weight: 600; transition: all 0.2s !important;
  box-shadow: 0 4px 12px rgba(74,144,226,0.25);
}
.btn-login:hover { background: #3a7fd0 !important; box-shadow: 0 6px 18px rgba(74,144,226,0.35) !important; transform: translateY(-1px); }

/* HERO */
.hero {
  min-height: 100vh;
  background: linear-gradient(160deg, #F0F7FF 0%, #EBF3FD 40%, #FFF8F3 100%);
  display: flex; align-items: center;
  padding: 100px 5% 60px;
  position: relative; overflow: hidden;
}

.hero::before {
  content: '';
  position: absolute; top: -100px; right: -100px;
  width: 500px; height: 500px;
  background: radial-gradient(circle, rgba(74,144,226,0.12) 0%, transparent 70%);
  border-radius: 50%;
  animation: float-blob 8s ease-in-out infinite;
}

.hero::after {
  content: '';
  position: absolute; bottom: -60px; left: -60px;
  width: 350px; height: 350px;
  background: radial-gradient(circle, rgba(255,169,77,0.1) 0%, transparent 70%);
  border-radius: 50%;
  animation: float-blob 10s ease-in-out infinite reverse;
}

@keyframes float-blob {
  0%, 100% { transform: translate(0,0) scale(1); }
  50% { transform: translate(20px, -20px) scale(1.05); }
}

.hero-content {
  flex: 1; max-width: 580px; position: relative; z-index: 2;
  animation: fadeUp 0.8s ease both;
}

.hero-badge {
  display: inline-flex; align-items: center; gap: 8px;
  background: white; border: 1.5px solid rgba(74,144,226,0.2);
  padding: 8px 16px; border-radius: 100px;
  font-size: 0.82rem; font-weight: 600; color: var(--blue);
  margin-bottom: 28px;
  box-shadow: 0 2px 12px rgba(74,144,226,0.1);
}

.hero-badge .dot {
  width: 8px; height: 8px; background: #22C55E;
  border-radius: 50%; animation: pulse 2s infinite;
}

@keyframes pulse {
  0%, 100% { opacity: 1; transform: scale(1); }
  50% { opacity: 0.7; transform: scale(1.3); }
}

.hero h1 {
  font-size: clamp(2.2rem, 5vw, 3.4rem);
  font-weight: 900; line-height: 1.15;
  color: var(--text); margin-bottom: 20px;
}

.hero h1 .accent { color: var(--blue); }
.hero h1 .accent-orange { color: var(--orange); }

.hero-sub {
  font-size: 1.1rem; color: var(--gray-600); line-height: 1.7;
  margin-bottom: 40px; max-width: 460px;
}

.hero-cta {
  display: flex; align-items: center; gap: 16px; flex-wrap: wrap;
}

.btn-primary {
  background: linear-gradient(135deg, var(--blue), #5B9FE8);
  color: white; border: none; padding: 15px 32px;
  border-radius: 100px; font-family: 'Nunito', sans-serif;
  font-weight: 800; font-size: 1rem; cursor: pointer;
  box-shadow: 0 8px 24px rgba(74,144,226,0.35);
  transition: all 0.3s; text-decoration: none; display: inline-flex; align-items: center; gap: 8px;
}
.btn-primary:hover { transform: translateY(-3px); box-shadow: 0 12px 32px rgba(74,144,226,0.45); }

.btn-secondary {
  color: var(--gray-600); font-weight: 600; font-size: 0.95rem;
  display: inline-flex; align-items: center; gap: 8px; cursor: pointer;
  background: none; border: none; transition: color 0.2s;
}
.btn-secondary:hover { color: var(--blue); }

.play-icon {
  width: 40px; height: 40px; background: white;
  border-radius: 50%; display: flex; align-items: center; justify-content: center;
  box-shadow: 0 4px 14px rgba(0,0,0,0.1); font-size: 0.85rem;
}

.hero-stats {
  display: flex; gap: 32px; margin-top: 48px;
}

.stat { }
.stat-number {
  font-family: 'Nunito', sans-serif; font-weight: 900; font-size: 1.6rem;
  color: var(--text); line-height: 1;
}
.stat-label { font-size: 0.82rem; color: var(--gray-400); margin-top: 2px; }

.hero-visual {
  flex: 1; display: flex; justify-content: center; align-items: center;
  position: relative; z-index: 2;
  animation: fadeUp 0.8s 0.2s ease both;
}

/* CHAT DEMO */
.chat-card {
  background: white;
  border-radius: 28px;
  box-shadow: 0 30px 80px rgba(74,144,226,0.18), 0 8px 24px rgba(0,0,0,0.06);
  width: 340px; overflow: hidden;
  position: relative;
}

.chat-header {
  background: linear-gradient(135deg, var(--blue), #6BA8ED);
  padding: 18px 20px;
  display: flex; align-items: center; gap: 12px;
}

.chat-avatar {
  width: 42px; height: 42px; background: rgba(255,255,255,0.25);
  border-radius: 50%; display: flex; align-items: center; justify-content: center;
  font-size: 1.2rem;
}

.chat-header-info h4 { color: white; font-size: 0.95rem; font-weight: 700; }
.chat-header-info p { color: rgba(255,255,255,0.8); font-size: 0.78rem; margin-top: 1px; }

.chat-online {
  margin-left: auto; display: flex; align-items: center; gap: 5px;
  color: rgba(255,255,255,0.9); font-size: 0.78rem;
}
.chat-online-dot { width: 8px; height: 8px; background: #4ADE80; border-radius: 50%; }

.chat-body { padding: 18px; background: #F8FBFF; min-height: 260px; }

.chat-status {
  text-align: center; padding: 8px 14px;
  background: rgba(74,144,226,0.08); border-radius: 100px;
  font-size: 0.75rem; color: var(--blue); font-weight: 600;
  margin-bottom: 14px; display: flex; align-items: center; justify-content: center; gap: 6px;
}

.analyzing-dots span {
  display: inline-block; width: 5px; height: 5px; background: var(--blue);
  border-radius: 50%; animation: bounce 1.2s infinite;
  margin: 0 1px;
}
.analyzing-dots span:nth-child(2) { animation-delay: 0.2s; }
.analyzing-dots span:nth-child(3) { animation-delay: 0.4s; }

@keyframes bounce {
  0%, 80%, 100% { transform: translateY(0); }
  40% { transform: translateY(-6px); }
}

.msg { display: flex; gap: 10px; margin-bottom: 12px; align-items: flex-end; }
.msg.user { flex-direction: row-reverse; }

.msg-avatar {
  width: 28px; height: 28px; border-radius: 50%; flex-shrink: 0;
  display: flex; align-items: center; justify-content: center; font-size: 0.85rem;
}
.msg-avatar.bot { background: linear-gradient(135deg, var(--blue), #6BA8ED); }
.msg-avatar.user-a { background: linear-gradient(135deg, #FF8C42, var(--orange)); }

.bubble {
  padding: 10px 14px; border-radius: 16px; font-size: 0.83rem;
  line-height: 1.5; max-width: 220px;
}
.bubble.bot { background: white; color: var(--text); box-shadow: 0 2px 8px rgba(0,0,0,0.06); border-bottom-left-radius: 4px; }
.bubble.user { background: linear-gradient(135deg, var(--blue), #5B9FE8); color: white; border-bottom-right-radius: 4px; }

.chat-input {
  background: white; border-top: 1px solid var(--gray-200);
  padding: 14px 16px; display: flex; align-items: center; gap: 10px;
}

.input-field {
  flex: 1; background: var(--gray-100); border: none; border-radius: 100px;
  padding: 9px 16px; font-size: 0.83rem; color: var(--gray-400);
  font-family: inherit; outline: none;
}

.input-actions { display: flex; gap: 6px; }
.input-btn {
  width: 32px; height: 32px; border-radius: 50%; border: none; cursor: pointer;
  display: flex; align-items: center; justify-content: center; font-size: 0.85rem;
  transition: all 0.2s;
}
.input-btn.file { background: var(--gray-100); color: var(--gray-400); }
.input-btn.mic { background: var(--gray-100); color: var(--gray-400); }
.input-btn.send { background: var(--blue); color: white; box-shadow: 0 4px 12px rgba(74,144,226,0.3); }
.input-btn:hover { transform: scale(1.1); }

/* Floating badges */
.float-badge {
  position: absolute; background: white; border-radius: 16px;
  padding: 10px 14px; font-size: 0.8rem; font-weight: 600;
  box-shadow: 0 8px 24px rgba(0,0,0,0.1);
  display: flex; align-items: center; gap: 8px;
  animation: float 4s ease-in-out infinite;
  white-space: nowrap;
}

.float-badge.badge-1 { top: 20px; right: -30px; animation-delay: 0s; }
.float-badge.badge-2 { bottom: 60px; left: -40px; animation-delay: 1.5s; }

@keyframes float {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-8px); }
}

/* SECTIONS */
section { padding: 80px 5%; }

.section-label {
  font-size: 0.82rem; font-weight: 700; color: var(--blue);
  text-transform: uppercase; letter-spacing: 1.5px;
  margin-bottom: 12px; display: block;
}

.section-title {
  font-size: clamp(1.8rem, 3.5vw, 2.5rem); font-weight: 900;
  line-height: 1.2; color: var(--text); margin-bottom: 16px;
}

.section-sub { font-size: 1rem; color: var(--gray-600); line-height: 1.7; max-width: 560px; }

/* FEATURES */
.features { background: var(--white); }

.features-header { text-align: center; margin-bottom: 56px; }
.features-header .section-sub { margin: 0 auto; }

.features-grid {
  display: grid; grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: 24px;
}

.feature-card {
  background: var(--white); border: 1.5px solid var(--gray-200);
  border-radius: 24px; padding: 32px 28px;
  transition: all 0.3s; position: relative; overflow: hidden;
  cursor: default;
}

.feature-card::before {
  content: ''; position: absolute; inset: 0; opacity: 0;
  background: linear-gradient(135deg, var(--blue-pale), rgba(255,169,77,0.05));
  transition: opacity 0.3s;
}

.feature-card:hover { transform: translateY(-6px); border-color: rgba(74,144,226,0.3); box-shadow: 0 20px 50px rgba(74,144,226,0.12); }
.feature-card:hover::before { opacity: 1; }

.feature-icon {
  width: 56px; height: 56px; border-radius: 18px;
  display: flex; align-items: center; justify-content: center;
  font-size: 1.5rem; margin-bottom: 20px; position: relative;
}

.feature-icon.blue { background: linear-gradient(135deg, var(--blue-pale), #D6E8FA); }
.feature-icon.orange { background: linear-gradient(135deg, #FFF3E8, #FFE0C2); }
.feature-icon.green { background: linear-gradient(135deg, #ECFDF5, #D1FAE5); }
.feature-icon.purple { background: linear-gradient(135deg, #F5F3FF, #EDE9FE); }

.feature-card h3 { font-size: 1.05rem; font-weight: 800; margin-bottom: 10px; }
.feature-card p { font-size: 0.88rem; color: var(--gray-600); line-height: 1.6; }

.feature-tag {
  display: inline-block; margin-top: 16px;
  background: var(--blue-pale); color: var(--blue);
  font-size: 0.75rem; font-weight: 600; padding: 4px 10px; border-radius: 100px;
}

/* CHATBOT SECTION */
.chatbot-section {
  background: linear-gradient(160deg, #EBF3FD, #F0F7FF);
}

.chatbot-layout {
  display: flex; gap: 60px; align-items: center; flex-wrap: wrap;
}

.chatbot-info { flex: 1; min-width: 280px; }
.chatbot-demo { flex: 1; min-width: 300px; display: flex; justify-content: center; }

.chatbot-full {
  background: white; border-radius: 28px;
  box-shadow: 0 24px 60px rgba(74,144,226,0.15);
  width: 100%; max-width: 380px; overflow: hidden;
}

.chatbot-full .chat-header { padding: 20px 22px; }
.chatbot-full .chat-body { min-height: 320px; padding: 20px; }

.chatbot-features { margin-top: 32px; display: flex; flex-direction: column; gap: 14px; }

.chatbot-feat {
  display: flex; align-items: center; gap: 12px;
  font-size: 0.9rem; color: var(--gray-600);
}

.chatbot-feat-dot {
  width: 10px; height: 10px; border-radius: 50%; flex-shrink: 0;
}

/* DASHBOARD */
.dashboard-section { background: white; }

.dashboard-layout {
  display: flex; gap: 60px; align-items: flex-start; flex-wrap: wrap;
}

.dashboard-info { flex: 1; min-width: 280px; padding-top: 20px; }
.dashboard-visual { flex: 2; min-width: 320px; }

.dashboard-card {
  background: white; border: 1.5px solid var(--gray-200);
  border-radius: 24px; overflow: hidden;
  box-shadow: 0 12px 40px rgba(0,0,0,0.06);
}

.dash-header {
  background: linear-gradient(135deg, #1E293B, #2D3F55);
  padding: 20px 24px;
  display: flex; align-items: center; justify-content: space-between;
}

.dash-header h4 { color: white; font-weight: 700; font-size: 0.95rem; }

.dash-user {
  display: flex; align-items: center; gap: 10px;
}

.dash-avatar {
  width: 36px; height: 36px; background: linear-gradient(135deg, var(--orange), #FFB36B);
  border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 1rem;
}

.dash-user-info h5 { color: white; font-size: 0.83rem; font-weight: 600; }
.dash-user-info p { color: rgba(255,255,255,0.6); font-size: 0.72rem; }

.dash-body { padding: 22px; display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }
.dash-body.wide { grid-template-columns: 1fr; }

.dash-widget {
  background: var(--gray-50); border-radius: 18px; padding: 18px;
  border: 1px solid var(--gray-200);
}

.widget-label { font-size: 0.75rem; font-weight: 600; color: var(--gray-400); margin-bottom: 12px; text-transform: uppercase; letter-spacing: 0.8px; }

/* Progress bars */
.progress-bar-wrap { margin-bottom: 10px; }
.progress-subject { display: flex; justify-content: space-between; align-items: center; margin-bottom: 4px; font-size: 0.8rem; }
.progress-subject span:first-child { font-weight: 600; color: var(--gray-600); }
.progress-subject span:last-child { font-weight: 700; color: var(--text); }

.pbar { height: 6px; background: var(--gray-200); border-radius: 100px; overflow: hidden; }
.pbar-fill { height: 100%; border-radius: 100px; transition: width 1s ease; }
.pbar-fill.math { background: linear-gradient(90deg, var(--blue), #6BA8ED); width: 78%; }
.pbar-fill.lit { background: linear-gradient(90deg, #22C55E, #4ADE80); width: 65%; }
.pbar-fill.eng { background: linear-gradient(90deg, var(--orange), #FFB36B); width: 88%; }
.pbar-fill.phy { background: linear-gradient(90deg, #A855F7, #C084FC); width: 52%; }

/* Heatmap */
.heatmap-grid {
  display: grid; grid-template-columns: repeat(7, 1fr); gap: 4px; margin-top: 4px;
}

.hm-cell {
  aspect-ratio: 1; border-radius: 4px;
  transition: transform 0.2s;
}
.hm-cell:hover { transform: scale(1.3); cursor: default; }

.hm-0 { background: #F1F5F9; }
.hm-1 { background: #BFDBFE; }
.hm-2 { background: #93C5FD; }
.hm-3 { background: #60A5FA; }
.hm-4 { background: var(--blue); }
.hm-5 { background: #3B82F6; }
.hm-6 { background: #EF4444; }
.hm-7 { background: #F97316; }
.hm-8 { background: #EAB308; }
.hm-9 { background: #22C55E; }

/* Podcast widget */
.podcast-item {
  display: flex; align-items: center; gap: 12px; padding: 10px 0;
  border-bottom: 1px solid var(--gray-200);
}
.podcast-item:last-child { border-bottom: none; padding-bottom: 0; }

.podcast-thumb {
  width: 44px; height: 44px; border-radius: 12px;
  display: flex; align-items: center; justify-content: center; font-size: 1.1rem;
  flex-shrink: 0;
}
.podcast-thumb.math { background: var(--blue-pale); }
.podcast-thumb.sci { background: #ECFDF5; }

.podcast-title { font-size: 0.82rem; font-weight: 600; color: var(--text); }
.podcast-meta { font-size: 0.73rem; color: var(--gray-400); margin-top: 2px; }

.podcast-play {
  margin-left: auto; width: 32px; height: 32px;
  background: var(--blue-pale); border-radius: 50%;
  display: flex; align-items: center; justify-content: center;
  font-size: 0.75rem; cursor: pointer; color: var(--blue);
  transition: all 0.2s;
}
.podcast-play:hover { background: var(--blue); color: white; transform: scale(1.1); }

/* Suggestions */
.suggestion-chip {
  display: inline-flex; align-items: center; gap: 6px;
  background: white; border: 1.5px solid var(--gray-200);
  padding: 6px 12px; border-radius: 100px;
  font-size: 0.78rem; font-weight: 600; color: var(--gray-600);
  margin: 4px; cursor: pointer; transition: all 0.2s;
}
.suggestion-chip:hover { border-color: var(--blue); color: var(--blue); background: var(--blue-pale); }

.chip-dot { width: 6px; height: 6px; border-radius: 50%; }

/* CTA */
.cta-section {
  background: linear-gradient(135deg, var(--blue) 0%, #3a7fd0 50%, #2D6BC4 100%);
  text-align: center; padding: 80px 5%;
  position: relative; overflow: hidden;
}

.cta-section::before {
  content: ''; position: absolute;
  top: -50%; left: -50%; width: 200%; height: 200%;
  background: radial-gradient(circle at 30% 50%, rgba(255,255,255,0.06), transparent 40%),
              radial-gradient(circle at 70% 50%, rgba(255,169,77,0.1), transparent 40%);
}

.cta-section h2 { font-size: clamp(2rem, 4vw, 3rem); color: white; font-weight: 900; margin-bottom: 16px; position: relative; }
.cta-section p { color: rgba(255,255,255,0.8); font-size: 1.05rem; margin-bottom: 36px; position: relative; }

.btn-white {
  background: white; color: var(--blue); border: none;
  padding: 15px 36px; border-radius: 100px;
  font-family: 'Nunito', sans-serif; font-weight: 800; font-size: 1rem;
  cursor: pointer; transition: all 0.3s; position: relative;
  box-shadow: 0 8px 28px rgba(0,0,0,0.15);
}
.btn-white:hover { transform: translateY(-3px); box-shadow: 0 14px 36px rgba(0,0,0,0.2); }

/* FOOTER */
footer {
  background: var(--gray-800); color: white;
  padding: 48px 5% 32px;
}

.footer-grid {
  display: grid; grid-template-columns: 2fr 1fr 1fr 1fr; gap: 40px; margin-bottom: 40px;
}

.footer-logo {
  display: flex; align-items: center; gap: 10px;
  font-family: 'Nunito', sans-serif; font-weight: 900; font-size: 1.1rem;
  color: white; margin-bottom: 14px;
}

.footer-logo-icon {
  width: 34px; height: 34px; background: linear-gradient(135deg, var(--blue), #6BA8ED);
  border-radius: 10px; display: flex; align-items: center; justify-content: center;
  font-size: 1rem;
}

.footer-desc { color: rgba(255,255,255,0.5); font-size: 0.85rem; line-height: 1.7; }

.footer-col h5 { font-weight: 700; margin-bottom: 14px; font-size: 0.9rem; color: rgba(255,255,255,0.9); }

.footer-col ul { list-style: none; }
.footer-col ul li { margin-bottom: 8px; }
.footer-col ul li a { color: rgba(255,255,255,0.5); text-decoration: none; font-size: 0.85rem; transition: color 0.2s; }
.footer-col ul li a:hover { color: white; }

.footer-bottom {
  border-top: 1px solid rgba(255,255,255,0.1);
  padding-top: 24px; display: flex; justify-content: space-between; align-items: center;
  flex-wrap: wrap; gap: 10px;
}

.footer-bottom p { color: rgba(255,255,255,0.4); font-size: 0.8rem; }

/* ANIMATIONS */
@keyframes fadeUp {
  from { opacity: 0; transform: translateY(30px); }
  to { opacity: 1; transform: translateY(0); }
}

/* ===== ANALYTICS SECTION ===== */
.analytics-section {
  background: linear-gradient(180deg, #F8FAFF 0%, #EFF6FF 100%);
  padding: 90px 5%;
}

.analytics-header { text-align: center; margin-bottom: 56px; }
.analytics-header .section-sub { margin: 0 auto; max-width: 600px; }

.analytics-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 24px;
  max-width: 1100px;
  margin: 0 auto;
}

/* Big card spanning 2 cols */
.analytics-card {
  background: white;
  border-radius: 24px;
  border: 1.5px solid var(--gray-200);
  padding: 28px;
  box-shadow: 0 6px 28px rgba(74,144,226,0.07);
  transition: box-shadow 0.3s;
}
.analytics-card:hover { box-shadow: 0 14px 44px rgba(74,144,226,0.13); }

.analytics-card.span2 { grid-column: span 2; }

.ac-header {
  display: flex; align-items: center; justify-content: space-between;
  margin-bottom: 22px;
}
.ac-title {
  font-family: 'Nunito', sans-serif; font-size: 1rem; font-weight: 800; color: var(--text);
  display: flex; align-items: center; gap: 8px;
}
.ac-badge {
  font-size: 0.72rem; font-weight: 700; padding: 3px 10px; border-radius: 100px;
  background: var(--blue-pale); color: var(--blue);
}
.ac-badge.green { background: #ECFDF5; color: #059669; }
.ac-badge.orange { background: #FFF3E8; color: var(--orange); }
.ac-badge.purple { background: #F5F3FF; color: #7C3AED; }

/* RADAR CHART (pure CSS) */
.radar-wrap {
  display: flex; align-items: center; gap: 32px; flex-wrap: wrap;
}

.radar-svg-container {
  flex-shrink: 0;
  position: relative;
}

.radar-legend {
  flex: 1; min-width: 180px; display: flex; flex-direction: column; gap: 10px;
}

.legend-item {
  display: flex; align-items: center; justify-content: space-between;
  font-size: 0.84rem;
}
.legend-dot {
  width: 10px; height: 10px; border-radius: 50%; flex-shrink: 0; margin-right: 8px;
}
.legend-name { flex: 1; color: var(--gray-600); font-weight: 500; }
.legend-score {
  font-family: 'Nunito', sans-serif; font-weight: 800; font-size: 0.9rem; color: var(--text);
}
.legend-bar-wrap {
  width: 70px; height: 5px; background: var(--gray-200); border-radius: 100px; margin-left: 8px; overflow: hidden;
}
.legend-bar { height: 100%; border-radius: 100px; }

/* SKILL MATRIX */
.skill-matrix { display: flex; flex-direction: column; gap: 14px; }

.skill-row { }
.skill-row-header {
  display: flex; align-items: center; justify-content: space-between; margin-bottom: 6px;
}
.skill-name { font-size: 0.85rem; font-weight: 600; color: var(--text); }
.skill-level {
  font-size: 0.75rem; font-weight: 700; padding: 2px 8px; border-radius: 100px;
}
.level-master { background: #ECFDF5; color: #059669; }
.level-good { background: var(--blue-pale); color: var(--blue); }
.level-avg { background: #FFF3E8; color: var(--orange); }
.level-weak { background: #FEF2F2; color: #EF4444; }

.skill-bar-track { height: 8px; background: var(--gray-100); border-radius: 100px; overflow: hidden; position: relative; }
.skill-bar-fill { height: 100%; border-radius: 100px; position: relative; }
.skill-bar-fill::after {
  content: '';
  position: absolute; right: 0; top: 50%; transform: translateY(-50%);
  width: 12px; height: 12px; border-radius: 50%; background: inherit;
  filter: brightness(0.85);
  box-shadow: 0 0 0 3px white, 0 0 0 4px currentColor;
}

/* COGNITIVE INDICATORS */
.cog-grid {
  display: grid; grid-template-columns: repeat(3, 1fr); gap: 14px;
}

.cog-item {
  background: var(--gray-50); border-radius: 16px; padding: 16px 14px; text-align: center;
  border: 1px solid var(--gray-200); transition: all 0.2s;
}
.cog-item:hover { background: var(--blue-pale); border-color: rgba(74,144,226,0.3); }

.cog-icon { font-size: 1.5rem; margin-bottom: 8px; }
.cog-label { font-size: 0.73rem; color: var(--gray-400); font-weight: 600; text-transform: uppercase; letter-spacing: 0.5px; margin-bottom: 6px; }

.cog-score-wrap { position: relative; display: inline-flex; align-items: center; justify-content: center; }
.cog-score {
  font-family: 'Nunito', sans-serif; font-weight: 900; font-size: 1.4rem; color: var(--text);
  line-height: 1;
}
.cog-unit { font-size: 0.75rem; color: var(--gray-400); font-weight: 500; margin-left: 2px; }
.cog-trend {
  font-size: 0.72rem; font-weight: 700; margin-top: 4px;
}
.trend-up { color: #22C55E; }
.trend-down { color: #EF4444; }
.trend-neutral { color: var(--gray-400); }

/* AI INSIGHT CARDS */
.insight-list { display: flex; flex-direction: column; gap: 12px; }

.insight-item {
  display: flex; align-items: flex-start; gap: 14px;
  padding: 14px 16px; border-radius: 14px; border: 1.5px solid var(--gray-200);
  transition: all 0.2s; cursor: default;
}
.insight-item:hover { border-color: rgba(74,144,226,0.3); background: var(--blue-pale); }

.insight-icon {
  width: 40px; height: 40px; border-radius: 12px; flex-shrink: 0;
  display: flex; align-items: center; justify-content: center; font-size: 1.1rem;
}
.insight-icon.warn { background: #FEF2F2; }
.insight-icon.good { background: #ECFDF5; }
.insight-icon.tip { background: #FFF3E8; }
.insight-icon.info { background: var(--blue-pale); }

.insight-body { flex: 1; }
.insight-title { font-size: 0.88rem; font-weight: 700; color: var(--text); margin-bottom: 3px; }
.insight-desc { font-size: 0.8rem; color: var(--gray-600); line-height: 1.5; }
.insight-action {
  margin-top: 6px; font-size: 0.75rem; font-weight: 700; color: var(--blue);
  cursor: pointer; display: inline-flex; align-items: center; gap: 4px;
}

/* WEEKLY CHART */
.weekly-chart { display: flex; align-items: flex-end; gap: 8px; height: 110px; padding-top: 10px; }
.week-col { flex: 1; display: flex; flex-direction: column; align-items: center; gap: 6px; }
.week-bar-wrap { flex: 1; width: 100%; display: flex; align-items: flex-end; }
.week-bar {
  width: 100%; border-radius: 8px 8px 0 0;
  min-height: 8px; transition: height 0.5s ease;
  position: relative;
}
.week-bar.today { box-shadow: 0 4px 16px rgba(74,144,226,0.35); }
.week-bar::after {
  content: attr(data-val);
  position: absolute; top: -20px; left: 50%; transform: translateX(-50%);
  font-size: 0.68rem; font-weight: 700; color: var(--gray-400); white-space: nowrap;
}
.week-bar.today::after { color: var(--blue); }
.week-label { font-size: 0.72rem; color: var(--gray-400); font-weight: 600; }

/* LEARNING TYPE */
.type-result {
  display: flex; align-items: center; gap: 20px; flex-wrap: wrap;
}
.type-badge-big {
  background: linear-gradient(135deg, var(--blue), #6BA8ED);
  color: white; border-radius: 20px; padding: 20px 24px; text-align: center;
  min-width: 140px; flex-shrink: 0;
}
.type-badge-big .type-icon { font-size: 2rem; margin-bottom: 6px; }
.type-badge-big .type-name { font-family: 'Nunito', sans-serif; font-weight: 900; font-size: 1rem; }
.type-badge-big .type-sub { font-size: 0.75rem; opacity: 0.85; margin-top: 2px; }

.type-traits { flex: 1; display: flex; flex-direction: column; gap: 8px; }
.trait-item {
  display: flex; align-items: center; gap: 10px; font-size: 0.83rem;
  padding: 8px 12px; background: var(--gray-50); border-radius: 10px;
}
.trait-check { color: #22C55E; font-weight: 700; }

/* FORECAST */
.forecast-row {
  display: flex; gap: 12px; flex-wrap: wrap;
}
.forecast-item {
  flex: 1; min-width: 130px; background: var(--gray-50);
  border-radius: 16px; padding: 16px; border: 1.5px solid var(--gray-200);
  text-align: center;
}
.forecast-subject { font-size: 0.75rem; font-weight: 600; color: var(--gray-400); text-transform: uppercase; letter-spacing: 0.5px; margin-bottom: 6px; }
.forecast-score {
  font-family: 'Nunito', sans-serif; font-weight: 900; font-size: 1.8rem; line-height: 1;
  margin-bottom: 4px;
}
.forecast-change { font-size: 0.78rem; font-weight: 700; }
.forecast-note { font-size: 0.72rem; color: var(--gray-400); margin-top: 4px; }

/* ========================================
   ASSESSMENT SECTION
   ======================================== */
.assessment-section {
  background: linear-gradient(160deg,#FFF8F0 0%,#FFFBF7 50%,#F0F7FF 100%);
  padding: 90px 5%; position: relative; overflow: hidden;
}
.assessment-section::before {
  content:''; position:absolute; top:-120px; right:-120px;
  width:420px; height:420px;
  background:radial-gradient(circle,rgba(255,169,77,0.08),transparent 70%); border-radius:50%;
}
.assessment-header { text-align:center; margin-bottom:52px; }
.assessment-header .section-sub { margin:0 auto; max-width:580px; }
.assessment-layout {
  display:grid; grid-template-columns:1fr 1fr; gap:28px;
  max-width:1100px; margin:0 auto; align-items:start;
}
.asmnt-form-panel {
  background:white; border-radius:24px; border:1.5px solid var(--gray-200);
  overflow:hidden; box-shadow:0 8px 32px rgba(255,169,77,0.1);
}
.asmnt-form-header {
  background:linear-gradient(135deg,#1E293B,#2D3F55);
  padding:20px 24px; display:flex; align-items:center; gap:12px;
}
.asmnt-form-header .fh-icon {
  width:42px; height:42px; background:rgba(255,169,77,0.2);
  border-radius:12px; display:flex; align-items:center; justify-content:center; font-size:1.2rem;
}
.asmnt-form-header h3 { color:white; font-size:1rem; font-weight:800; }
.asmnt-form-header p  { color:rgba(255,255,255,0.6); font-size:0.75rem; margin-top:1px; }
.asmnt-form-body { padding:22px; }
.asmnt-group-label {
  font-size:0.72rem; font-weight:800; text-transform:uppercase; letter-spacing:1.2px;
  margin-bottom:12px; margin-top:4px; display:flex; align-items:center; gap:8px;
}
.asmnt-group-label.req { color:var(--blue); }
.asmnt-group-label.opt { color:var(--gray-400); margin-top:16px; }
.asmnt-tag { font-size:0.65rem; font-weight:700; padding:2px 7px; border-radius:100px; text-transform:none; letter-spacing:0; }
.asmnt-tag.r { background:var(--blue-pale); color:var(--blue); }
.asmnt-tag.o { background:var(--gray-100); color:var(--gray-400); }
.asmnt-subjects-grid { display:grid; grid-template-columns:1fr 1fr; gap:10px; margin-bottom:4px; }
.asmnt-item {
  background:var(--gray-50); border-radius:12px; border:1.5px solid var(--gray-200);
  padding:11px 13px; transition:all 0.2s; position:relative;
}
.asmnt-item:focus-within { border-color:var(--blue); background:var(--blue-pale); box-shadow:0 0 0 3px rgba(74,144,226,0.1); }
.asmnt-item.asmnt-has-value { border-color:rgba(74,144,226,0.35); background:white; }
.asmnt-item.asmnt-error { border-color:#EF4444; background:#FEF2F2; }
.asmnt-subject-name { font-size:0.77rem; font-weight:700; color:var(--gray-600); margin-bottom:6px; display:flex; justify-content:space-between; }
.asmnt-req-star { color:#EF4444; }
.asmnt-score-wrap { display:flex; align-items:center; }
.asmnt-score-input {
  width:100%; border:none; background:transparent; outline:none;
  font-family:'Nunito',sans-serif; font-weight:900; font-size:1rem; color:var(--text);
  border-bottom:2px solid var(--gray-200); padding:4px 30px 4px 4px; transition:border-color 0.2s;
}
.asmnt-score-input:focus { border-color:var(--blue); }
.asmnt-score-input::placeholder { font-size:0.78rem; font-weight:400; font-family:'DM Sans',sans-serif; color:var(--gray-300); }
.asmnt-suffix { position:absolute; right:13px; bottom:14px; font-size:0.68rem; color:var(--gray-400); font-weight:600; }
.asmnt-indicator {
  position:absolute; top:-6px; right:-6px; width:18px; height:18px; border-radius:50%;
  display:none; align-items:center; justify-content:center;
  font-size:0.6rem; font-weight:800; color:white; z-index:1;
  border:2px solid white; box-shadow:0 2px 6px rgba(0,0,0,0.12);
}
.asmnt-item.asmnt-has-value .asmnt-indicator { display:flex; }
.aind-gioi { background:#22C55E; } .aind-kha { background:var(--blue); }
.aind-tb   { background:var(--orange); } .aind-yeu { background:#EF4444; }
.asmnt-err-msg { font-size:0.68rem; color:#EF4444; font-weight:600; margin-top:3px; display:none; }
.asmnt-item.asmnt-error .asmnt-err-msg { display:block; }
.asmnt-divider { height:1px; background:var(--gray-200); margin:16px 0 14px; }
.asmnt-submit-bar {
  padding:16px 22px; background:var(--gray-50); border-top:1px solid var(--gray-200);
  display:flex; gap:10px; align-items:center; flex-wrap:wrap;
}
.asmnt-btn-calc {
  flex:1; background:linear-gradient(135deg,var(--orange),#FF8C00);
  color:white; border:none; padding:13px 20px; border-radius:100px;
  font-family:'Nunito',sans-serif; font-weight:900; font-size:0.92rem; cursor:pointer;
  box-shadow:0 6px 20px rgba(255,140,0,0.3); transition:all 0.3s;
  display:flex; align-items:center; justify-content:center; gap:8px;
}
.asmnt-btn-calc:hover { transform:translateY(-2px); box-shadow:0 10px 28px rgba(255,140,0,0.4); }
.asmnt-btn-reset {
  background:var(--gray-100); color:var(--gray-600); border:none; padding:13px 18px;
  border-radius:100px; font-family:'Nunito',sans-serif; font-weight:700; font-size:0.85rem;
  cursor:pointer; transition:all 0.2s;
}
.asmnt-btn-reset:hover { background:var(--gray-200); }
.asmnt-results-panel { display:flex; flex-direction:column; gap:16px; }
.asmnt-empty-state {
  background:white; border-radius:24px; border:2px dashed var(--gray-200);
  padding:52px 28px; text-align:center;
}
.asmnt-empty-state .empty-icon { font-size:3rem; margin-bottom:14px; }
.asmnt-empty-state h4 { font-size:1rem; font-weight:800; color:var(--text); margin-bottom:8px; }
.asmnt-empty-state p { font-size:0.85rem; color:var(--gray-400); line-height:1.6; }
.asmnt-result-card {
  background:white; border-radius:20px; border:1.5px solid var(--gray-200);
  overflow:hidden; box-shadow:0 4px 16px rgba(0,0,0,0.05);
  animation:asmntFadeIn 0.4s ease both;
}
.asmnt-result-card:nth-child(2){animation-delay:.05s}
.asmnt-result-card:nth-child(3){animation-delay:.1s}
.asmnt-result-card:nth-child(4){animation-delay:.15s}
.asmnt-result-card:nth-child(5){animation-delay:.2s}
.asmnt-result-card:nth-child(6){animation-delay:.25s}
@keyframes asmntFadeIn { from{opacity:0;transform:translateY(16px)} to{opacity:1;transform:translateY(0)} }
.asmnt-banner {
  border-radius:20px; padding:22px 20px; display:flex; align-items:center; gap:18px;
  position:relative; overflow:hidden; animation:asmntFadeIn 0.3s ease both;
}
.asmnt-banner::before { content:''; position:absolute; inset:0; background:radial-gradient(ellipse at 80% 50%,rgba(255,255,255,0.15),transparent 60%); }
.asmnt-banner.gioi { background:linear-gradient(135deg,#059669,#10B981); }
.asmnt-banner.kha  { background:linear-gradient(135deg,#1D4ED8,var(--blue)); }
.asmnt-banner.tb   { background:linear-gradient(135deg,#D97706,var(--orange)); }
.asmnt-banner.yeu  { background:linear-gradient(135deg,#DC2626,#EF4444); }
.asmnt-score-circle {
  width:80px; height:80px; border-radius:50%;
  background:rgba(255,255,255,0.2); border:2.5px solid rgba(255,255,255,0.4);
  display:flex; flex-direction:column; align-items:center; justify-content:center; flex-shrink:0;
}
.asmnt-score-num { font-family:'Nunito',sans-serif; font-weight:900; font-size:1.7rem; color:white; line-height:1; }
.asmnt-score-lbl { font-size:0.65rem; color:rgba(255,255,255,0.85); font-weight:600; }
.asmnt-banner-info { flex:1; position:relative; }
.asmnt-banner-rank { font-family:'Nunito',sans-serif; font-weight:900; font-size:1.3rem; color:white; }
.asmnt-banner-sub  { color:rgba(255,255,255,0.8); font-size:0.78rem; margin-top:4px; line-height:1.5; }
.asmnt-banner-count { display:inline-flex;align-items:center;gap:5px;background:rgba(255,255,255,0.2);padding:3px 10px;border-radius:100px;font-size:0.7rem;font-weight:600;color:white;margin-top:7px; }
.arc-head { padding:14px 18px; border-bottom:1px solid var(--gray-100); display:flex; align-items:center; gap:10px; }
.arc-icon { width:34px;height:34px;border-radius:10px;display:flex;align-items:center;justify-content:center;font-size:1rem;flex-shrink:0; }
.arc-icon.blue{background:var(--blue-pale)} .arc-icon.green{background:#ECFDF5}
.arc-icon.orange{background:#FFF3E8} .arc-icon.purple{background:#F5F3FF} .arc-icon.yellow{background:#FEFCE8}
.arc-title { font-size:0.88rem; font-weight:800; color:var(--text); }
.arc-sub   { font-size:0.72rem; color:var(--gray-400); margin-top:1px; }
.arc-body  { padding:16px 18px; }
.arc-table { width:100%;border-collapse:collapse; }
.arc-table th { font-size:0.68rem;font-weight:700;color:var(--gray-400);text-transform:uppercase;letter-spacing:0.8px;padding:0 0 8px;border-bottom:1.5px solid var(--gray-200);text-align:left; }
.arc-table th:last-child{text-align:right}
.arc-table td { padding:7px 0;font-size:0.82rem;border-bottom:1px solid var(--gray-100);vertical-align:middle; }
.arc-table tr:last-child td { border-bottom:none; }
.atd-score { text-align:center;font-family:'Nunito',sans-serif;font-weight:900;font-size:0.95rem; }
.atd-rank  { text-align:right; }
.a-pill { display:inline-flex;align-items:center;padding:2px 7px;border-radius:100px;font-size:0.68rem;font-weight:700; }
.a-pill-gioi{background:#ECFDF5;color:#059669} .a-pill-kha{background:var(--blue-pale);color:#1D4ED8}
.a-pill-tb{background:#FFF3E8;color:#D97706} .a-pill-yeu{background:#FEF2F2;color:#DC2626}
.asmnt-tendency-list { display:flex;flex-direction:column;gap:10px; }
.asmnt-tend-item { display:flex;align-items:flex-start;gap:10px;padding:11px 13px;border-radius:12px;border:1.5px solid transparent; }
.asmnt-tend-item.strong{background:#ECFDF5;border-color:rgba(34,197,94,0.2)}
.asmnt-tend-item.medium{background:var(--blue-pale);border-color:rgba(74,144,226,0.15)}
.asmnt-tend-item.weak{background:var(--gray-50);border-color:var(--gray-200)}
.asmnt-tend-icon { width:32px;height:32px;border-radius:9px;flex-shrink:0;display:flex;align-items:center;justify-content:center;font-size:0.95rem; }
.asmnt-tend-item.strong .asmnt-tend-icon{background:rgba(34,197,94,0.15)}
.asmnt-tend-item.medium .asmnt-tend-icon{background:rgba(74,144,226,0.12)}
.asmnt-tend-item.weak   .asmnt-tend-icon{background:var(--gray-200)}
.asmnt-tend-body { flex:1; }
.asmnt-tend-title { font-size:0.84rem;font-weight:700;color:var(--text); }
.asmnt-tend-desc  { font-size:0.75rem;color:var(--gray-600);margin-top:2px;line-height:1.5; }
.asmnt-tend-score { font-family:'Nunito',sans-serif;font-weight:900;font-size:0.8rem;background:rgba(255,255,255,0.7);padding:2px 8px;border-radius:100px;white-space:nowrap;flex-shrink:0;align-self:center; }
.asmnt-combo-wrap { display:flex;flex-wrap:wrap;gap:8px; }
.asmnt-combo-chip { background:var(--blue-pale);border:1.5px solid rgba(74,144,226,0.2);border-radius:12px;padding:9px 12px;transition:all 0.2s; }
.asmnt-combo-chip:hover { border-color:var(--blue);box-shadow:0 4px 12px rgba(74,144,226,0.12); }
.asmnt-combo-code { font-family:'Nunito',sans-serif;font-weight:900;font-size:0.95rem;color:var(--blue); }
.asmnt-combo-name { font-size:0.72rem;color:var(--gray-600);margin-top:2px; }
.asmnt-career-wrap { display:flex;flex-wrap:wrap;gap:8px; }
.asmnt-career-tag { display:flex;align-items:center;gap:5px;background:white;border:1.5px solid var(--gray-200);padding:6px 12px;border-radius:100px;font-size:0.8rem;font-weight:600;color:var(--gray-600);transition:all 0.2s; }
.asmnt-career-tag:hover { border-color:var(--blue);color:var(--blue);background:var(--blue-pale); }
.asmnt-advice-list { display:flex;flex-direction:column;gap:9px; }
.asmnt-advice-item { display:flex;gap:10px;padding:11px 14px;background:var(--gray-50);border-radius:11px;border-left:3px solid transparent;transition:all 0.2s; }
.asmnt-advice-item:hover { background:var(--blue-pale);border-left-color:var(--blue); }
.asmnt-advice-num { width:22px;height:22px;border-radius:50%;flex-shrink:0;background:var(--blue-pale);color:var(--blue);font-family:'Nunito',sans-serif;font-weight:900;font-size:0.72rem;display:flex;align-items:center;justify-content:center; }
.asmnt-advice-text { font-size:0.82rem;color:var(--gray-600);line-height:1.6; }
.asmnt-advice-text strong { color:var(--text); }
.asmnt-sw-item { margin-bottom:8px; }
.asmnt-sw-row  { display:flex;justify-content:space-between;align-items:center;margin-bottom:4px; }
.asmnt-sw-name { font-size:0.8rem;font-weight:600;color:var(--text); }
.asmnt-sw-val  { font-family:'Nunito',sans-serif;font-weight:800;font-size:0.85rem; }
.asmnt-sw-bar  { height:6px;background:var(--gray-100);border-radius:100px;overflow:hidden; }
.asmnt-sw-fill { height:100%;border-radius:100px; }
@media(max-width:900px){ .assessment-layout { grid-template-columns:1fr; } }
@media(max-width:560px){ .asmnt-subjects-grid { grid-template-columns:1fr; } }

/* MOBILE */
.hamburger { display: none; background: none; border: none; font-size: 1.4rem; cursor: pointer; color: var(--gray-600); }

@media (max-width: 768px) {
  .nav-links { display: none; }
  .hamburger { display: block; }

  .hero { flex-direction: column; text-align: center; padding-top: 90px; }
  .hero-sub { margin: 0 auto 32px; }
  .hero-cta { justify-content: center; }
  .hero-stats { justify-content: center; }
  .hero-visual { margin-top: 40px; }
  .float-badge { display: none; }
  .chat-card { width: 300px; }

  .chatbot-layout { flex-direction: column-reverse; }
  .dashboard-layout { flex-direction: column; }
  .dash-body { grid-template-columns: 1fr; }

  .footer-grid { grid-template-columns: 1fr 1fr; }

  .hero::before, .hero::after { display: none; }
  .analytics-grid { grid-template-columns: 1fr; }
  .analytics-card.span2 { grid-column: span 1; }
  .cog-grid { grid-template-columns: repeat(2, 1fr); }
  .radar-wrap { flex-direction: column; align-items: center; }
}
</style>
</head>
<body>

<!-- NAV -->
<nav>
  <a href="#" class="logo">
    <span class="logo-icon">🤖</span>
    AI Study Buddy
  </a>
  <ul class="nav-links">
    <li><a href="#">Trang chủ</a></li>
    <li><a href="#features">Tính năng</a></li>
    <li><a href="#dashboard">Lộ trình học</a></li>
    <li><a href="#analytics">Phân tích</a></li>
    <li><a href="#assessment" style="color:var(--orange);font-weight:700;">🎯 Đánh giá năng lực</a></li>
    <li><a href="#" class="btn-login">Đăng nhập</a></li>
  </ul>
  <button class="hamburger">☰</button>
</nav>

<!-- HERO -->
<section class="hero">
  <div class="hero-content">
    <span class="hero-badge">
      <span class="dot"></span>
      Trợ lý AI học tập đầu tiên tại Việt Nam
    </span>

    <h1>
      AI không đưa<br>
      <span class="accent">đáp án –</span> AI<br>
      <span class="accent-orange">dẫn đường</span>
    </h1>

    <p class="hero-sub">
      Trợ lý học tập 24/7 giúp bạn hiểu bài, không chỉ chép bài.
      Cá nhân hóa theo từng học sinh THCS – THPT.
    </p>

    <div class="hero-cta">
      <a href="#" class="btn-primary">
        🚀 Bắt đầu học ngay
      </a>
      <button class="btn-secondary">
        <span class="play-icon">▶</span>
        Xem demo
      </button>
    </div>

    <div class="hero-stats">
      <div class="stat">
        <div class="stat-number">50K+</div>
        <div class="stat-label">Học sinh đang dùng</div>
      </div>
      <div class="stat">
        <div class="stat-number">4.9★</div>
        <div class="stat-label">Đánh giá trung bình</div>
      </div>
      <div class="stat">
        <div class="stat-number">24/7</div>
        <div class="stat-label">Hỗ trợ liên tục</div>
      </div>
    </div>
  </div>

  <div class="hero-visual">
    <div style="position: relative;">
      <!-- Chat Demo Card -->
      <div class="chat-card">
        <div class="chat-header">
          <div class="chat-avatar">🤖</div>
          <div class="chat-header-info">
            <h4>AI Study Buddy</h4>
            <p>Gia sư Socratic 24/7</p>
          </div>
          <div class="chat-online">
            <span class="chat-online-dot"></span>
            Online
          </div>
        </div>
        <div class="chat-body">
          <div class="chat-status">
            <span>⚡</span> AI đang phân tích bài tập…
            <span class="analyzing-dots"><span></span><span></span><span></span></span>
          </div>
          <div class="msg">
            <div class="msg-avatar bot">🤖</div>
            <div class="bubble bot">Em đang gặp khó khăn ở bước nào trong bài toán này?</div>
          </div>
          <div class="msg user">
            <div class="msg-avatar user-a">😊</div>
            <div class="bubble user">Con không hiểu sao lại dùng đạo hàm ở đây ạ…</div>
          </div>
          <div class="msg">
            <div class="msg-avatar bot">🤖</div>
            <div class="bubble bot">Hay lắm! Thử nghĩ xem – tốc độ thay đổi của hàm số nghĩa là gì với em? 🤔</div>
          </div>
          <div class="msg user">
            <div class="msg-avatar user-a">😊</div>
            <div class="bubble user">Ồ là độ dốc phải không ạ?</div>
          </div>
        </div>
        <div class="chat-input">
          <input class="input-field" placeholder="Nhập câu hỏi của bạn…" readonly>
          <div class="input-actions">
            <button class="input-btn file">📎</button>
            <button class="input-btn mic">🎙️</button>
            <button class="input-btn send">➤</button>
          </div>
        </div>
      </div>

      <!-- Floating badges -->
      <div class="float-badge badge-1">
        🎯 Đúng rồi! +10 XP
      </div>
      <div class="float-badge badge-2">
        📊 Tiến độ: 78%
      </div>
    </div>
  </div>
</section>

<!-- FEATURES -->
<section class="features" id="features">
  <div class="features-header">
    <span class="section-label">Tính năng nổi bật</span>
    <h2 class="section-title">Học thông minh hơn, không phải<br>chăm chỉ hơn</h2>
    <p class="section-sub">Bộ công cụ AI được thiết kế riêng cho cách học của học sinh Việt Nam.</p>
  </div>

  <div class="features-grid">
    <div class="feature-card">
      <div class="feature-icon blue">💬</div>
      <h3>Gia sư Socratic 24/7</h3>
      <p>AI không cho đáp án – AI đặt câu hỏi dẫn dắt để em tự tìm ra lời giải. Phương pháp Socratic hiện đại.</p>
      <span class="feature-tag">Học sâu hơn</span>
    </div>

    <div class="feature-card">
      <div class="feature-icon orange">🎧</div>
      <h3>Podcast học tập cá nhân</h3>
      <p>Podcast tự động tạo từ nội dung yếu của em. Học trên đường đi học, trước giờ ngủ – bất cứ lúc nào.</p>
      <span class="feature-tag" style="background:#FFF3E8; color:var(--orange);">Học mọi lúc</span>
    </div>

    <div class="feature-card">
      <div class="feature-icon green">🗺️</div>
      <h3>Knowledge Gap Map</h3>
      <p>Bản đồ nhiệt thể hiện rõ kiến thức nào em nắm vững, kiến thức nào cần ôn tập ngay hôm nay.</p>
      <span class="feature-tag" style="background:#ECFDF5; color:#059669;">Nhìn rõ điểm yếu</span>
    </div>

    <div class="feature-card">
      <div class="feature-icon purple">💜</div>
      <h3>Emotional Support AI</h3>
      <p>Khi áp lực học, AI sẽ lắng nghe và hỗ trợ tinh thần. Học tốt bắt đầu từ trạng thái tâm lý khỏe mạnh.</p>
      <span class="feature-tag" style="background:#F5F3FF; color:#7C3AED;">Cân bằng cảm xúc</span>
    </div>
    <div class="feature-card" style="border-color:rgba(255,169,77,0.3);background:linear-gradient(135deg,#FFFBF5,white);">
      <div class="feature-icon orange">🎯</div>
      <h3>Đánh giá năng lực GDPT 2018</h3>
      <p>Nhập điểm 11 môn học, AI phân tích thiên hướng, gợi ý tổ hợp thi THPT và ngành nghề phù hợp.</p>
      <span class="feature-tag" style="background:#FFF3E8; color:var(--orange);">Mới · Miễn phí</span>
    </div>
  </div>
</section>
<section class="chatbot-section" id="chatbot">
  <div class="chatbot-layout">
    <div class="chatbot-info">
      <span class="section-label">Giao diện Chat</span>
      <h2 class="section-title">Trò chuyện tự nhiên như với gia sư thật</h2>
      <p class="section-sub">Gửi ảnh bài tập, ghi âm câu hỏi, hoặc gõ văn bản – AI phân tích tức thì và hướng dẫn từng bước.</p>

      <div class="chatbot-features">
        <div class="chatbot-feat">
          <span class="chatbot-feat-dot" style="background:var(--blue)"></span>
          <span>Nhận diện bài tập từ ảnh chụp</span>
        </div>
        <div class="chatbot-feat">
          <span class="chatbot-feat-dot" style="background:var(--orange)"></span>
          <span>Ghi âm câu hỏi bằng giọng nói</span>
        </div>
        <div class="chatbot-feat">
          <span class="chatbot-feat-dot" style="background:#22C55E"></span>
          <span>Phân tích lỗi sai và giải thích nguyên nhân</span>
        </div>
        <div class="chatbot-feat">
          <span class="chatbot-feat-dot" style="background:#A855F7"></span>
          <span>Gợi ý bài tập tương tự để luyện tập</span>
        </div>
      </div>
    </div>

    <div class="chatbot-demo">
      <div class="chatbot-full">
        <div class="chat-header">
          <div class="chat-avatar">🤖</div>
          <div class="chat-header-info">
            <h4>AI Study Buddy</h4>
            <p>Toán lớp 11 · Đạo hàm</p>
          </div>
          <div class="chat-online">
            <span class="chat-online-dot"></span>
            Đang hoạt động
          </div>
        </div>
        <div class="chat-body">
          <div class="chat-status">
            📸 Đã nhận ảnh bài tập · đang phân tích
            <span class="analyzing-dots"><span></span><span></span><span></span></span>
          </div>

          <!-- Image message simulation -->
          <div class="msg user" style="margin-bottom: 14px;">
            <div class="msg-avatar user-a">😊</div>
            <div class="bubble user" style="background: rgba(255,255,255,0.15); backdrop-filter: blur(10px);">
              <div style="background: rgba(255,255,255,0.2); border-radius: 10px; padding: 8px; font-size: 0.78rem; margin-bottom: 4px;">📷 bai_tap_dao_ham.jpg</div>
              Con không hiểu bài này ạ
            </div>
          </div>

          <div class="msg">
            <div class="msg-avatar bot">🤖</div>
            <div class="bubble bot">Mình thấy em đang làm bài <strong>tìm đạo hàm f(x) = x³ - 3x + 2</strong>. Em đã nhớ quy tắc đạo hàm của xⁿ chưa? 🤔</div>
          </div>

          <div class="msg user">
            <div class="msg-avatar user-a">😊</div>
            <div class="bubble user">Là n·x^(n-1) phải không ạ?</div>
          </div>

          <div class="msg">
            <div class="msg-avatar bot">🤖</div>
            <div class="bubble bot">Chính xác! ⭐ Bây giờ áp dụng vào từng số hạng nhé – x³ sẽ cho ta gì?</div>
          </div>
        </div>
        <div class="chat-input">
          <input class="input-field" placeholder="Hỏi bất cứ điều gì…" readonly>
          <div class="input-actions">
            <button class="input-btn file" title="Gửi ảnh">📎</button>
            <button class="input-btn mic" title="Ghi âm">🎙️</button>
            <button class="input-btn send">➤</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- DASHBOARD -->
<section class="dashboard-section" id="dashboard">
  <div class="dashboard-layout">
    <div class="dashboard-info">
      <span class="section-label">Dashboard cá nhân</span>
      <h2 class="section-title">Nhìn thấy hành trình học tập của mình</h2>
      <p class="section-sub">Theo dõi tiến độ từng môn, phát hiện điểm yếu cần cải thiện, và nhận gợi ý ôn tập thông minh mỗi ngày.</p>
      <div style="margin-top: 28px;">
        <a href="#" class="btn-primary" style="display: inline-flex;">Xem Dashboard →</a>
      </div>
    </div>

    <div class="dashboard-visual">
      <div class="dashboard-card">
        <!-- Header -->
        <div class="dash-header">
          <div class="dash-user">
            <div class="dash-avatar">👩‍🎓</div>
            <div class="dash-user-info">
              <h5>Nguyễn Minh Anh</h5>
              <p>Lớp 11A2 · THPT Chu Văn An</p>
            </div>
          </div>
          <div style="text-align: right;">
            <div style="color: var(--orange); font-size: 0.85rem; font-weight: 700;">🔥 15 ngày streak</div>
            <div style="color: rgba(255,255,255,0.5); font-size: 0.72rem;">480 XP tuần này</div>
          </div>
        </div>

        <!-- Body -->
        <div class="dash-body">
          <!-- Progress -->
          <div class="dash-widget">
            <div class="widget-label">📈 Tiến độ học tập</div>
            <div class="progress-bar-wrap">
              <div class="progress-subject"><span>Toán</span><span>78%</span></div>
              <div class="pbar"><div class="pbar-fill math"></div></div>
            </div>
            <div class="progress-bar-wrap">
              <div class="progress-subject"><span>Văn</span><span>65%</span></div>
              <div class="pbar"><div class="pbar-fill lit"></div></div>
            </div>
            <div class="progress-bar-wrap">
              <div class="progress-subject"><span>Tiếng Anh</span><span>88%</span></div>
              <div class="pbar"><div class="pbar-fill eng"></div></div>
            </div>
            <div class="progress-bar-wrap">
              <div class="progress-subject"><span>Vật lý</span><span>52%</span></div>
              <div class="pbar"><div class="pbar-fill phy"></div></div>
            </div>
          </div>

          <!-- Heatmap -->
          <div class="dash-widget">
            <div class="widget-label">🗺️ Knowledge Heatmap</div>
            <div style="font-size: 0.72rem; color: var(--gray-400); margin-bottom: 8px;">Tháng 3, 2025 · Toán</div>
            <div class="heatmap-grid">
              <div class="hm-cell hm-3"></div><div class="hm-cell hm-5"></div><div class="hm-cell hm-0"></div><div class="hm-cell hm-4"></div><div class="hm-cell hm-2"></div><div class="hm-cell hm-6"></div><div class="hm-cell hm-1"></div>
              <div class="hm-cell hm-9"></div><div class="hm-cell hm-4"></div><div class="hm-cell hm-8"></div><div class="hm-cell hm-3"></div><div class="hm-cell hm-7"></div><div class="hm-cell hm-5"></div><div class="hm-cell hm-2"></div>
              <div class="hm-cell hm-0"></div><div class="hm-cell hm-6"></div><div class="hm-cell hm-4"></div><div class="hm-cell hm-9"></div><div class="hm-cell hm-1"></div><div class="hm-cell hm-3"></div><div class="hm-cell hm-5"></div>
              <div class="hm-cell hm-8"></div><div class="hm-cell hm-2"></div><div class="hm-cell hm-7"></div><div class="hm-cell hm-4"></div><div class="hm-cell hm-0"></div><div class="hm-cell hm-6"></div><div class="hm-cell hm-9"></div>
            </div>
            <div style="display: flex; align-items: center; gap: 6px; margin-top: 10px; font-size: 0.7rem; color: var(--gray-400);">
              <span>Yếu</span>
              <div style="display: flex; gap: 2px;">
                <div style="width:10px;height:10px;border-radius:2px;background:#F1F5F9;"></div>
                <div style="width:10px;height:10px;border-radius:2px;background:#93C5FD;"></div>
                <div style="width:10px;height:10px;border-radius:2px;background:var(--blue);"></div>
                <div style="width:10px;height:10px;border-radius:2px;background:#EAB308;"></div>
                <div style="width:10px;height:10px;border-radius:2px;background:#22C55E;"></div>
              </div>
              <span>Tốt</span>
            </div>
          </div>
        </div>

        <!-- Podcast today -->
        <div style="padding: 0 22px 20px;">
          <div class="dash-widget">
            <div class="widget-label">🎧 Podcast hôm nay</div>
            <div class="podcast-item">
              <div class="podcast-thumb math">📐</div>
              <div>
                <div class="podcast-title">Đạo hàm và ứng dụng thực tế</div>
                <div class="podcast-meta">Toán 11 · 8 phút · Cá nhân hóa cho em</div>
              </div>
              <div class="podcast-play">▶</div>
            </div>
            <div class="podcast-item">
              <div class="podcast-thumb sci">🔬</div>
              <div>
                <div class="podcast-title">Dao động điều hòa – ôn tập nhanh</div>
                <div class="podcast-meta">Vật lý 11 · 6 phút · Điểm yếu của em</div>
              </div>
              <div class="podcast-play">▶</div>
            </div>
          </div>

          <!-- Suggestions -->
          <div class="dash-widget" style="margin-top: 14px;">
            <div class="widget-label">💡 Gợi ý ôn tập</div>
            <div>
              <span class="suggestion-chip"><span class="chip-dot" style="background:#EF4444;"></span> Cực trị hàm số</span>
              <span class="suggestion-chip"><span class="chip-dot" style="background:#F97316;"></span> Dao động điều hòa</span>
              <span class="suggestion-chip"><span class="chip-dot" style="background:#EAB308;"></span> Phép đọc hiểu</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- ANALYTICS SECTION -->
<section class="analytics-section" id="analytics">
  <div class="analytics-header">
    <span class="section-label">Phân tích năng lực học tập</span>
    <h2 class="section-title">Hiểu chính mình để học hiệu quả hơn</h2>
    <p class="section-sub">AI liên tục đánh giá năng lực tư duy, phong cách học và dự báo kết quả – giúp bạn đầu tư đúng chỗ.</p>
  </div>

  <div class="analytics-grid">

    <!-- RADAR CHART -->
    <div class="analytics-card">
      <div class="ac-header">
        <div class="ac-title">🕸️ Bản đồ năng lực tổng thể</div>
        <span class="ac-badge">Cập nhật hôm nay</span>
      </div>
      <div class="radar-wrap">
        <div class="radar-svg-container">
          <svg width="200" height="200" viewBox="0 0 200 200">
            <!-- Background hexagons -->
            <polygon points="100,20 168,60 168,140 100,180 32,140 32,60" fill="none" stroke="#E2E8F0" stroke-width="1"/>
            <polygon points="100,40 152,72 152,128 100,160 48,128 48,72" fill="none" stroke="#E2E8F0" stroke-width="1"/>
            <polygon points="100,60 136,84 136,116 100,140 64,116 64,84" fill="none" stroke="#E2E8F0" stroke-width="1"/>
            <polygon points="100,80 120,92 120,108 100,120 80,108 80,92" fill="none" stroke="#E2E8F0" stroke-width="1"/>
            <!-- Axis lines -->
            <line x1="100" y1="20" x2="100" y2="100" stroke="#E2E8F0" stroke-width="1"/>
            <line x1="168" y1="60" x2="100" y2="100" stroke="#E2E8F0" stroke-width="1"/>
            <line x1="168" y1="140" x2="100" y2="100" stroke="#E2E8F0" stroke-width="1"/>
            <line x1="100" y1="180" x2="100" y2="100" stroke="#E2E8F0" stroke-width="1"/>
            <line x1="32" y1="140" x2="100" y2="100" stroke="#E2E8F0" stroke-width="1"/>
            <line x1="32" y1="60" x2="100" y2="100" stroke="#E2E8F0" stroke-width="1"/>
            <!-- Data polygon: Tư duy logic 85%, Ghi nhớ 72%, Phân tích 90%, Sáng tạo 65%, Ngôn ngữ 78%, Toán học 82% -->
            <polygon
              points="100,31 158,65 159,133 100,164 49,127 44,67"
              fill="rgba(74,144,226,0.18)" stroke="#4A90E2" stroke-width="2.5" stroke-linejoin="round"/>
            <!-- Data dots -->
            <circle cx="100" cy="31" r="5" fill="#4A90E2"/>
            <circle cx="158" cy="65" r="5" fill="#4A90E2"/>
            <circle cx="159" cy="133" r="5" fill="#4A90E2"/>
            <circle cx="100" cy="164" r="5" fill="#4A90E2"/>
            <circle cx="49" cy="127" r="5" fill="#4A90E2"/>
            <circle cx="44" cy="67" r="5" fill="#4A90E2"/>
            <!-- Labels -->
            <text x="100" y="14" text-anchor="middle" font-size="9" font-family="Nunito" font-weight="700" fill="#475569">Tư duy logic</text>
            <text x="176" y="62" text-anchor="start" font-size="9" font-family="Nunito" font-weight="700" fill="#475569">Ghi nhớ</text>
            <text x="176" y="142" text-anchor="start" font-size="9" font-family="Nunito" font-weight="700" fill="#475569">Phân tích</text>
            <text x="100" y="194" text-anchor="middle" font-size="9" font-family="Nunito" font-weight="700" fill="#475569">Sáng tạo</text>
            <text x="24" y="142" text-anchor="end" font-size="9" font-family="Nunito" font-weight="700" fill="#475569">Ngôn ngữ</text>
            <text x="24" y="62" text-anchor="end" font-size="9" font-family="Nunito" font-weight="700" fill="#475569">Toán học</text>
          </svg>
        </div>
        <div class="radar-legend">
          <div class="legend-item">
            <span class="legend-dot" style="background:#4A90E2;"></span>
            <span class="legend-name">Tư duy logic</span>
            <span class="legend-score">85</span>
            <div class="legend-bar-wrap"><div class="legend-bar" style="width:85%;background:linear-gradient(90deg,var(--blue),#6BA8ED);"></div></div>
          </div>
          <div class="legend-item">
            <span class="legend-dot" style="background:#22C55E;"></span>
            <span class="legend-name">Ghi nhớ</span>
            <span class="legend-score">72</span>
            <div class="legend-bar-wrap"><div class="legend-bar" style="width:72%;background:linear-gradient(90deg,#22C55E,#4ADE80);"></div></div>
          </div>
          <div class="legend-item">
            <span class="legend-dot" style="background:#6BA8ED;"></span>
            <span class="legend-name">Phân tích</span>
            <span class="legend-score">90</span>
            <div class="legend-bar-wrap"><div class="legend-bar" style="width:90%;background:linear-gradient(90deg,#3B82F6,#60A5FA);"></div></div>
          </div>
          <div class="legend-item">
            <span class="legend-dot" style="background:var(--orange);"></span>
            <span class="legend-name">Sáng tạo</span>
            <span class="legend-score">65</span>
            <div class="legend-bar-wrap"><div class="legend-bar" style="width:65%;background:linear-gradient(90deg,var(--orange),#FFB36B);"></div></div>
          </div>
          <div class="legend-item">
            <span class="legend-dot" style="background:#A855F7;"></span>
            <span class="legend-name">Ngôn ngữ</span>
            <span class="legend-score">78</span>
            <div class="legend-bar-wrap"><div class="legend-bar" style="width:78%;background:linear-gradient(90deg,#A855F7,#C084FC);"></div></div>
          </div>
          <div class="legend-item">
            <span class="legend-dot" style="background:#1D4ED8;"></span>
            <span class="legend-name">Toán học</span>
            <span class="legend-score">82</span>
            <div class="legend-bar-wrap"><div class="legend-bar" style="width:82%;background:linear-gradient(90deg,#1D4ED8,#3B82F6);"></div></div>
          </div>
        </div>
      </div>
    </div>

    <!-- COGNITIVE INDICATORS -->
    <div class="analytics-card">
      <div class="ac-header">
        <div class="ac-title">🧠 Chỉ số tư duy</div>
        <span class="ac-badge green">Tuần này</span>
      </div>
      <div class="cog-grid">
        <div class="cog-item">
          <div class="cog-icon">⚡</div>
          <div class="cog-label">Tốc độ học</div>
          <div class="cog-score-wrap">
            <span class="cog-score">8.4</span>
            <span class="cog-unit">/10</span>
          </div>
          <div class="cog-trend trend-up">↑ +0.6 so tuần trước</div>
        </div>
        <div class="cog-item">
          <div class="cog-icon">🎯</div>
          <div class="cog-label">Độ chính xác</div>
          <div class="cog-score-wrap">
            <span class="cog-score">76</span>
            <span class="cog-unit">%</span>
          </div>
          <div class="cog-trend trend-up">↑ +4% so tuần trước</div>
        </div>
        <div class="cog-item">
          <div class="cog-icon">🔄</div>
          <div class="cog-label">Giữ kiến thức</div>
          <div class="cog-score-wrap">
            <span class="cog-score">83</span>
            <span class="cog-unit">%</span>
          </div>
          <div class="cog-trend trend-up">↑ +2% so tháng trước</div>
        </div>
        <div class="cog-item">
          <div class="cog-icon">🧩</div>
          <div class="cog-label">Vận dụng</div>
          <div class="cog-score-wrap">
            <span class="cog-score">7.1</span>
            <span class="cog-unit">/10</span>
          </div>
          <div class="cog-trend trend-down">↓ -0.3 cần cải thiện</div>
        </div>
        <div class="cog-item">
          <div class="cog-icon">⏱️</div>
          <div class="cog-label">Tập trung tb</div>
          <div class="cog-score-wrap">
            <span class="cog-score">42</span>
            <span class="cog-unit">phút</span>
          </div>
          <div class="cog-trend trend-up">↑ +8 phút</div>
        </div>
        <div class="cog-item">
          <div class="cog-icon">💡</div>
          <div class="cog-label">Câu hỏi hay</div>
          <div class="cog-score-wrap">
            <span class="cog-score">14</span>
            <span class="cog-unit">câu</span>
          </div>
          <div class="cog-trend trend-neutral">= Ổn định</div>
        </div>
      </div>
    </div>

    <!-- SKILL MASTERY -->
    <div class="analytics-card">
      <div class="ac-header">
        <div class="ac-title">📚 Mức độ thành thạo từng kỹ năng</div>
        <span class="ac-badge orange">Toán lớp 11</span>
      </div>
      <div class="skill-matrix">
        <div class="skill-row">
          <div class="skill-row-header">
            <span class="skill-name">Giới hạn & Liên tục</span>
            <span class="skill-level level-master">Thành thạo</span>
          </div>
          <div class="skill-bar-track">
            <div class="skill-bar-fill" style="width:92%;background:linear-gradient(90deg,#22C55E,#4ADE80);"></div>
          </div>
        </div>
        <div class="skill-row">
          <div class="skill-row-header">
            <span class="skill-name">Đạo hàm cơ bản</span>
            <span class="skill-level level-good">Khá tốt</span>
          </div>
          <div class="skill-bar-track">
            <div class="skill-bar-fill" style="width:78%;background:linear-gradient(90deg,var(--blue),#6BA8ED);"></div>
          </div>
        </div>
        <div class="skill-row">
          <div class="skill-row-header">
            <span class="skill-name">Ứng dụng đạo hàm</span>
            <span class="skill-level level-avg">Trung bình</span>
          </div>
          <div class="skill-bar-track">
            <div class="skill-bar-fill" style="width:58%;background:linear-gradient(90deg,var(--orange),#FFB36B);"></div>
          </div>
        </div>
        <div class="skill-row">
          <div class="skill-row-header">
            <span class="skill-name">Cực trị hàm số</span>
            <span class="skill-level level-weak">Cần ôn tập</span>
          </div>
          <div class="skill-bar-track">
            <div class="skill-bar-fill" style="width:38%;background:linear-gradient(90deg,#EF4444,#F87171);"></div>
          </div>
        </div>
        <div class="skill-row">
          <div class="skill-row-header">
            <span class="skill-name">Tích phân bất định</span>
            <span class="skill-level level-avg">Trung bình</span>
          </div>
          <div class="skill-bar-track">
            <div class="skill-bar-fill" style="width:52%;background:linear-gradient(90deg,var(--orange),#FFB36B);"></div>
          </div>
        </div>
      </div>
    </div>

    <!-- WEEKLY CHART -->
    <div class="analytics-card">
      <div class="ac-header">
        <div class="ac-title">📅 Hoạt động học trong tuần</div>
        <span class="ac-badge">Giờ / ngày</span>
      </div>
      <div class="weekly-chart">
        <div class="week-col">
          <div class="week-bar-wrap">
            <div class="week-bar" data-val="1.5h" style="height:45%;background:var(--blue-pale);"></div>
          </div>
          <div class="week-label">T2</div>
        </div>
        <div class="week-col">
          <div class="week-bar-wrap">
            <div class="week-bar" data-val="2.2h" style="height:66%;background:var(--blue-pale);"></div>
          </div>
          <div class="week-label">T3</div>
        </div>
        <div class="week-col">
          <div class="week-bar-wrap">
            <div class="week-bar" data-val="1.0h" style="height:30%;background:var(--blue-pale);"></div>
          </div>
          <div class="week-label">T4</div>
        </div>
        <div class="week-col">
          <div class="week-bar-wrap">
            <div class="week-bar" data-val="3.1h" style="height:93%;background:var(--blue-pale);"></div>
          </div>
          <div class="week-label">T5</div>
        </div>
        <div class="week-col">
          <div class="week-bar-wrap">
            <div class="week-bar" data-val="2.5h" style="height:75%;background:var(--blue-pale);"></div>
          </div>
          <div class="week-label">T6</div>
        </div>
        <div class="week-col">
          <div class="week-bar-wrap">
            <div class="week-bar" data-val="0.8h" style="height:24%;background:var(--gray-100);"></div>
          </div>
          <div class="week-label">T7</div>
        </div>
        <div class="week-col">
          <div class="week-bar-wrap">
            <div class="week-bar today" data-val="2.8h" style="height:84%;background:linear-gradient(180deg,var(--blue),#3a7fd0);"></div>
          </div>
          <div class="week-label" style="color:var(--blue);font-weight:700;">Hôm nay</div>
        </div>
      </div>
      <div style="margin-top: 14px; padding-top: 14px; border-top: 1px solid var(--gray-200); display: flex; justify-content: space-between;">
        <div style="text-align:center;">
          <div style="font-family:'Nunito',sans-serif;font-weight:900;font-size:1.3rem;color:var(--text);">13.9h</div>
          <div style="font-size:0.72rem;color:var(--gray-400);">Tổng tuần này</div>
        </div>
        <div style="text-align:center;">
          <div style="font-family:'Nunito',sans-serif;font-weight:900;font-size:1.3rem;color:#22C55E;">+2.1h</div>
          <div style="font-size:0.72rem;color:var(--gray-400);">So tuần trước</div>
        </div>
        <div style="text-align:center;">
          <div style="font-family:'Nunito',sans-serif;font-weight:900;font-size:1.3rem;color:var(--orange);">2.0h</div>
          <div style="font-size:0.72rem;color:var(--gray-400);">Mục tiêu / ngày</div>
        </div>
      </div>
    </div>

    <!-- LEARNING TYPE + AI INSIGHTS (full width row) -->
    <div class="analytics-card">
      <div class="ac-header">
        <div class="ac-title">🌟 Phong cách học tập</div>
        <span class="ac-badge purple">Phân tích AI</span>
      </div>
      <div class="type-result">
        <div class="type-badge-big">
          <div class="type-icon">🔭</div>
          <div class="type-name">Người phân tích</div>
          <div class="type-sub">Visual + Logical</div>
        </div>
        <div class="type-traits">
          <div class="trait-item"><span class="trait-check">✓</span> Học tốt qua sơ đồ tư duy và hình ảnh trực quan</div>
          <div class="trait-item"><span class="trait-check">✓</span> Cần hiểu "tại sao" trước khi ghi nhớ</div>
          <div class="trait-item"><span class="trait-check">✓</span> Làm việc tốt nhất theo chuỗi bước logic</div>
          <div class="trait-item" style="color:var(--orange);">⚠ Dễ bị phân tâm khi bài thiếu cấu trúc rõ ràng</div>
        </div>
      </div>
    </div>

    <div class="analytics-card">
      <div class="ac-header">
        <div class="ac-title">🔮 Dự báo kết quả kỳ thi</div>
        <span class="ac-badge">Dựa trên tiến độ hiện tại</span>
      </div>
      <div class="forecast-row">
        <div class="forecast-item">
          <div class="forecast-subject">Toán</div>
          <div class="forecast-score" style="color:var(--blue);">8.2</div>
          <div class="forecast-change trend-up">↑ +0.8 điểm</div>
          <div class="forecast-note">Nếu ôn cực trị</div>
        </div>
        <div class="forecast-item">
          <div class="forecast-subject">Vật lý</div>
          <div class="forecast-score" style="color:var(--orange);">6.8</div>
          <div class="forecast-change trend-down">↓ Cần tăng cường</div>
          <div class="forecast-note">Dao động & Sóng</div>
        </div>
        <div class="forecast-item">
          <div class="forecast-subject">Tiếng Anh</div>
          <div class="forecast-score" style="color:#22C55E;">9.0</div>
          <div class="forecast-change trend-up">↑ Xuất sắc</div>
          <div class="forecast-note">Duy trì luyện tập</div>
        </div>
        <div class="forecast-item">
          <div class="forecast-subject">Văn</div>
          <div class="forecast-score" style="color:#A855F7;">7.5</div>
          <div class="forecast-change trend-up">↑ +0.5 điểm</div>
          <div class="forecast-note">Luyện nghị luận</div>
        </div>
      </div>
    </div>

    <!-- AI INSIGHTS full width -->
    <div class="analytics-card span2">
      <div class="ac-header">
        <div class="ac-title">🤖 Nhận xét & Khuyến nghị từ AI</div>
        <span class="ac-badge">Cá nhân hóa cho em</span>
      </div>
      <div class="insight-list">
        <div class="insight-item">
          <div class="insight-icon warn">🚨</div>
          <div class="insight-body">
            <div class="insight-title">Lỗ hổng kiến thức quan trọng: Cực trị hàm số</div>
            <div class="insight-desc">Em mắc lỗi ở 8/10 bài tập về cực trị trong 2 tuần qua. Đây là chủ đề hay xuất hiện trong đề thi. AI gợi ý học lại từ khái niệm đạo hàm = 0 trước khi làm bài tập nâng cao.</div>
            <span class="insight-action">📌 Bắt đầu ôn ngay →</span>
          </div>
        </div>
        <div class="insight-item">
          <div class="insight-icon good">🏆</div>
          <div class="insight-body">
            <div class="insight-title">Điểm mạnh nổi bật: Tư duy phân tích vượt trội</div>
            <div class="insight-desc">Điểm phân tích của em xếp top 8% trong nhóm cùng lớp. Em đặc biệt xuất sắc ở việc nhận diện pattern và liên hệ kiến thức. Hãy tận dụng điều này khi học môn Hóa!</div>
            <span class="insight-action">✨ Xem chi tiết →</span>
          </div>
        </div>
        <div class="insight-item">
          <div class="insight-icon tip">⏰</div>
          <div class="insight-body">
            <div class="insight-title">Thời điểm học tốt nhất của em: 20:00 – 22:00</div>
            <div class="insight-desc">Dữ liệu cho thấy độ chính xác của em tăng 23% khi học buổi tối so với buổi sáng. AI gợi ý sắp xếp các chủ đề khó vào khung giờ này để tối ưu hiệu suất.</div>
            <span class="insight-action">📅 Cập nhật lịch học →</span>
          </div>
        </div>
        <div class="insight-item">
          <div class="insight-icon info">🎧</div>
          <div class="insight-body">
            <div class="insight-title">Podcast cá nhân hóa đã sẵn sàng: 3 tập mới</div>
            <div class="insight-desc">Dựa trên phân tích điểm yếu tuần này, AI đã tạo 3 tập podcast ngắn về Cực trị, Dao động điều hòa và Phép đọc hiểu văn bản. Tổng thời gian: 22 phút.</div>
            <span class="insight-action">▶ Nghe ngay →</span>
          </div>
        </div>
      </div>
    </div>

  </div>
</section>

<!-- ASSESSMENT SECTION -->
<section class="assessment-section" id="assessment">
  <div class="assessment-header">
    <span class="section-label">Công cụ mới · Miễn phí</span>
    <h2 class="section-title">Đánh Giá Năng Lực Học Tập<br>Chương Trình GDPT 2018</h2>
    <p class="section-sub">Nhập điểm 11 môn học, AI phân tích thiên hướng, gợi ý tổ hợp thi THPT và ngành nghề phù hợp ngay lập tức.</p>
  </div>

  <div class="assessment-layout">

    <!-- FORM PANEL (left) -->
    <div class="asmnt-form-panel">
      <div class="asmnt-form-header">
        <div class="fh-icon">📝</div>
        <div>
          <h3>Nhập điểm của bạn</h3>
          <p>Điểm từ 0–10 · Môn ★ bắt buộc phải nhập</p>
        </div>
      </div>
      <div class="asmnt-form-body">

        <!-- Môn bắt buộc -->
        <div class="asmnt-group-label req">
          <span style="width:8px;height:8px;border-radius:50%;background:var(--blue);flex-shrink:0;display:inline-block;"></span>
          Môn bắt buộc <span class="asmnt-tag r">Phải nhập</span>
        </div>
        <div class="asmnt-subjects-grid">
          <!-- Toán -->
          <div class="asmnt-item" id="aw-toan">
            <div class="asmnt-subject-name">Toán học <span class="asmnt-req-star">★</span></div>
            <div class="asmnt-score-wrap">
              <input class="asmnt-score-input" type="number" id="as-toan" min="0" max="10" step="0.1" placeholder="Điểm…" data-required="true" oninput="asmntInput(this)" onblur="asmntValidate(this)">
            </div>
            <span class="asmnt-suffix">/ 10</span>
            <div class="asmnt-err-msg">Nhập điểm 0–10</div>
            <div class="asmnt-indicator" id="ai-toan"></div>
          </div>
          <!-- Ngữ văn -->
          <div class="asmnt-item" id="aw-van">
            <div class="asmnt-subject-name">Ngữ văn <span class="asmnt-req-star">★</span></div>
            <div class="asmnt-score-wrap">
              <input class="asmnt-score-input" type="number" id="as-van" min="0" max="10" step="0.1" placeholder="Điểm…" data-required="true" oninput="asmntInput(this)" onblur="asmntValidate(this)">
            </div>
            <span class="asmnt-suffix">/ 10</span>
            <div class="asmnt-err-msg">Nhập điểm 0–10</div>
            <div class="asmnt-indicator" id="ai-van"></div>
          </div>
          <!-- Tiếng Anh -->
          <div class="asmnt-item" id="aw-anh">
            <div class="asmnt-subject-name">Tiếng Anh <span class="asmnt-req-star">★</span></div>
            <div class="asmnt-score-wrap">
              <input class="asmnt-score-input" type="number" id="as-anh" min="0" max="10" step="0.1" placeholder="Điểm…" data-required="true" oninput="asmntInput(this)" onblur="asmntValidate(this)">
            </div>
            <span class="asmnt-suffix">/ 10</span>
            <div class="asmnt-err-msg">Nhập điểm 0–10</div>
            <div class="asmnt-indicator" id="ai-anh"></div>
          </div>
          <!-- Lịch sử -->
          <div class="asmnt-item" id="aw-su">
            <div class="asmnt-subject-name">Lịch sử <span class="asmnt-req-star">★</span></div>
            <div class="asmnt-score-wrap">
              <input class="asmnt-score-input" type="number" id="as-su" min="0" max="10" step="0.1" placeholder="Điểm…" data-required="true" oninput="asmntInput(this)" onblur="asmntValidate(this)">
            </div>
            <span class="asmnt-suffix">/ 10</span>
            <div class="asmnt-err-msg">Nhập điểm 0–10</div>
            <div class="asmnt-indicator" id="ai-su"></div>
          </div>
        </div>

        <div class="asmnt-divider"></div>

        <!-- Môn tự chọn -->
        <div class="asmnt-group-label opt">
          <span style="width:8px;height:8px;border-radius:50%;background:var(--gray-400);flex-shrink:0;display:inline-block;"></span>
          Môn tự chọn <span class="asmnt-tag o">Có thể bỏ trống</span>
        </div>
        <div class="asmnt-subjects-grid">
          <div class="asmnt-item" id="aw-dia">
            <div class="asmnt-subject-name">Địa lí</div>
            <div class="asmnt-score-wrap"><input class="asmnt-score-input" type="number" id="as-dia" min="0" max="10" step="0.1" placeholder="Bỏ trống được" data-required="false" oninput="asmntInput(this)"></div>
            <span class="asmnt-suffix">/ 10</span>
            <div class="asmnt-indicator" id="ai-dia"></div>
          </div>
          <div class="asmnt-item" id="aw-ly">
            <div class="asmnt-subject-name">Vật lý</div>
            <div class="asmnt-score-wrap"><input class="asmnt-score-input" type="number" id="as-ly" min="0" max="10" step="0.1" placeholder="Bỏ trống được" data-required="false" oninput="asmntInput(this)"></div>
            <span class="asmnt-suffix">/ 10</span>
            <div class="asmnt-indicator" id="ai-ly"></div>
          </div>
          <div class="asmnt-item" id="aw-hoa">
            <div class="asmnt-subject-name">Hóa học</div>
            <div class="asmnt-score-wrap"><input class="asmnt-score-input" type="number" id="as-hoa" min="0" max="10" step="0.1" placeholder="Bỏ trống được" data-required="false" oninput="asmntInput(this)"></div>
            <span class="asmnt-suffix">/ 10</span>
            <div class="asmnt-indicator" id="ai-hoa"></div>
          </div>
          <div class="asmnt-item" id="aw-sinh">
            <div class="asmnt-subject-name">Sinh học</div>
            <div class="asmnt-score-wrap"><input class="asmnt-score-input" type="number" id="as-sinh" min="0" max="10" step="0.1" placeholder="Bỏ trống được" data-required="false" oninput="asmntInput(this)"></div>
            <span class="asmnt-suffix">/ 10</span>
            <div class="asmnt-indicator" id="ai-sinh"></div>
          </div>
          <div class="asmnt-item" id="aw-tin">
            <div class="asmnt-subject-name">Tin học</div>
            <div class="asmnt-score-wrap"><input class="asmnt-score-input" type="number" id="as-tin" min="0" max="10" step="0.1" placeholder="Bỏ trống được" data-required="false" oninput="asmntInput(this)"></div>
            <span class="asmnt-suffix">/ 10</span>
            <div class="asmnt-indicator" id="ai-tin"></div>
          </div>
          <div class="asmnt-item" id="aw-cn">
            <div class="asmnt-subject-name">Công nghệ</div>
            <div class="asmnt-score-wrap"><input class="asmnt-score-input" type="number" id="as-cn" min="0" max="10" step="0.1" placeholder="Bỏ trống được" data-required="false" oninput="asmntInput(this)"></div>
            <span class="asmnt-suffix">/ 10</span>
            <div class="asmnt-indicator" id="ai-cn"></div>
          </div>
          <div class="asmnt-item" id="aw-gdqp">
            <div class="asmnt-subject-name">Giáo dục QP</div>
            <div class="asmnt-score-wrap"><input class="asmnt-score-input" type="number" id="as-gdqp" min="0" max="10" step="0.1" placeholder="Bỏ trống được" data-required="false" oninput="asmntInput(this)"></div>
            <span class="asmnt-suffix">/ 10</span>
            <div class="asmnt-indicator" id="ai-gdqp"></div>
          </div>
          <!-- 3 môn bổ sung GDPT 2018 -->
          <div class="asmnt-item" id="aw-khtn">
            <div class="asmnt-subject-name" style="display:flex;align-items:center;gap:4px;">
              KHTN
              <span style="font-size:0.62rem;background:#ECFDF5;color:#059669;padding:1px 5px;border-radius:4px;font-weight:700;">Tích hợp</span>
            </div>
            <div class="asmnt-score-wrap"><input class="asmnt-score-input" type="number" id="as-khtn" min="0" max="10" step="0.1" placeholder="Bỏ trống được" data-required="false" oninput="asmntInput(this)"></div>
            <span class="asmnt-suffix">/ 10</span>
            <div class="asmnt-indicator" id="ai-khtn"></div>
          </div>
          <div class="asmnt-item" id="aw-lsdia">
            <div class="asmnt-subject-name" style="display:flex;align-items:center;gap:4px;">
              Lịch sử &amp; Địa lí
              <span style="font-size:0.62rem;background:#FFF3E8;color:var(--orange);padding:1px 5px;border-radius:4px;font-weight:700;">Tích hợp</span>
            </div>
            <div class="asmnt-score-wrap"><input class="asmnt-score-input" type="number" id="as-lsdia" min="0" max="10" step="0.1" placeholder="Bỏ trống được" data-required="false" oninput="asmntInput(this)"></div>
            <span class="asmnt-suffix">/ 10</span>
            <div class="asmnt-indicator" id="ai-lsdia"></div>
          </div>
          <div class="asmnt-item" id="aw-gdcd">
            <div class="asmnt-subject-name">Giáo dục CD</div>
            <div class="asmnt-score-wrap"><input class="asmnt-score-input" type="number" id="as-gdcd" min="0" max="10" step="0.1" placeholder="Bỏ trống được" data-required="false" oninput="asmntInput(this)"></div>
            <span class="asmnt-suffix">/ 10</span>
            <div class="asmnt-indicator" id="ai-gdcd"></div>
          </div>
          <div class="asmnt-item" id="aw-gdktpl">
            <div class="asmnt-subject-name" style="display:flex;align-items:center;gap:4px;flex-wrap:wrap;">
              GD Kinh tế &amp; PL
              <span style="font-size:0.62rem;background:#F5F3FF;color:#7C3AED;padding:1px 5px;border-radius:4px;font-weight:700;">THPT</span>
            </div>
            <div class="asmnt-score-wrap"><input class="asmnt-score-input" type="number" id="as-gdktpl" min="0" max="10" step="0.1" placeholder="Bỏ trống được" data-required="false" oninput="asmntInput(this)"></div>
            <span class="asmnt-suffix">/ 10</span>
            <div class="asmnt-indicator" id="ai-gdktpl"></div>
          </div>
        </div>
      </div>

      <div class="asmnt-submit-bar">
        <button class="asmnt-btn-calc" onclick="asmntCalculate()">
          🧮 Tính kết quả & Phân tích
        </button>
        <button class="asmnt-btn-reset" onclick="asmntReset()">🔄 Nhập lại</button>
      </div>
    </div>

    <!-- RESULTS PANEL (right) -->
    <div class="asmnt-results-panel" id="asmnt-results">
      <!-- Empty state shown by default -->
      <div class="asmnt-empty-state" id="asmnt-empty">
        <div class="empty-icon">🎯</div>
        <h4>Kết quả hiển thị ở đây</h4>
        <p>Nhập điểm các môn học bên trái và nhấn<br><strong>Tính kết quả & Phân tích</strong> để xem ngay.</p>
      </div>
    </div>

  </div>
</section>

<!-- ASSESSMENT JAVASCRIPT -->
<script>
/* =============================================
   AI STUDY BUDDY – Assessment Tool JS
   GDPT 2018 · Tích hợp vào trang chủ
   ============================================= */

const ASMNT_SUBJECTS = [
  {id:'toan', name:'Toán',         required:true },
  {id:'van',  name:'Ngữ văn',      required:true },
  {id:'anh',  name:'Tiếng Anh',    required:true },
  {id:'su',   name:'Lịch sử',      required:true },
  {id:'dia',  name:'Địa lí',       required:false},
  {id:'ly',   name:'Vật lý',       required:false},
  {id:'hoa',  name:'Hóa học',      required:false},
  {id:'sinh', name:'Sinh học',     required:false},
  {id:'tin',  name:'Tin học',      required:false},
  {id:'cn',   name:'Công nghệ',    required:false},
  {id:'gdqp', name:'GD Quốc phòng',  required:false},
  {id:'khtn', name:'KHTN (Tích hợp)',required:false},
  {id:'lsdia',name:'Lịch sử & Địa lí',required:false},
  {id:'gdcd',   name:'Giáo dục CD',          required:false},
  {id:'gdktpl', name:'GD Kinh tế & Pháp luật',required:false},
];

const ASMNT_COMBOS = {
  A00:{code:'A00',subs:['toan','ly','hoa'],    name:'Toán – Lý – Hóa'},
  A01:{code:'A01',subs:['toan','ly','anh'],    name:'Toán – Lý – Anh'},
  B00:{code:'B00',subs:['toan','hoa','sinh'],  name:'Toán – Hóa – Sinh'},
  B08:{code:'B08',subs:['toan','sinh','anh'],  name:'Toán – Sinh – Anh'},
  C00:{code:'C00',subs:['van','su','dia'],     name:'Văn – Sử – Địa'},
  C01:{code:'C01',subs:['van','toan','ly'],    name:'Văn – Toán – Lý'},
  D01:{code:'D01',subs:['van','toan','anh'],   name:'Văn – Toán – Anh'},
  D14:{code:'D14',subs:['van','su','anh'],     name:'Văn – Sử – Anh'},
  D15:{code:'D15',subs:['van','dia','anh'],    name:'Văn – Địa – Anh'},
  I00:{code:'I00',subs:['toan','ly','tin'],    name:'Toán – Lý – Tin'},
  // Tổ hợp dùng môn tích hợp GDPT 2018
  KH1:{code:'KH1',subs:['toan','khtn','anh'],  name:'Toán – KHTN – Anh'},
  KH2:{code:'KH2',subs:['van','lsdia','anh'],  name:'Văn – LS&ĐL – Anh'},
  KH3:{code:'KH3',subs:['toan','khtn','lsdia'],name:'Toán – KHTN – LS&ĐL'},
  CD1:{code:'CD1', subs:['van','gdcd','anh'],    name:'Văn – GDCD – Anh'},
  CD2:{code:'CD2', subs:['toan','gdcd','anh'],   name:'Toán – GDCD – Anh'},
  KT1:{code:'KT1', subs:['van','gdktpl','anh'],  name:'Văn – KT&PL – Anh'},
  KT2:{code:'KT2', subs:['toan','gdktpl','anh'], name:'Toán – KT&PL – Anh'},
  KT3:{code:'KT3', subs:['van','gdktpl','su'],   name:'Văn – KT&PL – Sử'},
};

/* Trả về rank object theo điểm */
function asmntRank(s) {
  if (s >= 8.0) return {text:'Giỏi',       cls:'gioi',pillCls:'a-pill-gioi'};
  if (s >= 6.5) return {text:'Khá',        cls:'kha', pillCls:'a-pill-kha' };
  if (s >= 5.0) return {text:'Trung bình', cls:'tb',  pillCls:'a-pill-tb'  };
  return               {text:'Yếu',        cls:'yeu', pillCls:'a-pill-yeu' };
}

/* Màu gradient bar theo điểm */
function asmntBarColor(s) {
  if (s>=8) return 'linear-gradient(90deg,#22C55E,#4ADE80)';
  if (s>=6.5) return 'linear-gradient(90deg,#4A90E2,#7BB3EE)';
  if (s>=5) return 'linear-gradient(90deg,#FFA94D,#FFB36B)';
  return 'linear-gradient(90deg,#EF4444,#F87171)';
}

/* Tính TB của nhóm môn (bỏ qua null) */
function asmntGroupAvg(sc, keys) {
  const v = keys.map(k=>sc[k]).filter(x=>x!==null);
  return v.length ? v.reduce((a,b)=>a+b,0)/v.length : null;
}

/* Realtime feedback khi gõ */
function asmntInput(el) {
  const id   = el.id.replace('as-','');
  const wrap = document.getElementById('aw-'+id);
  const ind  = document.getElementById('ai-'+id);
  let val = parseFloat(el.value);
  if (el.value!=='' && (isNaN(val)||val<0)) el.value=0;
  if (val>10) el.value=10;
  val = parseFloat(el.value);
  if (el.value!=='' && !isNaN(val)) {
    const r = asmntRank(val);
    wrap.classList.add('asmnt-has-value');
    wrap.classList.remove('asmnt-error');
    ind.className = 'asmnt-indicator aind-'+r.cls;
    ind.textContent = r.text[0];
  } else {
    wrap.classList.remove('asmnt-has-value');
    ind.className = 'asmnt-indicator';
    ind.textContent = '';
  }
}

/* Validate khi blur môn bắt buộc */
function asmntValidate(el) {
  if (el.dataset.required!=='true') return true;
  const id   = el.id.replace('as-','');
  const wrap = document.getElementById('aw-'+id);
  if (el.value===''||isNaN(parseFloat(el.value))) {
    wrap.classList.add('asmnt-error'); return false;
  }
  wrap.classList.remove('asmnt-error'); return true;
}

/* Main calculate */
function asmntCalculate() {
  // Validate bắt buộc
  let valid = true;
  ASMNT_SUBJECTS.forEach(s=>{
    if (s.required) { const el=document.getElementById('as-'+s.id); if (!asmntValidate(el)) valid=false; }
  });
  if (!valid) {
    const firstErr = document.querySelector('.asmnt-item.asmnt-error');
    if (firstErr) firstErr.scrollIntoView({behavior:'smooth',block:'center'});
    return;
  }

  // Thu thập điểm
  const sc = {};
  ASMNT_SUBJECTS.forEach(s=>{
    const v = document.getElementById('as-'+s.id).value;
    sc[s.id] = (v!==''&&!isNaN(parseFloat(v))) ? parseFloat(v) : null;
  });

  // Tính điểm TB
  const entered = ASMNT_SUBJECTS.filter(s=>sc[s.id]!==null);
  const avg = entered.reduce((sum,s)=>sum+sc[s.id],0)/entered.length;
  const avgR = Math.round(avg*100)/100;
  const rank = asmntRank(avgR);

  // Xây dựng kết quả
  const panel = document.getElementById('asmnt-results');
  panel.innerHTML = '';

  // 1. Banner kết quả
  const subMsg = {gioi:'Xuất sắc! Giữ vững và hướng tới tổ hợp điểm cao.',kha:'Tốt lắm! Ôn kỹ môn yếu để lên mức Giỏi.',tb:'Đạt chuẩn. Cần đầu tư thêm vào môn yếu.',yeu:'Đừng nản! Bắt đầu từ kiến thức cơ bản nhất.'};
  panel.innerHTML += `
    <div class="asmnt-banner ${rank.cls}">
      <div class="asmnt-score-circle">
        <div class="asmnt-score-num">${avgR.toFixed(2)}</div>
        <div class="asmnt-score-lbl">Điểm TB</div>
      </div>
      <div class="asmnt-banner-info">
        <div class="asmnt-banner-rank">Học lực: ${rank.text}</div>
        <div class="asmnt-banner-sub">${subMsg[rank.cls]}</div>
        <div class="asmnt-banner-count">📚 Đã nhập ${entered.length}/${ASMNT_SUBJECTS.length} môn</div>
      </div>
    </div>
  `;

  // 2. Bảng điểm
  let rows = '';
  ASMNT_SUBJECTS.forEach(s=>{
    if (sc[s.id]===null) return;
    const r = asmntRank(sc[s.id]);
    const col = sc[s.id]>=8?'#059669':sc[s.id]>=6.5?'#1D4ED8':sc[s.id]>=5?'#D97706':'#DC2626';
    rows += `<tr>
      <td style="font-weight:600;">${s.name}${s.required?'<span style="color:var(--blue);font-size:0.65rem;margin-left:3px;">★</span>':''}</td>
      <td class="atd-score" style="color:${col}">${sc[s.id].toFixed(1)}</td>
      <td class="atd-rank"><span class="a-pill ${r.pillCls}">${r.text}</span></td>
    </tr>`;
  });
  panel.innerHTML += `
    <div class="asmnt-result-card">
      <div class="arc-head"><div class="arc-icon blue">📊</div><div><div class="arc-title">Bảng điểm chi tiết</div><div class="arc-sub">Điểm từng môn & xếp loại</div></div></div>
      <div class="arc-body">
        <table class="arc-table">
          <thead><tr><th>Môn học</th><th style="text-align:center;">Điểm</th><th style="text-align:right;">Xếp loại</th></tr></thead>
          <tbody>${rows}</tbody>
        </table>
      </div>
    </div>
  `;

  // 3. Điểm mạnh / yếu
  const sorted = [...entered].map(s=>({...s,score:sc[s.id]})).sort((a,b)=>b.score-a.score);
  const top3   = sorted.slice(0,3);
  const bot3   = [...sorted].reverse().slice(0,3);
  const swBar = (item) => `
    <div class="asmnt-sw-item">
      <div class="asmnt-sw-row"><span class="asmnt-sw-name">${item.name}</span><span class="asmnt-sw-val">${item.score.toFixed(1)}</span></div>
      <div class="asmnt-sw-bar"><div class="asmnt-sw-fill" style="width:${item.score*10}%;background:${asmntBarColor(item.score)};"></div></div>
    </div>`;
  panel.innerHTML += `
    <div class="asmnt-result-card">
      <div class="arc-head"><div class="arc-icon green">💪</div><div><div class="arc-title">Điểm mạnh & Cần cải thiện</div><div class="arc-sub">So sánh các môn</div></div></div>
      <div class="arc-body">
        <div style="font-size:0.72rem;font-weight:700;color:#059669;text-transform:uppercase;letter-spacing:0.8px;margin-bottom:10px;">⬆ Môn nổi bật</div>
        ${top3.map(swBar).join('')}
        <div style="height:1px;background:var(--gray-200);margin:14px 0;"></div>
        <div style="font-size:0.72rem;font-weight:700;color:#DC2626;text-transform:uppercase;letter-spacing:0.8px;margin-bottom:10px;">⬇ Cần tập trung ôn</div>
        ${bot3.map(swBar).join('')}
      </div>
    </div>
  `;

  // 4. Phân tích thiên hướng
  const groups = [
    {icon:'🔬',title:'Khoa học Tự nhiên',    keys:['toan','ly','hoa','khtn'],   desc:'Tư duy logic, phân tích. Phù hợp kỹ thuật & nghiên cứu.', thr:7.0},
    {icon:'📚',title:'Khoa học Xã hội',      keys:['van','su','dia','lsdia'],   desc:'Năng lực ngôn ngữ & tư duy xã hội. Phù hợp luật, sư phạm.', thr:7.0},
    {icon:'💻',title:'Công nghệ Thông tin',  keys:['tin','toan'],               desc:'Tin học nổi bật. Tiềm năng lớn trong lập trình & AI.', thr:7.5},
    {icon:'🧬',title:'Y – Sinh học',         keys:['sinh','hoa','toan','khtn'], desc:'Sinh–Hóa–KHTN cao. Phù hợp y dược & sinh học ứng dụng.', thr:7.0},
    {icon:'🌍',title:'Ngôn ngữ & Quốc tế',  keys:['anh','van'],                desc:'Ngoại ngữ vượt trội. Phù hợp ngoại giao, phiên dịch.', thr:7.5},
    {icon:'⚙️',title:'Kỹ thuật & Công nghệ',keys:['toan','ly','cn','khtn'],    desc:'Tư duy kỹ thuật. Phù hợp cơ khí, điện tử, xây dựng.', thr:6.5},
    {icon:'🏛️',title:'Khoa học Chính trị – Pháp luật',keys:['van','gdcd','gdktpl','su'],desc:'GDCD & KT-PL nổi bật. Phù hợp luật, chính sách, hành chính công.', thr:7.0},
    {icon:'💰',title:'Kinh tế – Tài chính',keys:['gdktpl','toan'],desc:'Điểm KT&PL + Toán tốt. Phù hợp kinh tế học, tài chính, ngân hàng, quản trị.', thr:7.0},
    {icon:'🗺️',title:'Địa lý – Du lịch',    keys:['dia','lsdia','anh'],        desc:'Địa lí & LS&ĐL tốt. Phù hợp địa lý học, du lịch, quy hoạch.', thr:6.5},
  ];
  let tendItems = '';
  groups.forEach(g=>{
    const avg = asmntGroupAvg(sc, g.keys);
    if (avg===null) return;
    const str = avg>=g.thr+1.0 ? 'strong' : avg>=g.thr ? 'medium' : 'weak';
    tendItems += `
      <div class="asmnt-tend-item ${str}">
        <div class="asmnt-tend-icon">${g.icon}</div>
        <div class="asmnt-tend-body">
          <div class="asmnt-tend-title">${g.title}</div>
          <div class="asmnt-tend-desc">${g.desc}</div>
        </div>
        <div class="asmnt-tend-score">TB: ${avg.toFixed(1)}</div>
      </div>`;
  });
  if (!tendItems) tendItems = '<p style="color:var(--gray-400);font-size:0.85rem;">Nhập thêm môn tự chọn để xem phân tích đầy đủ.</p>';
  panel.innerHTML += `
    <div class="asmnt-result-card">
      <div class="arc-head"><div class="arc-icon orange">🧭</div><div><div class="arc-title">Phân tích thiên hướng</div><div class="arc-sub">Dựa trên nhóm điểm môn học</div></div></div>
      <div class="arc-body"><div class="asmnt-tendency-list">${tendItems}</div></div>
    </div>
  `;

  // 5. Tổ hợp thi + Ngành nghề
  const rankedCombos = Object.values(ASMNT_COMBOS).map(c=>{
    const v = c.subs.map(id=>sc[id]).filter(x=>x!==null);
    if (v.length<c.subs.length) return null;
    return {...c, avg: v.reduce((a,b)=>a+b,0)/v.length};
  }).filter(Boolean).sort((a,b)=>b.avg-a.avg).slice(0,6);

  let comboHTML = rankedCombos.length ? rankedCombos.map(c=>`
    <div class="asmnt-combo-chip">
      <div class="asmnt-combo-code">${c.code} <span style="font-size:0.7rem;color:var(--gray-400);">(${c.avg.toFixed(1)})</span></div>
      <div class="asmnt-combo-name">${c.name}</div>
      <span class="a-pill ${asmntRank(c.avg).pillCls}" style="margin-top:5px;display:inline-flex;">${asmntRank(c.avg).text}</span>
    </div>`).join('')
    : '<p style="color:var(--gray-400);font-size:0.82rem;">Nhập thêm môn tự chọn để xem gợi ý tổ hợp.</p>';

  // Ngành nghề
  const careers = [];
  const tlh    = asmntGroupAvg(sc,['toan','ly','hoa','khtn']);
  const vsd    = asmntGroupAvg(sc,['van','su','dia','lsdia']);
  const tnT    = asmntGroupAvg(sc,['tin','toan']);
  const shh    = asmntGroupAvg(sc,['sinh','hoa','khtn']);
  const gdcdS   = sc['gdcd'];
  const lsdiaS  = sc['lsdia'];
  const khtnS   = sc['khtn'];
  const gdktplS = sc['gdktpl'];
  if (tlh!==null&&tlh>=7)   careers.push(...['🔭 Kỹ sư','⚗️ Hóa học','⚡ Điện–Điện tử','🏗️ Xây dựng','🧪 Khoa học ứng dụng']);
  if (vsd!==null&&vsd>=7)   careers.push(...['📰 Báo chí','🎓 Sư phạm','🌏 Địa lý học','🏛️ Quản lý nhà nước']);
  if (tnT!==null&&tnT>=7)   careers.push(...['💻 Lập trình viên','🤖 AI/ML','📊 Data Science']);
  if (shh!==null&&shh>=7)   careers.push(...['🏥 Y khoa','💊 Dược học','🧬 Công nghệ Sinh học']);
  if (sc['anh']!==null&&sc['anh']>=7.5) careers.push(...['🌐 Ngôn ngữ Anh','✈️ Du lịch–Lữ hành','📖 Phiên dịch']);
  if (sc['toan']!==null&&sc['toan']>=8) careers.push(...['📈 Tài chính','🧮 Toán ứng dụng']);
  if (gdcdS!==null&&gdcdS>=7)     careers.push(...['⚖️ Luật học','🤝 Quan hệ QT','🏛️ Chính sách công','👮 Hành chính-Pháp lý']);
  if (lsdiaS!==null&&lsdiaS>=7)  careers.push(...['🗺️ Địa lý học','🏺 Lịch sử','🌿 Quy hoạch lãnh thổ']);
  if (khtnS!==null&&khtnS>=7.5)  careers.push(...['🔬 Nghiên cứu khoa học','🌡️ Khí tượng học','🏔️ Địa chất']);
  if (gdktplS!==null&&gdktplS>=7) careers.push(...['💼 Kinh tế học','🏦 Ngân hàng–Tài chính','📊 Kế toán–Kiểm toán','⚖️ Luật Kinh tế','🏢 Quản trị Kinh doanh']);
  const uniqCareers = [...new Set(careers)].slice(0,16);
  const careerHTML = uniqCareers.length
    ? uniqCareers.map(c=>{const p=c.split(' ');return `<div class="asmnt-career-tag">${p[0]} ${p.slice(1).join(' ')}</div>`;}).join('')
    : '<p style="color:var(--gray-400);font-size:0.82rem;">Nhập thêm điểm để xem gợi ý ngành nghề.</p>';

  panel.innerHTML += `
    <div class="asmnt-result-card">
      <div class="arc-head"><div class="arc-icon purple">🎯</div><div><div class="arc-title">Tổ hợp thi THPT phù hợp</div><div class="arc-sub">Sắp xếp theo điểm cao nhất</div></div></div>
      <div class="arc-body"><div class="asmnt-combo-wrap">${comboHTML}</div></div>
    </div>
    <div class="asmnt-result-card">
      <div class="arc-head"><div class="arc-icon yellow">🚀</div><div><div class="arc-title">Ngành nghề tham khảo</div><div class="arc-sub">Phù hợp với năng lực của bạn</div></div></div>
      <div class="arc-body"><div class="asmnt-career-wrap">${careerHTML}</div></div>
    </div>
  `;

  // 6. Lời khuyên cá nhân hóa
  const advices = [];
  const genMap = {gioi:'Kết quả xuất sắc! Đặt mục tiêu điểm THPT tối đa và thử sức các kỳ thi HSG.',kha:'Kết quả khá tốt! Tập trung ôn môn dưới 7.0 để đẩy TB lên mức Giỏi.',tb:'Hãy lập lịch học đều đặn mỗi ngày và ưu tiên ôn lại kiến thức nền môn yếu.',yeu:'Đừng bỏ cuộc! Nhờ AI Study Buddy giải thích từng bước để xây dựng lại nền tảng.'};
  advices.push(genMap[rank.cls]);
  const worst = [...entered].sort((a,b)=>sc[a.id]-sc[b.id])[0];
  if (worst&&sc[worst.id]<6.5) advices.push(`<strong>${worst.name} (${sc[worst.id].toFixed(1)})</strong> là môn cần ưu tiên ôn ngay. Dùng AI Study Buddy tạo lộ trình riêng cho môn này.`);
  if (tlh!==null&&tlh>=8) advices.push('Nhóm <strong>Toán–Lý–Hóa–KHTN</strong> rất nổi bật. Luyện thử đề THPT theo tổ hợp A00/A01/KH1 để định hướng mục tiêu.');
  if (vsd!==null&&vsd>=8) advices.push('Nhóm <strong>Văn–Sử–Địa–LS&ĐL</strong> tốt. Luyện viết nghị luận xã hội mỗi tuần để tăng điểm Văn đáng kể.');
  if (sc['anh']!==null&&sc['anh']>=8) advices.push('<strong>Tiếng Anh</strong> vượt trội – cân nhắc luyện IELTS/TOEIC để mở rộng cơ hội học bổng quốc tế.');
  if (tnT!==null&&tnT>=7.5) advices.push('<strong>Tin học</strong> tốt! Thử học Python hoặc web để có lợi thế khi vào đại học CNTT.');
  if (gdcdS!==null&&gdcdS>=7.5)     advices.push('<strong>Giáo dục Công dân</strong> tốt – hãy tìm hiểu thêm về ngành Luật, Quản trị Nhà nước để định hướng sớm.');
  if (gdktplS!==null&&gdktplS>=7.5) advices.push('<strong>GD Kinh tế & Pháp luật</strong> nổi bật – phù hợp với các tổ hợp KT1/KT2, hướng tới ngành Kinh tế, Luật Kinh tế, Tài chính–Ngân hàng.');
  if (lsdiaS!==null&&lsdiaS>=7.5) advices.push('<strong>Lịch sử & Địa lí</strong> (tích hợp) nổi bật – phù hợp để đăng ký tổ hợp LS&ĐL-Anh cho kỳ thi THPT mới.');
  if (khtnS!==null&&khtnS>=7.5) advices.push('<strong>KHTN</strong> (tích hợp) khá cao – đây là môn thay thế Lý-Hóa-Sinh ở THCS, hãy đảm bảo nền tảng vững trước khi chọn phân môn THPT.');
  advices.push('Sử dụng <strong>Knowledge Gap Map</strong> trên AI Study Buddy để theo dõi lỗ hổng kiến thức mỗi tuần.');

  const adviceHTML = advices.slice(0,6).map((t,i)=>`
    <div class="asmnt-advice-item">
      <div class="asmnt-advice-num">${i+1}</div>
      <div class="asmnt-advice-text">${t}</div>
    </div>`).join('');

  panel.innerHTML += `
    <div class="asmnt-result-card">
      <div class="arc-head"><div class="arc-icon blue">💡</div><div><div class="arc-title">Lời khuyên cá nhân hóa</div><div class="arc-sub">AI Study Buddy gợi ý riêng cho bạn</div></div></div>
      <div class="arc-body"><div class="asmnt-advice-list">${adviceHTML}</div></div>
    </div>
  `;
}

/* Reset form */
function asmntReset() {
  ASMNT_SUBJECTS.forEach(s=>{
    const el   = document.getElementById('as-'+s.id);
    const wrap = document.getElementById('aw-'+s.id);
    const ind  = document.getElementById('ai-'+s.id);
    el.value = '';
    wrap.classList.remove('asmnt-has-value','asmnt-error');
    if (ind) { ind.className='asmnt-indicator'; ind.textContent=''; }
  });
  const panel = document.getElementById('asmnt-results');
  panel.innerHTML = `
    <div class="asmnt-empty-state" id="asmnt-empty">
      <div class="empty-icon">🎯</div>
      <h4>Kết quả hiển thị ở đây</h4>
      <p>Nhập điểm các môn học bên trái và nhấn<br><strong>Tính kết quả & Phân tích</strong> để xem ngay.</p>
    </div>`;
}
</script>

<!-- CTA -->
<section class="cta-section">
  <h2>Bắt đầu hành trình<br>học thông minh ngay hôm nay</h2>
  <p>Miễn phí 30 ngày · Không cần thẻ tín dụng · Cho học sinh THCS – THPT</p>
  <button class="btn-white">🚀 Đăng ký miễn phí</button>
</section>

<!-- FOOTER -->
<footer>
  <div class="footer-grid">
    <div>
      <div class="footer-logo">
        <span class="footer-logo-icon">🤖</span>
        AI Study Buddy
      </div>
      <p class="footer-desc">Trợ lý học tập AI cá nhân hóa<br>dành riêng cho học sinh Việt Nam.<br>Học thông minh hơn, không phải chăm hơn.</p>
    </div>
    <div class="footer-col">
      <h5>Sản phẩm</h5>
      <ul>
        <li><a href="#">Tính năng</a></li>
        <li><a href="#">Lộ trình học</a></li>
        <li><a href="#">Podcast AI</a></li>
        <li><a href="#assessment">Đánh giá năng lực</a></li>
        <li><a href="#">Dashboard</a></li>
      </ul>
    </div>
    <div class="footer-col">
      <h5>Hỗ trợ</h5>
      <ul>
        <li><a href="#">Trung tâm trợ giúp</a></li>
        <li><a href="#">Liên hệ</a></li>
        <li><a href="#">Blog giáo dục</a></li>
      </ul>
    </div>
    <div class="footer-col">
      <h5>👥 Người sáng tạo</h5>
      <ul>
        <li style="margin-bottom:12px;">
          <div style="color:white;font-weight:700;font-size:0.88rem;">Nguyễn Mỹ Hà Vy</div>
          <div style="color:rgba(255,255,255,0.4);font-size:0.75rem;margin-top:2px;">Product Design & UX</div>
        </li>
        <li style="margin-bottom:12px;">
          <div style="color:white;font-weight:700;font-size:0.88rem;">Nguyễn Xuân Vũ</div>
          <div style="color:rgba(255,255,255,0.4);font-size:0.75rem;margin-top:2px;">AI Engineering & Backend</div>
        </li>
        <li>
          <div style="color:white;font-weight:700;font-size:0.88rem;">Võ Phạm Minh Tài</div>
          <div style="color:rgba(255,255,255,0.4);font-size:0.75rem;margin-top:2px;">Frontend & Data Science</div>
        </li>
      </ul>
    </div>
  </div>

  <!-- API INTEGRATIONS BAR -->
  <div style="border-top:1px solid rgba(255,255,255,0.08);padding:22px 0 20px;margin-bottom:0;">
    <div style="font-size:0.72rem;font-weight:700;color:rgba(255,255,255,0.35);text-transform:uppercase;letter-spacing:1.5px;text-align:center;margin-bottom:16px;">
      Được xây dựng với sự tích hợp của các API mạnh mẽ
    </div>
    <div style="display:flex;flex-wrap:wrap;justify-content:center;align-items:center;gap:10px;">
      <span style="display:inline-flex;align-items:center;gap:6px;background:rgba(255,255,255,0.07);border:1px solid rgba(255,255,255,0.12);padding:6px 14px;border-radius:100px;font-size:0.78rem;font-weight:600;color:rgba(255,255,255,0.7);">🤖 Claude AI (Anthropic)</span>
      <span style="display:inline-flex;align-items:center;gap:6px;background:rgba(255,255,255,0.07);border:1px solid rgba(255,255,255,0.12);padding:6px 14px;border-radius:100px;font-size:0.78rem;font-weight:600;color:rgba(255,255,255,0.7);">🧠 OpenAI GPT-4o</span>
      <span style="display:inline-flex;align-items:center;gap:6px;background:rgba(255,255,255,0.07);border:1px solid rgba(255,255,255,0.12);padding:6px 14px;border-radius:100px;font-size:0.78rem;font-weight:600;color:rgba(255,255,255,0.7);">🎙️ ElevenLabs TTS</span>
      <span style="display:inline-flex;align-items:center;gap:6px;background:rgba(255,255,255,0.07);border:1px solid rgba(255,255,255,0.12);padding:6px 14px;border-radius:100px;font-size:0.78rem;font-weight:600;color:rgba(255,255,255,0.7);">🔍 Google Gemini</span>
      <span style="display:inline-flex;align-items:center;gap:6px;background:rgba(255,255,255,0.07);border:1px solid rgba(255,255,255,0.12);padding:6px 14px;border-radius:100px;font-size:0.78rem;font-weight:600;color:rgba(255,255,255,0.7);">📚 notebookLM</span>
      <span style="display:inline-flex;align-items:center;gap:6px;background:rgba(255,255,255,0.07);border:1px solid rgba(255,255,255,0.12);padding:6px 14px;border-radius:100px;font-size:0.78rem;font-weight:600;color:rgba(255,255,255,0.7);">🗣️ Google Sites STT</span>
      <span style="display:inline-flex;align-items:center;gap:6px;background:rgba(255,255,255,0.07);border:1px solid rgba(255,255,255,0.12);padding:6px 14px;border-radius:100px;font-size:0.78rem;font-weight:600;color:rgba(255,255,255,0.7);">📊 Chatbot Interface</span>
    </div>
  </div>

  <div class="footer-bottom">
    <p>© 2025 AI Study Buddy · Được làm với ❤️ bởi <strong style="color:rgba(255,255,255,0.7);">Nguyễn Mỹ Hà Vy · Nguyễn Xuân Vũ · Võ Phạm Minh Tài</strong></p>
    <p style="color:rgba(255,255,255,0.3);">Việt Nam 🇻🇳</p>
  </div>
</footer>

</body>
</html>
