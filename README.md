<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Asathiya Transports — Premium Freight Solutions</title>
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Rajdhani:wght@300;400;500;600;700&family=Barlow+Condensed:ital,wght@0,200;0,300;0,600;0,700;1,200&display=swap" rel="stylesheet"/>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/gsap.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/ScrollTrigger.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/TextPlugin.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
<style>
:root{
  --red:#e63328;--deep-red:#a01f1b;--orange:#f57c2b;
  --black:#080808;--charcoal:#111;--steel:#1c1c1c;--border:#242424;
  --white:#f2ede4;--muted:#666;--gold:#c9930a;
}
*,*::before,*::after{margin:0;padding:0;box-sizing:border-box}
html{scroll-behavior:smooth;overflow-x:hidden}
body{background:var(--black);color:var(--white);font-family:'Rajdhani',sans-serif;cursor:none;overflow-x:hidden}

/* ═══ CUSTOM CURSOR ═══ */
#cursor{position:fixed;width:12px;height:12px;background:var(--red);border-radius:50%;pointer-events:none;z-index:99999;transform:translate(-50%,-50%);transition:transform 0.1s,background 0.2s,width 0.3s,height 0.3s;mix-blend-mode:difference}
#cursor-ring{position:fixed;width:40px;height:40px;border:1px solid rgba(230,51,40,0.5);border-radius:50%;pointer-events:none;z-index:99998;transform:translate(-50%,-50%);transition:all 0.12s ease;mix-blend-mode:difference}
body:hover #cursor{transform:translate(-50%,-50%) scale(1)}
a:hover ~ #cursor, button:hover ~ #cursor{width:24px;height:24px}

/* ═══ LOADER ═══ */
#loader{position:fixed;inset:0;background:var(--black);z-index:99997;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:2rem}
.loader-logo{font-family:'Bebas Neue',sans-serif;font-size:clamp(2rem,6vw,5rem);letter-spacing:8px;color:var(--white);opacity:0}
.loader-bar-wrap{width:300px;height:2px;background:#1a1a1a;overflow:hidden}
.loader-bar{height:100%;background:linear-gradient(90deg,var(--red),var(--orange));width:0%;transition:width 0.05s}
.loader-pct{font-family:'Barlow Condensed',sans-serif;font-size:0.75rem;letter-spacing:4px;color:var(--muted)}

/* ═══ CANVAS BG ═══ */
#three-canvas{position:fixed;top:0;left:0;width:100%;height:100%;z-index:0;pointer-events:none;opacity:0.35}

/* ═══ NAV ═══ */
nav{position:fixed;top:0;left:0;right:0;z-index:1000;display:flex;align-items:center;justify-content:space-between;padding:1.4rem 4rem;background:rgba(8,8,8,0);backdrop-filter:blur(0px);border-bottom:1px solid rgba(255,255,255,0);transition:all 0.5s ease}
nav.scrolled{background:rgba(8,8,8,0.95);backdrop-filter:blur(16px);border-bottom:1px solid rgba(230,51,40,0.2)}
.nav-logo{font-family:'Bebas Neue',sans-serif;font-size:1.4rem;letter-spacing:4px;color:var(--red);display:flex;align-items:center;gap:0.6rem}
.nav-logo svg{width:28px;height:28px}
.nav-links{display:flex;gap:3rem;list-style:none}
.nav-links a{text-decoration:none;color:rgba(242,237,228,0.7);font-size:0.72rem;font-weight:700;letter-spacing:3px;text-transform:uppercase;transition:color 0.2s;position:relative}
.nav-links a::after{content:'';position:absolute;bottom:-4px;left:0;width:0;height:1px;background:var(--red);transition:width 0.3s ease}
.nav-links a:hover{color:var(--white)}
.nav-links a:hover::after{width:100%}
.nav-cta{padding:0.6rem 1.4rem;background:var(--red);color:var(--white);font-size:0.7rem;font-weight:700;letter-spacing:2px;text-transform:uppercase;text-decoration:none;transition:all 0.25s;clip-path:polygon(8px 0%,100% 0%,calc(100% - 8px) 100%,0% 100%)}
.nav-cta:hover{background:var(--deep-red);transform:translateY(-2px)}

/* ═══ HERO ═══ */
.hero{position:relative;height:100vh;display:flex;align-items:center;overflow:hidden;z-index:1}
.hero-bg-img{position:absolute;inset:0;background:url('https://images.unsplash.com/photo-1601584115197-04ecc0da31d7?w=1920&q=80') center/cover no-repeat;transform:scale(1.1);transition:transform 8s ease}
.hero-bg-img.loaded{transform:scale(1)}
.hero-overlay{position:absolute;inset:0;background:linear-gradient(105deg,rgba(8,8,8,0.96) 0%,rgba(8,8,8,0.75) 50%,rgba(8,8,8,0.3) 100%)}
.hero-grid{position:absolute;inset:0;background-image:linear-gradient(rgba(230,51,40,0.04) 1px,transparent 1px),linear-gradient(90deg,rgba(230,51,40,0.04) 1px,transparent 1px);background-size:80px 80px;animation:gridDrift 20s linear infinite}
@keyframes gridDrift{to{background-position:80px 80px}}
.hero-content{position:relative;z-index:2;padding:0 4rem;max-width:900px}
.hero-badge{display:inline-flex;align-items:center;gap:0.6rem;font-size:0.65rem;font-weight:700;letter-spacing:4px;text-transform:uppercase;color:var(--red);border:1px solid rgba(230,51,40,0.4);padding:0.4rem 1rem;margin-bottom:2rem;background:rgba(230,51,40,0.06);backdrop-filter:blur(4px)}
.badge-dot{width:6px;height:6px;background:var(--red);border-radius:50%;animation:pulse 1.5s infinite}
@keyframes pulse{0%,100%{opacity:1;transform:scale(1)}50%{opacity:0.4;transform:scale(0.6)}}
.hero-title{font-family:'Bebas Neue',sans-serif;font-size:clamp(4.5rem,11vw,10rem);line-height:0.85;letter-spacing:3px;overflow:hidden}
.hero-title .line{display:block;clip-path:inset(0 0 0 0)}
.hero-title .red{color:var(--red)}
.hero-title .stroke{-webkit-text-stroke:1px var(--white);color:transparent}
.hero-subtitle{margin-top:1.8rem;font-size:1.1rem;font-weight:300;color:rgba(242,237,228,0.55);letter-spacing:1px;line-height:1.7;max-width:480px}
.hero-actions{margin-top:2.5rem;display:flex;gap:1.2rem;flex-wrap:wrap}
.btn{display:inline-flex;align-items:center;gap:0.6rem;padding:0.9rem 2rem;font-family:'Rajdhani',sans-serif;font-size:0.78rem;font-weight:700;letter-spacing:2.5px;text-transform:uppercase;text-decoration:none;cursor:pointer;border:none;transition:all 0.3s;position:relative;overflow:hidden}
.btn::before{content:'';position:absolute;inset:0;background:rgba(255,255,255,0.08);transform:translateX(-100%);transition:transform 0.4s ease}
.btn:hover::before{transform:translateX(0)}
.btn-fire{background:linear-gradient(135deg,var(--red),var(--orange));color:white;clip-path:polygon(12px 0,100% 0,calc(100% - 12px) 100%,0 100%)}
.btn-fire:hover{transform:translateY(-3px);box-shadow:0 12px 32px rgba(230,51,40,0.45)}
.btn-ghost{background:transparent;color:var(--white);border:1px solid rgba(255,255,255,0.2);clip-path:polygon(12px 0,100% 0,calc(100% - 12px) 100%,0 100%)}
.btn-ghost:hover{border-color:var(--red);color:var(--red)}
.hero-scroll{position:absolute;bottom:2.5rem;left:50%;transform:translateX(-50%);display:flex;flex-direction:column;align-items:center;gap:0.6rem;z-index:2}
.scroll-label{font-size:0.6rem;letter-spacing:4px;text-transform:uppercase;color:var(--muted)}
.scroll-line{width:1px;height:50px;background:linear-gradient(to bottom,var(--red),transparent);animation:scrollPulse 1.8s ease-in-out infinite}
@keyframes scrollPulse{0%{transform:scaleY(0);transform-origin:top}50%{transform:scaleY(1);transform-origin:top}51%{transform:scaleY(1);transform-origin:bottom}100%{transform:scaleY(0);transform-origin:bottom}}
/* hero image slideshow */
.hero-slides{position:absolute;inset:0;z-index:0}
.hero-slide{position:absolute;inset:0;background-size:cover;background-position:center;opacity:0;transition:opacity 1.5s ease}
.hero-slide.active{opacity:1}

/* ═══ MARQUEE ═══ */
.marquee-wrap{position:relative;z-index:2;background:var(--red);padding:0.75rem 0;overflow:hidden;border-top:1px solid rgba(255,255,255,0.1);border-bottom:1px solid rgba(255,255,255,0.1)}
.marquee-track{display:flex;gap:3rem;white-space:nowrap;animation:marquee 18s linear infinite}
.marquee-item{font-family:'Bebas Neue',sans-serif;font-size:1.1rem;letter-spacing:4px;color:rgba(255,255,255,0.9);display:flex;align-items:center;gap:3rem}
.marquee-item::after{content:'◆';color:rgba(255,255,255,0.5);font-size:0.5rem}
@keyframes marquee{to{transform:translateX(-50%)}}

/* ═══ STATS ═══ */
.stats-section{position:relative;z-index:2;padding:5rem 4rem;background:var(--charcoal)}
.stats-inner{display:grid;grid-template-columns:repeat(4,1fr);gap:2px;background:rgba(230,51,40,0.15)}
.stat-card{background:var(--charcoal);padding:3rem 2rem;text-align:center;position:relative;overflow:hidden;transition:background 0.3s}
.stat-card::before{content:'';position:absolute;bottom:0;left:0;right:0;height:0;background:linear-gradient(to top,rgba(230,51,40,0.12),transparent);transition:height 0.4s}
.stat-card:hover{background:#161616}
.stat-card:hover::before{height:100%}
.stat-num{font-family:'Bebas Neue',sans-serif;font-size:4rem;letter-spacing:2px;line-height:1;background:linear-gradient(135deg,var(--red),var(--orange));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text}
.stat-label{font-size:0.68rem;font-weight:700;letter-spacing:3px;text-transform:uppercase;color:var(--muted);margin-top:0.5rem}
.stat-divider{width:30px;height:2px;background:var(--red);margin:0.8rem auto 0;opacity:0.5}

/* ═══ ABOUT ═══ */
.about-section{position:relative;z-index:2;min-height:90vh;display:grid;grid-template-columns:1fr 1fr;overflow:hidden}
.about-visual{position:relative;overflow:hidden}
.about-img{width:100%;height:100%;min-height:600px;object-fit:cover;filter:grayscale(30%) contrast(1.1);transition:filter 0.5s,transform 8s ease}
.about-img:hover{filter:grayscale(0) contrast(1.2);transform:scale(1.03)}
.about-img-overlay{position:absolute;inset:0;background:linear-gradient(to right,transparent 60%,var(--black));pointer-events:none}
.about-tag{position:absolute;top:2rem;left:2rem;background:var(--red);padding:0.5rem 1rem;font-size:0.65rem;font-weight:700;letter-spacing:3px;text-transform:uppercase;z-index:2}
.about-content{background:var(--black);padding:5rem;display:flex;flex-direction:column;justify-content:center}
.eyebrow{font-size:0.65rem;font-weight:700;letter-spacing:5px;text-transform:uppercase;color:var(--red);margin-bottom:1rem;display:flex;align-items:center;gap:0.8rem}
.eyebrow::before{content:'';display:inline-block;width:24px;height:1px;background:var(--red)}
.section-h{font-family:'Bebas Neue',sans-serif;font-size:clamp(2.8rem,5vw,4.5rem);letter-spacing:2px;line-height:0.95;margin-bottom:1.5rem}
.section-h span{color:var(--red)}
.about-body{font-size:1rem;font-weight:300;color:var(--muted);line-height:1.9;margin-bottom:2rem}
.info-cards{display:grid;grid-template-columns:1fr 1fr;gap:1px;background:rgba(255,255,255,0.05);margin-top:2rem}
.info-card{background:var(--charcoal);padding:1.5rem;transition:background 0.3s}
.info-card:hover{background:#181818}
.info-card-label{font-size:0.6rem;font-weight:700;letter-spacing:3px;text-transform:uppercase;color:var(--red);margin-bottom:0.4rem}
.info-card-val{font-size:0.88rem;line-height:1.5;color:var(--white)}

/* ═══ SERVICES ═══ */
.services-section{position:relative;z-index:2;padding:7rem 4rem;background:var(--black);overflow:hidden}
.services-bg{position:absolute;inset:0;background:url('https://images.unsplash.com/photo-1586528116311-ad8dd3c8310d?w=1920&q=60') center/cover no-repeat fixed;opacity:0.04}
.services-header{display:flex;justify-content:space-between;align-items:flex-end;margin-bottom:4rem;flex-wrap:wrap;gap:2rem}
.services-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:1.5px;background:rgba(230,51,40,0.12)}
.svc-card{background:var(--charcoal);padding:0;overflow:hidden;position:relative;group:true;transition:transform 0.4s}
.svc-card:hover{transform:translateY(-4px)}
.svc-img-wrap{width:100%;height:220px;overflow:hidden;position:relative}
.svc-img{width:100%;height:100%;object-fit:cover;filter:grayscale(60%);transition:transform 0.6s ease,filter 0.5s}
.svc-card:hover .svc-img{transform:scale(1.07);filter:grayscale(10%)}
.svc-img-overlay{position:absolute;inset:0;background:linear-gradient(to top,var(--charcoal) 0%,rgba(17,17,17,0.3) 60%,transparent 100%)}
.svc-body{padding:2rem}
.svc-num{font-family:'Bebas Neue',sans-serif;font-size:3.5rem;color:rgba(230,51,40,0.12);line-height:1;margin-bottom:0.5rem}
.svc-name{font-family:'Bebas Neue',sans-serif;font-size:1.8rem;letter-spacing:2px;margin-bottom:0.6rem;transition:color 0.3s}
.svc-card:hover .svc-name{color:var(--red)}
.svc-desc{font-size:0.88rem;color:var(--muted);line-height:1.7;font-weight:300}
.svc-arrow{display:inline-flex;align-items:center;gap:0.5rem;margin-top:1.2rem;font-size:0.7rem;font-weight:700;letter-spacing:2px;text-transform:uppercase;color:var(--red);opacity:0;transform:translateX(-10px);transition:all 0.3s}
.svc-card:hover .svc-arrow{opacity:1;transform:translateX(0)}

/* ═══ PARALLAX BANNER ═══ */
.parallax-banner{position:relative;z-index:2;height:60vh;overflow:hidden;display:flex;align-items:center;justify-content:center}
.parallax-img{position:absolute;inset:-20%;background:url('https://images.unsplash.com/photo-1519003722824-194d4455a60c?w=1920&q=80') center/cover no-repeat;filter:brightness(0.3) contrast(1.2) saturate(0.6)}
.parallax-content{position:relative;z-index:2;text-align:center}
.parallax-content h2{font-family:'Bebas Neue',sans-serif;font-size:clamp(3rem,8vw,7rem);letter-spacing:6px;line-height:1}
.parallax-content h2 span{color:var(--red)}
.parallax-content p{font-size:1rem;color:rgba(242,237,228,0.5);letter-spacing:2px;margin-top:1rem;font-weight:300}

/* ═══ WHY US ═══ */
.why-section{position:relative;z-index:2;padding:7rem 4rem;background:var(--charcoal);display:grid;grid-template-columns:1fr 1fr;gap:6rem;align-items:center}
.why-visual{position:relative}
.why-img{width:100%;height:500px;object-fit:cover;filter:contrast(1.1) saturate(0.8)}
.why-img-accent{position:absolute;bottom:-1.5rem;right:-1.5rem;width:60%;height:200px;border:2px solid var(--red);z-index:-1}
.why-counter{position:absolute;top:2rem;right:-3rem;background:var(--red);padding:1.5rem 2rem;text-align:center}
.why-counter-num{font-family:'Bebas Neue',sans-serif;font-size:3rem;line-height:1}
.why-counter-label{font-size:0.6rem;letter-spacing:2px;text-transform:uppercase;opacity:0.8}
.why-list{margin-top:2.5rem;display:flex;flex-direction:column;gap:0}
.why-item{display:grid;grid-template-columns:48px 1fr;gap:1.2rem;align-items:start;padding:1.5rem 0;border-bottom:1px solid var(--border);cursor:pointer;transition:all 0.3s}
.why-item:hover .why-icon{background:var(--red);color:white}
.why-icon{width:48px;height:48px;display:flex;align-items:center;justify-content:center;font-size:1.2rem;border:1px solid var(--border);transition:all 0.3s;flex-shrink:0}
.why-title{font-family:'Bebas Neue',sans-serif;font-size:1.2rem;letter-spacing:2px;margin-bottom:0.25rem}
.why-desc{font-size:0.85rem;color:var(--muted);line-height:1.6;font-weight:300}

/* ═══ FLEET ═══ */
.fleet-section{position:relative;z-index:2;padding:7rem 4rem;background:var(--black)}
.fleet-header{margin-bottom:3rem}
.fleet-slider{position:relative;overflow:hidden}
.fleet-track{display:flex;gap:2px;transition:transform 0.6s cubic-bezier(0.25,0.46,0.45,0.94)}
.fleet-card{flex:0 0 calc(33.333% - 2px);background:var(--charcoal);overflow:hidden;position:relative}
.fleet-img{width:100%;height:280px;object-fit:cover;filter:grayscale(40%);transition:filter 0.5s,transform 0.5s}
.fleet-card:hover .fleet-img{filter:grayscale(0%);transform:scale(1.04)}
.fleet-info{padding:1.5rem}
.fleet-type{font-family:'Bebas Neue',sans-serif;font-size:1.4rem;letter-spacing:2px}
.fleet-cap{font-size:0.78rem;color:var(--muted);letter-spacing:1px;font-weight:300}
.fleet-controls{display:flex;gap:0.8rem;margin-top:2rem}
.fleet-btn{width:48px;height:48px;border:1px solid var(--border);background:transparent;color:var(--white);font-size:1.1rem;cursor:pointer;display:flex;align-items:center;justify-content:center;transition:all 0.2s}
.fleet-btn:hover{background:var(--red);border-color:var(--red)}

/* ═══ CONTACT ═══ */
.contact-section{position:relative;z-index:2;min-height:100vh;display:grid;grid-template-columns:1fr 1fr;overflow:hidden}
.contact-visual{position:relative;overflow:hidden}
.contact-bg{width:100%;height:100%;object-fit:cover;filter:grayscale(50%) brightness(0.4);position:absolute;inset:0}
.contact-visual-content{position:relative;z-index:2;padding:5rem;display:flex;flex-direction:column;justify-content:flex-end;height:100%}
.contact-visual-content h2{font-family:'Bebas Neue',sans-serif;font-size:clamp(2.5rem,4vw,4rem);letter-spacing:3px;margin-bottom:2rem}
.contact-details{display:flex;flex-direction:column;gap:1.5rem}
.contact-row{display:flex;align-items:flex-start;gap:1rem}
.c-icon{width:40px;height:40px;background:rgba(230,51,40,0.2);border:1px solid rgba(230,51,40,0.4);display:flex;align-items:center;justify-content:center;font-size:1rem;flex-shrink:0}
.c-label{font-size:0.58rem;font-weight:700;letter-spacing:3px;text-transform:uppercase;color:var(--red);margin-bottom:0.2rem}
.c-val{font-size:0.9rem;line-height:1.6}
.c-val a{color:var(--white);text-decoration:none;transition:color 0.2s}
.c-val a:hover{color:var(--red)}
.contact-form-side{background:var(--charcoal);padding:5rem;display:flex;flex-direction:column;justify-content:center}
.form-title{font-family:'Bebas Neue',sans-serif;font-size:2rem;letter-spacing:3px;margin-bottom:2rem}
.form-title span{color:var(--red)}
.field{display:flex;flex-direction:column;gap:0.4rem;margin-bottom:1.2rem}
.field label{font-size:0.6rem;font-weight:700;letter-spacing:3px;text-transform:uppercase;color:rgba(242,237,228,0.4)}
.field input,.field textarea,.field select{background:rgba(255,255,255,0.04);border:none;border-bottom:1px solid var(--border);color:var(--white);padding:0.75rem 0;font-family:'Rajdhani',sans-serif;font-size:0.95rem;outline:none;transition:border-color 0.3s;resize:none;appearance:none;-webkit-appearance:none}
.field input:focus,.field textarea:focus,.field select:focus{border-bottom-color:var(--red)}
.field select option{background:var(--charcoal)}
.field textarea{height:100px;padding:0.75rem 0}
.form-row-2{display:grid;grid-template-columns:1fr 1fr;gap:1.5rem}
.submit-btn{margin-top:0.5rem;padding:1rem 2.5rem;background:linear-gradient(135deg,var(--red) 0%,var(--orange) 100%);color:white;border:none;font-family:'Rajdhani',sans-serif;font-size:0.78rem;font-weight:700;letter-spacing:3px;text-transform:uppercase;cursor:pointer;transition:all 0.3s;position:relative;overflow:hidden;clip-path:polygon(14px 0,100% 0,calc(100% - 14px) 100%,0 100%)}
.submit-btn::before{content:'';position:absolute;inset:0;background:rgba(255,255,255,0.12);transform:translateX(-100%);transition:transform 0.4s ease}
.submit-btn:hover::before{transform:translateX(0)}
.submit-btn:hover{transform:translateY(-2px);box-shadow:0 12px 32px rgba(230,51,40,0.4)}

/* ═══ GST STRIP ═══ */
.gst-strip{position:relative;z-index:2;background:var(--steel);padding:1.2rem 4rem;display:flex;gap:4rem;flex-wrap:wrap;align-items:center;border-top:1px solid rgba(230,51,40,0.15)}
.gst-item{display:flex;flex-direction:column;gap:0.15rem}
.gst-key{font-size:0.55rem;font-weight:700;letter-spacing:3px;text-transform:uppercase;color:var(--muted)}
.gst-val{font-size:0.82rem;font-weight:600;letter-spacing:1px;color:var(--white)}

/* ═══ FOOTER ═══ */
footer{position:relative;z-index:2;background:var(--black);padding:3rem 4rem 2rem;border-top:1px solid rgba(255,255,255,0.04)}
.footer-top{display:flex;justify-content:space-between;align-items:flex-start;flex-wrap:wrap;gap:2rem;padding-bottom:2rem;border-bottom:1px solid var(--border)}
.footer-brand{max-width:300px}
.footer-name{font-family:'Bebas Neue',sans-serif;font-size:1.8rem;letter-spacing:4px;color:var(--red);margin-bottom:0.6rem}
.footer-tagline{font-size:0.82rem;color:var(--muted);line-height:1.7;font-weight:300}
.footer-links h4{font-size:0.62rem;font-weight:700;letter-spacing:3px;text-transform:uppercase;color:var(--red);margin-bottom:1rem}
.footer-links ul{list-style:none;display:flex;flex-direction:column;gap:0.5rem}
.footer-links a{text-decoration:none;color:var(--muted);font-size:0.88rem;transition:color 0.2s}
.footer-links a:hover{color:var(--white)}
.footer-bottom{display:flex;justify-content:space-between;align-items:center;padding-top:1.5rem;flex-wrap:wrap;gap:1rem}
.footer-copy{font-size:0.7rem;color:var(--muted);letter-spacing:1px}

/* ═══ TOAST ═══ */
#toast{position:fixed;bottom:2.5rem;right:2.5rem;background:linear-gradient(135deg,var(--red),var(--orange));color:white;padding:1rem 2rem;font-size:0.8rem;font-weight:700;letter-spacing:1.5px;z-index:9999;transform:translateY(80px);opacity:0;transition:all 0.5s cubic-bezier(0.34,1.56,0.64,1);pointer-events:none;clip-path:polygon(12px 0,100% 0,calc(100% - 12px) 100%,0 100%)}
#toast.show{transform:translateY(0);opacity:1}

/* ═══ SCROLL REVEAL ═══ */
.reveal{opacity:0;transform:translateY(40px)}

/* ═══ FLOATING PARTICLES CANVAS ═══ */
#particles{position:fixed;inset:0;pointer-events:none;z-index:1}

/* ═══ RESPONSIVE ═══ */
@media(max-width:900px){
  nav{padding:1rem 1.5rem}
  .nav-links{display:none}
  .hero-content{padding:0 1.5rem}
  .about-section{grid-template-columns:1fr}
  .services-section{padding:4rem 1.5rem}
  .services-grid{grid-template-columns:1fr}
  .why-section{grid-template-columns:1fr;padding:4rem 1.5rem;gap:3rem}
  .why-counter{right:0}
  .fleet-section{padding:4rem 1.5rem}
  .fleet-card{flex:0 0 80%}
  .contact-section{grid-template-columns:1fr}
  .contact-visual{min-height:400px}
  .contact-form-side{padding:3rem 1.5rem}
  .contact-visual-content{padding:3rem 1.5rem}
  .stats-inner{grid-template-columns:1fr 1fr}
  .gst-strip{padding:1rem 1.5rem}
  footer{padding:2rem 1.5rem}
}
</style>
</head>
<body>

<!-- CURSOR -->
<div id="cursor"></div>
<div id="cursor-ring"></div>

<!-- PARTICLES -->
<canvas id="particles"></canvas>

<!-- THREE.JS CANVAS -->
<canvas id="three-canvas"></canvas>

<!-- LOADER -->
<div id="loader">
  <div class="loader-logo">ASATHIYA TRANSPORTS</div>
  <div class="loader-bar-wrap"><div class="loader-bar" id="loaderBar"></div></div>
  <div class="loader-pct" id="loaderPct">0%</div>
</div>

<!-- NAV -->
<nav id="mainNav">
  <div class="nav-logo">
    <svg viewBox="0 0 28 28" fill="none" xmlns="http://www.w3.org/2000/svg">
      <rect x="2" y="10" width="18" height="12" rx="1" fill="currentColor" opacity="0.9"/>
      <rect x="20" y="6" width="6" height="16" rx="1" fill="currentColor"/>
      <circle cx="7" cy="23" r="3" fill="var(--charcoal)" stroke="currentColor" stroke-width="1.5"/>
      <circle cx="21" cy="23" r="3" fill="var(--charcoal)" stroke="currentColor" stroke-width="1.5"/>
    </svg>
    ASATHIYA
  </div>
  <ul class="nav-links">
    <li><a href="#about">About</a></li>
    <li><a href="#services">Services</a></li>
    <li><a href="#fleet">Fleet</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
  <a href="#contact" class="nav-cta">Get Quote →</a>
</nav>

<!-- HERO -->
<section class="hero" id="hero">
  <div class="hero-slides">
    <div class="hero-slide active" style="background-image:url('https://images.unsplash.com/photo-1601584115197-04ecc0da31d7?w=1920&q=80')"></div>
    <div class="hero-slide" style="background-image:url('https://images.unsplash.com/photo-1508780709619-79562169bc64?w=1920&q=80')"></div>
    <div class="hero-slide" style="background-image:url('https://images.unsplash.com/photo-1532300964467-9be00eb5f671?w=1920&q=80')"></div>
  </div>
  <div class="hero-overlay"></div>
  <div class="hero-grid"></div>
  <div class="hero-content">
    <div class="hero-badge" id="heroBadge"><span class="badge-dot"></span> Tamil Nadu's Trusted Freight Partner</div>
    <h1 class="hero-title">
      <span class="line" id="hline1">ASATHIYA</span>
      <span class="line stroke" id="hline2">TRANS</span>
      <span class="line red" id="hline3">PORTS</span>
    </h1>
    <p class="hero-subtitle" id="heroSub">Premium road freight solutions from Tirunelveli District — delivering cargo across India with precision, speed, and trust.</p>
    <div class="hero-actions" id="heroActions">
      <a href="#contact" class="btn btn-fire">🚛 Get Instant Quote</a>
      <a href="#services" class="btn btn-ghost">Explore Services</a>
    </div>
  </div>
  <div class="hero-scroll">
    <span class="scroll-label">Scroll</span>
    <div class="scroll-line"></div>
  </div>
</section>

<!-- MARQUEE -->
<div class="marquee-wrap">
  <div class="marquee-track" id="marqueeTrack">
    <div class="marquee-item">Full Truck Load</div><div class="marquee-item">Part Load LTL</div>
    <div class="marquee-item">Pan-India Freight</div><div class="marquee-item">Express Delivery</div>
    <div class="marquee-item">Tirunelveli District</div><div class="marquee-item">Tamil Nadu 627 110</div>
    <div class="marquee-item">GST Registered</div><div class="marquee-item">24/7 Support</div>
    <div class="marquee-item">Full Truck Load</div><div class="marquee-item">Part Load LTL</div>
    <div class="marquee-item">Pan-India Freight</div><div class="marquee-item">Express Delivery</div>
    <div class="marquee-item">Tirunelveli District</div><div class="marquee-item">Tamil Nadu 627 110</div>
    <div class="marquee-item">GST Registered</div><div class="marquee-item">24/7 Support</div>
  </div>
</div>

<!-- STATS -->
<div class="stats-section" id="statsSection">
  <div class="stats-inner">
    <div class="stat-card"><div class="stat-num" data-target="10" data-suffix="+">0</div><div class="stat-label">Years of Service</div><div class="stat-divider"></div></div>
    <div class="stat-card"><div class="stat-num" data-target="500" data-suffix="+">0</div><div class="stat-label">Loads Delivered</div><div class="stat-divider"></div></div>
    <div class="stat-card"><div class="stat-num" data-target="24" data-suffix="/7">0</div><div class="stat-label">Customer Support</div><div class="stat-divider"></div></div>
    <div class="stat-card"><div class="stat-num" data-target="15" data-suffix="+ States">0</div><div class="stat-label">Coverage Area</div><div class="stat-divider"></div></div>
  </div>
</div>

<!-- ABOUT -->
<section class="about-section" id="about">
  <div class="about-visual">
    <img class="about-img" src="https://images.unsplash.com/photo-1558618666-fcd25c85cd64?w=900&q=80" alt="Truck on highway" loading="lazy"/>
    <div class="about-img-overlay"></div>
    <div class="about-tag">Est. Nanguneri Taluk</div>
  </div>
  <div class="about-content">
    <div class="eyebrow reveal">Who We Are</div>
    <h2 class="section-h reveal">MOVING<br>INDIA'S<br><span>CARGO</span></h2>
    <p class="about-body reveal">Asathiya Transports is a GST-registered freight carrier headquartered in Anna Nagar, Elankulam Post, Nanguneri Taluk, Tirunelveli District. We connect businesses across Tamil Nadu and beyond with dependable, professional road logistics built on years of trust.</p>
    <div class="info-cards reveal">
      <div class="info-card"><div class="info-card-label">Registered Address</div><div class="info-card-val">No. 184–1/3, Main Road, Anna Nagar, Elankulam Post, Nanguneri Taluk, Tirunelveli Dist. TN – 627 110</div></div>
      <div class="info-card"><div class="info-card-label">PAN Number</div><div class="info-card-val">AWWPV7253P</div><br><div class="info-card-label">GST IN</div><div class="info-card-val">33AWWPV7253P22A</div></div>
    </div>
  </div>
</section>

<!-- SERVICES -->
<section class="services-section" id="services">
  <div class="services-bg"></div>
  <div class="services-header">
    <div>
      <div class="eyebrow reveal">What We Do</div>
      <h2 class="section-h reveal">OUR <span>SERVICES</span></h2>
    </div>
    <p class="reveal" style="max-width:340px;color:var(--muted);font-size:0.9rem;line-height:1.7;font-weight:300">Comprehensive freight solutions tailored for businesses of all sizes across India.</p>
  </div>
  <div class="services-grid">
    <div class="svc-card reveal">
      <div class="svc-img-wrap"><img class="svc-img" src="https://images.unsplash.com/photo-1559060017-445fb9722f2a?w=800&q=80" alt="Full Truck Load" loading="lazy"/><div class="svc-img-overlay"></div></div>
      <div class="svc-body"><div class="svc-num">01</div><div class="svc-name">Full Truck Load</div><p class="svc-desc">End-to-end FTL transport for large consignments. Dedicated vehicle allocation with direct point-to-point delivery and real-time tracking.</p><div class="svc-arrow">Learn More →</div></div>
    </div>
    <div class="svc-card reveal">
      <div class="svc-img-wrap"><img class="svc-img" src="https://images.unsplash.com/photo-1586528116493-da5a9f8f7de5?w=800&q=80" alt="Part Load" loading="lazy"/><div class="svc-img-overlay"></div></div>
      <div class="svc-body"><div class="svc-num">02</div><div class="svc-name">Part Load / LTL</div><p class="svc-desc">Cost-effective movement for smaller shipments consolidated across routes. Ideal for SMEs needing flexible, economical freight solutions.</p><div class="svc-arrow">Learn More →</div></div>
    </div>
    <div class="svc-card reveal">
      <div class="svc-img-wrap"><img class="svc-img" src="https://images.unsplash.com/photo-1519003722824-194d4455a60c?w=800&q=80" alt="Pan-India Freight" loading="lazy"/><div class="svc-img-overlay"></div></div>
      <div class="svc-body"><div class="svc-num">03</div><div class="svc-name">Pan-India Freight</div><p class="svc-desc">Interstate logistics covering Tamil Nadu and connecting major hubs across all Indian states with reliable scheduling.</p><div class="svc-arrow">Learn More →</div></div>
    </div>
    <div class="svc-card reveal">
      <div class="svc-img-wrap"><img class="svc-img" src="https://images.unsplash.com/photo-1510797215324-95aa89f43c33?w=800&q=80" alt="Express Delivery" loading="lazy"/><div class="svc-img-overlay"></div></div>
      <div class="svc-body"><div class="svc-num">04</div><div class="svc-name">Express Delivery</div><p class="svc-desc">Time-critical shipments handled with priority routing. 24/7 support and dedicated dispatch for urgent cargo requirements.</p><div class="svc-arrow">Learn More →</div></div>
    </div>
  </div>
</section>

<!-- PARALLAX BANNER -->
<div class="parallax-banner">
  <div class="parallax-img" id="parallaxImg"></div>
  <div class="parallax-content">
    <h2 class="reveal">ON TIME.<br><span>EVERY TIME.</span></h2>
    <p class="reveal">Tirunelveli · Tamil Nadu · India</p>
  </div>
</div>

<!-- WHY US -->
<section class="why-section" id="why">
  <div class="why-visual reveal">
    <img class="why-img" src="https://images.unsplash.com/photo-1545127398-14699f92334b?w=900&q=80" alt="Logistics warehouse" loading="lazy"/>
    <div class="why-img-accent"></div>
    <div class="why-counter">
      <div class="why-counter-num">100%</div>
      <div class="why-counter-label">Delivery Success</div>
    </div>
  </div>
  <div>
    <div class="eyebrow reveal">Why Choose Us</div>
    <h2 class="section-h reveal">THE ASATHIYA<br><span>ADVANTAGE</span></h2>
    <div class="why-list">
      <div class="why-item reveal"><div class="why-icon">🛡️</div><div><div class="why-title">Fully GST Registered</div><p class="why-desc">Compliant with all Indian tax regulations. GST IN: 33AWWPV7253P22A — enabling seamless B2B invoicing.</p></div></div>
      <div class="why-item reveal"><div class="why-icon">📍</div><div><div class="why-title">Local Expertise</div><p class="why-desc">Deep knowledge of South Tamil Nadu routes, especially Tirunelveli, Tuticorin, and surrounding districts.</p></div></div>
      <div class="why-item reveal"><div class="why-icon">⚡</div><div><div class="why-title">Fast Dispatch</div><p class="why-desc">Same-day booking confirmation with trucks dispatched within hours of order placement.</p></div></div>
      <div class="why-item reveal"><div class="why-icon">📞</div><div><div class="why-title">24/7 Reachability</div><p class="why-desc">Two direct lines always open. Dedicated support staff for tracking updates and urgent changes.</p></div></div>
    </div>
  </div>
</section>

<!-- FLEET -->
<section class="fleet-section" id="fleet">
  <div class="fleet-header">
    <div class="eyebrow reveal">Our Fleet</div>
    <h2 class="section-h reveal">BUILT TO <span>DELIVER</span></h2>
  </div>
  <div class="fleet-slider">
    <div class="fleet-track" id="fleetTrack">
      <div class="fleet-card"><img class="fleet-img" src="https://images.unsplash.com/photo-1601584115197-04ecc0da31d7?w=700&q=80" alt="Heavy Truck" loading="lazy"/><div class="fleet-info"><div class="fleet-type">Heavy Trucks</div><div class="fleet-cap">20–40 Ton Capacity · FTL Specialist</div></div></div>
      <div class="fleet-card"><img class="fleet-img" src="https://images.unsplash.com/photo-1563207153-f403bf289096?w=700&q=80" alt="Medium Truck" loading="lazy"/><div class="fleet-info"><div class="fleet-type">Medium Carriers</div><div class="fleet-cap">8–15 Ton Capacity · Versatile Freight</div></div></div>
      <div class="fleet-card"><img class="fleet-img" src="https://images.unsplash.com/photo-1558618666-fcd25c85cd64?w=700&q=80" alt="Light Commercial" loading="lazy"/><div class="fleet-info"><div class="fleet-type">Light Commercial</div><div class="fleet-cap">1–5 Ton · Express & Part Load</div></div></div>
      <div class="fleet-card"><img class="fleet-img" src="https://images.unsplash.com/photo-1486262715619-67b85e0b08d3?w=700&q=80" alt="Refrigerated" loading="lazy"/><div class="fleet-info"><div class="fleet-type">Refrigerated Units</div><div class="fleet-cap">Temperature Controlled · Perishables</div></div></div>
    </div>
  </div>
  <div class="fleet-controls">
    <button class="fleet-btn" id="prevBtn">←</button>
    <button class="fleet-btn" id="nextBtn">→</button>
  </div>
</section>

<!-- CONTACT -->
<section class="contact-section" id="contact">
  <div class="contact-visual">
    <img class="contact-bg" src="https://images.unsplash.com/photo-1586528116311-ad8dd3c8310d?w=900&q=80" alt="Transport background" loading="lazy"/>
    <div class="contact-visual-content">
      <h2>LET'S<br>MOVE YOUR<br><span style="color:var(--red)">CARGO.</span></h2>
      <div class="contact-details">
        <div class="contact-row"><div class="c-icon">📍</div><div><div class="c-label">Address</div><div class="c-val">No. 184–1/3, Main Road, Anna Nagar, Elankulam Post, Nanguneri Taluk, Tirunelveli District, Tamil Nadu – 627 110</div></div></div>
        <div class="contact-row"><div class="c-icon">📞</div><div><div class="c-label">Mobile</div><div class="c-val"><a href="tel:9976731444">+91 99767 31444</a><br><a href="tel:9788748900">+91 97887 48900</a></div></div></div>
        <div class="contact-row"><div class="c-icon">✉️</div><div><div class="c-label">Email</div><div class="c-val"><a href="mailto:asathiyamani1969@gmail.com" style="color:var(--red)">asathiyamani1969@gmail.com</a></div></div></div>
      </div>
    </div>
  </div>
  <div class="contact-form-side">
    <div class="form-title reveal">REQUEST A<br><span>QUOTE</span></div>
    <form id="quoteForm">
      <div class="form-row-2">
        <div class="field"><label>Your Name</label><input type="text" placeholder="Full name" required/></div>
        <div class="field"><label>Phone</label><input type="tel" placeholder="+91 XXXXX XXXXX" required/></div>
      </div>
      <div class="field"><label>Email</label><input type="email" placeholder="your@email.com"/></div>
      <div class="field"><label>Service Required</label>
        <select><option value="">— Choose Service —</option><option>Full Truck Load (FTL)</option><option>Part Load / LTL</option><option>Pan-India Freight</option><option>Express Delivery</option></select>
      </div>
      <div class="form-row-2">
        <div class="field"><label>From (City)</label><input type="text" placeholder="Origin"/></div>
        <div class="field"><label>To (City)</label><input type="text" placeholder="Destination"/></div>
      </div>
      <div class="field"><label>Message</label><textarea placeholder="Cargo type, weight, special requirements…"></textarea></div>
      <button type="submit" class="submit-btn">Send Enquiry 🚛</button>
    </form>
  </div>
</section>

<!-- GST STRIP -->
<div class="gst-strip">
  <div class="gst-item"><div class="gst-key">PAN Card No.</div><div class="gst-val">AWWPV7253P</div></div>
  <div class="gst-item"><div class="gst-key">GST Identification No.</div><div class="gst-val">33AWWPV7253P22A</div></div>
  <div class="gst-item"><div class="gst-key">State Code</div><div class="gst-val">Tamil Nadu — 33</div></div>
  <div class="gst-item"><div class="gst-key">District</div><div class="gst-val">Tirunelveli</div></div>
</div>

<!-- FOOTER -->
<footer>
  <div class="footer-top">
    <div class="footer-brand">
      <div class="footer-name">Asathiya Transports</div>
      <p class="footer-tagline">Premium road freight solutions from the heart of Tamil Nadu. Connecting cargo to destinations across India with reliability and care.</p>
    </div>
    <div class="footer-links">
      <h4>Navigation</h4>
      <ul>
        <li><a href="#about">About Us</a></li>
        <li><a href="#services">Our Services</a></li>
        <li><a href="#fleet">Our Fleet</a></li>
        <li><a href="#contact">Contact</a></li>
      </ul>
    </div>
    <div class="footer-links">
      <h4>Contact</h4>
      <ul>
        <li><a href="tel:9976731444">+91 99767 31444</a></li>
        <li><a href="tel:9788748900">+91 97887 48900</a></li>
        <li><a href="mailto:asathiyamani1969@gmail.com">asathiyamani1969@gmail.com</a></li>
      </ul>
    </div>
  </div>
  <div class="footer-bottom">
    <div class="footer-copy">© 2026 Asathiya Transports. All Rights Reserved. | GST: 33AWWPV7253P22A</div>
    <div class="footer-copy" style="color:var(--border)">Nanguneri Taluk · Tirunelveli · Tamil Nadu 627 110</div>
  </div>
</footer>

<div id="toast">✔ Enquiry sent! We'll contact you shortly.</div>

<script>
// ═══════════════ CURSOR ═══════════════
const cursor = document.getElementById('cursor');
const ring   = document.getElementById('cursor-ring');
let mx=0,my=0,rx=0,ry=0;
document.addEventListener('mousemove',e=>{mx=e.clientX;my=e.clientY;cursor.style.left=mx+'px';cursor.style.top=my+'px'});
setInterval(()=>{rx+=(mx-rx)*0.12;ry+=(my-ry)*0.12;ring.style.left=rx+'px';ring.style.top=ry+'px'},16);
document.querySelectorAll('a,button,.svc-card,.why-item').forEach(el=>{
  el.addEventListener('mouseenter',()=>{cursor.style.width='28px';cursor.style.height='28px';ring.style.width='60px';ring.style.height='60px'});
  el.addEventListener('mouseleave',()=>{cursor.style.width='12px';cursor.style.height='12px';ring.style.width='40px';ring.style.height='40px'});
});

// ═══════════════ LOADER ═══════════════
const loaderBar=document.getElementById('loaderBar');
const loaderPct=document.getElementById('loaderPct');
const loaderLogo=document.querySelector('.loader-logo');
let pct=0;
gsap.to(loaderLogo,{opacity:1,duration:0.8,ease:'power2.out'});
const loaderTimer=setInterval(()=>{
  pct+=Math.random()*4+1;
  if(pct>=100){pct=100;clearInterval(loaderTimer);setTimeout(hideLoader,300)}
  loaderBar.style.width=pct+'%';
  loaderPct.textContent=Math.round(pct)+'%';
},60);
function hideLoader(){
  gsap.to('#loader',{opacity:0,duration:0.8,ease:'power2.inOut',onComplete:()=>{document.getElementById('loader').style.display='none';startHeroAnims()}});
}

// ═══════════════ HERO ANIMS ═══════════════
function startHeroAnims(){
  gsap.from('#heroBadge',{y:30,opacity:0,duration:0.8,ease:'power3.out'});
  gsap.from(['#hline1','#hline2','#hline3'],{y:80,opacity:0,stagger:0.12,duration:0.9,delay:0.2,ease:'power3.out'});
  gsap.from('#heroSub',{y:20,opacity:0,duration:0.8,delay:0.65,ease:'power2.out'});
  gsap.from('#heroActions',{y:20,opacity:0,duration:0.8,delay:0.85,ease:'power2.out'});
}

// ═══════════════ HERO SLIDESHOW ═══════════════
const slides=document.querySelectorAll('.hero-slide');
let slideIdx=0;
setInterval(()=>{
  slides[slideIdx].classList.remove('active');
  slideIdx=(slideIdx+1)%slides.length;
  slides[slideIdx].classList.add('active');
},5000);

// ═══════════════ NAV SCROLL ═══════════════
window.addEventListener('scroll',()=>{
  document.getElementById('mainNav').classList.toggle('scrolled',window.scrollY>60);
});

// ═══════════════ GSAP SCROLL TRIGGERS ═══════════════
gsap.registerPlugin(ScrollTrigger,TextPlugin);
document.querySelectorAll('.reveal').forEach(el=>{
  gsap.fromTo(el,{y:40,opacity:0},{y:0,opacity:1,duration:0.8,ease:'power3.out',scrollTrigger:{trigger:el,start:'top 88%',toggleActions:'play none none none'}});
});

// ═══════════════ STAT COUNTERS ═══════════════
const statNums=document.querySelectorAll('.stat-num[data-target]');
statNums.forEach(el=>{
  ScrollTrigger.create({trigger:el,start:'top 85%',once:true,onEnter:()=>{
    const target=+el.dataset.target,suffix=el.dataset.suffix||'';
    gsap.fromTo({val:0},{val:target},{val:target,duration:1.8,ease:'power2.out',onUpdate:function(){el.textContent=Math.round(this.targets()[0].val)+suffix}});
  }});
});

// ═══════════════ PARALLAX ═══════════════
gsap.to('#parallaxImg',{yPercent:25,ease:'none',scrollTrigger:{trigger:'.parallax-banner',scrub:true}});

// ═══════════════ FLEET SLIDER ═══════════════
let fleetPos=0;
const fleetTrack=document.getElementById('fleetTrack');
const cardW=()=>fleetTrack.children[0].offsetWidth+2;
document.getElementById('nextBtn').addEventListener('click',()=>{
  const max=fleetTrack.children.length-Math.floor(fleetTrack.parentElement.offsetWidth/cardW());
  if(fleetPos<max){fleetPos++;fleetTrack.style.transform=`translateX(-${fleetPos*cardW()}px)`}
});
document.getElementById('prevBtn').addEventListener('click',()=>{
  if(fleetPos>0){fleetPos--;fleetTrack.style.transform=`translateX(-${fleetPos*cardW()}px)`}
});

// ═══════════════ FORM ═══════════════
document.getElementById('quoteForm').addEventListener('submit',function(e){
  e.preventDefault();
  const t=document.getElementById('toast');
  t.classList.add('show');setTimeout(()=>t.classList.remove('show'),3800);
  this.reset();
});

// ═══════════════ SMOOTH SCROLL ═══════════════
document.querySelectorAll('a[href^="#"]').forEach(a=>{
  a.addEventListener('click',e=>{e.preventDefault();document.querySelector(a.getAttribute('href'))?.scrollIntoView({behavior:'smooth',block:'start'})});
});

// ═══════════════ CANVAS PARTICLES ═══════════════
(function(){
  const canvas=document.getElementById('particles');
  const ctx=canvas.getContext('2d');
  let W,H,pts=[];
  function resize(){W=canvas.width=innerWidth;H=canvas.height=innerHeight}
  resize();window.addEventListener('resize',resize);
  for(let i=0;i<60;i++){
    pts.push({x:Math.random()*W,y:Math.random()*H,vx:(Math.random()-0.5)*0.3,vy:(Math.random()-0.5)*0.3,r:Math.random()*1.5+0.3,a:Math.random()});
  }
  function draw(){
    ctx.clearRect(0,0,W,H);
    pts.forEach(p=>{
      p.x+=p.vx;p.y+=p.vy;
      if(p.x<0)p.x=W;if(p.x>W)p.x=0;
      if(p.y<0)p.y=H;if(p.y>H)p.y=0;
      ctx.beginPath();
      ctx.arc(p.x,p.y,p.r,0,Math.PI*2);
      ctx.fillStyle=`rgba(230,51,40,${p.a*0.4})`;
      ctx.fill();
    });
    // connect nearby
    for(let i=0;i<pts.length;i++){
      for(let j=i+1;j<pts.length;j++){
        const dx=pts[i].x-pts[j].x,dy=pts[i].y-pts[j].y,d=Math.sqrt(dx*dx+dy*dy);
        if(d<120){ctx.beginPath();ctx.moveTo(pts[i].x,pts[i].y);ctx.lineTo(pts[j].x,pts[j].y);ctx.strokeStyle=`rgba(230,51,40,${(1-d/120)*0.08})`;ctx.lineWidth=0.5;ctx.stroke()}
      }
    }
    requestAnimationFrame(draw);
  }
  draw();
})();

// ═══════════════ THREE.JS WIREFRAME SPHERE ═══════════════
(function(){
  try{
    const canvas=document.getElementById('three-canvas');
    const renderer=new THREE.WebGLRenderer({canvas,alpha:true,antialias:true});
    renderer.setSize(window.innerWidth,window.innerHeight);
    renderer.setPixelRatio(Math.min(devicePixelRatio,2));
    const scene=new THREE.Scene();
    const camera=new THREE.PerspectiveCamera(60,window.innerWidth/window.innerHeight,0.1,100);
    camera.position.z=3;
    const geo=new THREE.TorusKnotGeometry(0.9,0.28,120,16);
    const mat=new THREE.MeshBasicMaterial({color:0xe63328,wireframe:true,opacity:0.12,transparent:true});
    const mesh=new THREE.Mesh(geo,mat);
    mesh.position.set(4,-0.5,0);
    scene.add(mesh);
    const geo2=new THREE.IcosahedronGeometry(1.2,1);
    const mat2=new THREE.MeshBasicMaterial({color:0xf57c2b,wireframe:true,opacity:0.06,transparent:true});
    const mesh2=new THREE.Mesh(geo2,mat2);
    mesh2.position.set(-4,1,0);
    scene.add(mesh2);
    window.addEventListener('resize',()=>{
      renderer.setSize(window.innerWidth,window.innerHeight);
      camera.aspect=window.innerWidth/window.innerHeight;
      camera.updateProjectionMatrix();
    });
    function animate(){
      requestAnimationFrame(animate);
      mesh.rotation.x+=0.003;mesh.rotation.y+=0.005;
      mesh2.rotation.x-=0.002;mesh2.rotation.y+=0.003;
      renderer.render(scene,camera);
    }
    animate();
  }catch(e){}
})();
</script>
</body>
</html>
