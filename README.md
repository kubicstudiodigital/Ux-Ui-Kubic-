# Ux-Ui-Kubic-
Portafolio
import { useState } from "react";

const NEON   = "#00d4ff";
const NEON2  = "#0099cc";
const NEONGL = "rgba(0,212,255,0.18)";
const BG     = "#050810";
const CARD   = "#0b1020";
const CARD2  = "#0d1428";
const BORDER = "#0d2a3a";
const MUTED  = "#3a6a8a";
const ACCENT = "#ff2d78";

// ── Shared atoms ─────────────────────────────────────────────────────────────
const KubicLogo = ({ invert }) => (
  <div style={{ display:"flex", alignItems:"center", gap:8, fontFamily:"'Orbitron',sans-serif", fontWeight:900, fontSize:17, letterSpacing:3, color: invert ? BG : NEON, textShadow: invert ? "none" : `0 0 10px ${NEON}` }}>
    <svg width="22" height="22" viewBox="0 0 24 24" fill="none">
      <rect x="1" y="1" width="9" height="9" rx="2" fill={invert ? BG : NEON} style={{filter: invert ? "none" : `drop-shadow(0 0 4px ${NEON})`}}/>
      <rect x="14" y="1" width="9" height="9" rx="2" fill={invert ? BG : NEON} style={{filter: invert ? "none" : `drop-shadow(0 0 4px ${NEON})`}}/>
      <rect x="1" y="14" width="9" height="9" rx="2" fill={invert ? BG : NEON} style={{filter: invert ? "none" : `drop-shadow(0 0 4px ${NEON})`}}/>
      <rect x="14" y="14" width="9" height="9" rx="2" fill={invert ? BG : NEON} style={{filter: invert ? "none" : `drop-shadow(0 0 4px ${NEON})`}}/>
    </svg>
    KUBIC
  </div>
);

const NavBar = ({ invert }) => (
  <div style={{ background: invert ? "#001a2a" : "#070e1c", padding:"16px 18px", display:"flex", alignItems:"center", justifyContent:"space-between", borderBottom:`1px solid ${BORDER}` }}>
    <KubicLogo invert={invert} />
    <div style={{ display:"flex", gap:14, alignItems:"center" }}>
      <svg width="22" height="22" fill="none" stroke={NEON} strokeWidth="2" viewBox="0 0 24 24" style={{filter:`drop-shadow(0 0 4px ${NEON})`}}><circle cx="12" cy="8" r="4"/><path d="M4 20c0-4 3.6-7 8-7s8 3 8 7"/></svg>
      <svg width="22" height="22" fill="none" stroke={NEON} strokeWidth="2.5" viewBox="0 0 24 24" style={{filter:`drop-shadow(0 0 4px ${NEON})`}}><line x1="3" y1="6" x2="21" y2="6"/><line x1="3" y1="12" x2="21" y2="12"/><line x1="3" y1="18" x2="21" y2="18"/></svg>
    </div>
  </div>
);

const BottomNav = ({ active }) => {
  const tabs = [
    { id:"home",      label:"HOME",      icon:<svg width="17" height="17" fill="none" stroke="currentColor" strokeWidth="2" viewBox="0 0 24 24"><path d="M3 9l9-7 9 7v11a2 2 0 01-2 2H5a2 2 0 01-2-2z"/><polyline points="9 22 9 12 15 12 15 22"/></svg> },
    { id:"servicios", label:"SERVICIOS", icon:<svg width="17" height="17" fill="none" stroke="currentColor" strokeWidth="2" viewBox="0 0 24 24"><circle cx="12" cy="12" r="3"/><path d="M12 1v4M12 19v4M4.22 4.22l2.83 2.83M16.95 16.95l2.83 2.83M1 12h4M19 12h4M4.22 19.78l2.83-2.83M16.95 7.05l2.83-2.83"/></svg> },
    { id:"proyectos", label:"PROYECTOS", icon:<svg width="17" height="17" fill="none" stroke="currentColor" strokeWidth="2" viewBox="0 0 24 24"><rect x="3" y="3" width="7" height="7"/><rect x="14" y="3" width="7" height="7"/><rect x="3" y="14" width="7" height="7"/><rect x="14" y="14" width="7" height="7"/></svg> },
    { id:"contacto",  label:"CONTACTO",  icon:<svg width="17" height="17" fill="none" stroke="currentColor" strokeWidth="2" viewBox="0 0 24 24"><path d="M22 16.92v3a2 2 0 01-2.18 2 19.79 19.79 0 01-8.63-3.07A19.5 19.5 0 013.07 8.81 19.79 19.79 0 01.1 4.18 2 2 0 012.11 2h3a2 2 0 012 1.72c.127.96.361 1.903.7 2.81a2 2 0 01-.45 2.11L6.91 9.91a16 16 0 006.29 6.29l1.27-.45a2 2 0 012.11-.45c.907.339 1.85.573 2.81.7A2 2 0 0122 18z"/></svg> },
  ];
  return (
    <div style={{ display:"flex", background:"#07101e", borderTop:`1px solid ${BORDER}` }}>
      {tabs.map(t => (
        <div key={t.id} style={{ flex:1, padding:"11px 4px 8px", display:"flex", flexDirection:"column", alignItems:"center", gap:3, fontSize:8, fontFamily:"'Orbitron',sans-serif", fontWeight:700, letterSpacing:.8, color: active===t.id ? NEON : MUTED, background: active===t.id ? "rgba(0,212,255,0.08)" : "transparent", borderTop: active===t.id ? `2px solid ${NEON}` : "2px solid transparent", textShadow: active===t.id ? `0 0 8px ${NEON}` : "none" }}>
          {t.icon}{t.label}
        </div>
      ))}
    </div>
  );
};

// Scanline + grid overlay
const CyberBG = ({ children, style={} }) => (
  <div style={{ position:"relative", ...style }}>
    <div style={{ position:"absolute", inset:0, backgroundImage:`linear-gradient(rgba(0,212,255,0.03) 1px, transparent 1px), linear-gradient(90deg, rgba(0,212,255,0.03) 1px, transparent 1px)`, backgroundSize:"20px 20px", pointerEvents:"none" }}/>
    <div style={{ position:"absolute", inset:0, background:"repeating-linear-gradient(0deg, transparent, transparent 2px, rgba(0,0,0,0.08) 2px, rgba(0,0,0,0.08) 4px)", pointerEvents:"none" }}/>
    {children}
  </div>
);

const NeonTag = ({ label }) => (
  <span style={{ border:`1px solid ${NEON}`, borderRadius:4, padding:"6px 14px", fontSize:11, color:NEON, fontFamily:"'Orbitron',sans-serif", fontWeight:700, letterSpacing:1, background:"rgba(0,212,255,0.06)", boxShadow:`0 0 8px rgba(0,212,255,0.2), inset 0 0 6px rgba(0,212,255,0.05)`, textShadow:`0 0 6px ${NEON}` }}>{label}</span>
);

// ── Phone shell ──────────────────────────────────────────────────────────────
const Phone = ({ title, children }) => (
  <div style={{ display:"flex", flexDirection:"column", alignItems:"center", gap:12 }}>
    <div style={{ fontFamily:"'Orbitron',sans-serif", fontSize:9, fontWeight:700, letterSpacing:3, color:MUTED, textTransform:"uppercase", textShadow:`0 0 6px ${MUTED}` }}>{title}</div>
    <div style={{ width:270, background:BG, borderRadius:32, overflow:"hidden", display:"flex", flexDirection:"column", boxShadow:`0 0 0 1px ${BORDER}, 0 0 30px rgba(0,212,255,0.12), 0 30px 80px rgba(0,0,0,0.8)`, border:"5px solid #0d1428" }}>
      {children}
    </div>
  </div>
);

// ── Screen 1 · CTA ───────────────────────────────────────────────────────────
const Screen1 = () => (
  <Phone title="01 · Pantalla Principal">
    <NavBar />
    <CyberBG style={{ flex:1, background:BG, padding:12 }}>
      <div style={{ background:`linear-gradient(135deg, #001a2e 0%, #001428 100%)`, borderRadius:14, padding:"26px 20px", position:"relative", overflow:"hidden", border:`1px solid rgba(0,212,255,0.3)`, boxShadow:`0 0 20px rgba(0,212,255,0.1), inset 0 0 30px rgba(0,212,255,0.04)` }}>
        {/* corner accent lines */}
        <div style={{ position:"absolute", top:0, left:0, width:30, height:30, borderTop:`2px solid ${NEON}`, borderLeft:`2px solid ${NEON}`, borderRadius:"14px 0 0 0", boxShadow:`-2px -2px 8px rgba(0,212,255,0.4)` }}/>
        <div style={{ position:"absolute", bottom:0, right:0, width:30, height:30, borderBottom:`2px solid ${NEON}`, borderRight:`2px solid ${NEON}`, borderRadius:"0 0 14px 0", boxShadow:`2px 2px 8px rgba(0,212,255,0.4)` }}/>
        {/* bubble icon */}
        <div style={{ position:"absolute", right:14, top:14, width:80, height:68, background:"rgba(0,212,255,0.07)", borderRadius:10, border:`1px solid rgba(0,212,255,0.2)`, display:"flex", alignItems:"center", justifyContent:"center" }}>
          <svg width="36" height="36" fill="none" stroke={NEON} strokeWidth="1.5" viewBox="0 0 24 24" style={{filter:`drop-shadow(0 0 6px ${NEON})`}}><path d="M21 15a2 2 0 01-2 2H7l-4 4V5a2 2 0 012-2h14a2 2 0 012 2z"/><line x1="8" y1="9" x2="16" y2="9"/><line x1="8" y1="13" x2="14" y2="13"/></svg>
        </div>
        <div style={{ fontFamily:"'Orbitron',sans-serif", fontSize:20, fontWeight:900, color:"#fff", lineHeight:1.15, marginBottom:10, maxWidth:150, textShadow:`0 0 20px rgba(0,212,255,0.3)` }}>¿LISTO PARA DAR EL SALTO?</div>
        <div style={{ fontSize:11, color:"#5a8aaa", lineHeight:1.65, marginBottom:20 }}>Transformemos tu visión en una realidad digital dominante. Nuestro equipo está listo para el desafío.</div>
        <button style={{ background:`linear-gradient(90deg, #001a2e, #003a5a)`, color:NEON, border:`1px solid ${NEON}`, borderRadius:6, padding:"13px 0", fontFamily:"'Orbitron',sans-serif", fontSize:10, fontWeight:900, letterSpacing:2, width:"100%", cursor:"pointer", boxShadow:`0 0 14px rgba(0,212,255,0.3), inset 0 0 14px rgba(0,212,255,0.05)`, textShadow:`0 0 8px ${NEON}` }}>HABLEMOS AHORA</button>
      </div>
    </CyberBG>
    <BottomNav active="proyectos" />
  </Phone>
);

// ── Screen 2 · Branding ──────────────────────────────────────────────────────
const Screen2 = () => (
  <Phone title="02 · Diseño Gráfico & Branding">
    <NavBar />
    <CyberBG style={{ flex:1, background:BG, padding:12 }}>
      <div style={{ background:CARD, borderRadius:14, padding:"22px 18px", border:`1px solid ${BORDER}`, position:"relative", overflow:"hidden", boxShadow:`inset 0 0 40px rgba(0,212,255,0.03)` }}>
        <div style={{ position:"absolute", top:0, right:0, width:60, height:60, background:`radial-gradient(circle at top right, rgba(0,212,255,0.12), transparent 70%)` }}/>
        <div style={{ fontFamily:"'Orbitron',sans-serif", fontSize:38, fontWeight:900, color:"rgba(0,212,255,0.12)", lineHeight:1, marginBottom:10, textShadow:`0 0 20px rgba(0,212,255,0.1)` }}>01</div>
        <div style={{ fontFamily:"'Orbitron',sans-serif", fontSize:16, fontWeight:900, color:"#fff", marginBottom:10, lineHeight:1.3, textShadow:`0 0 12px rgba(0,212,255,0.2)` }}>Diseño Gráfico &{"\n"}Branding</div>
        <div style={{ fontSize:11, color:MUTED, lineHeight:1.7, marginBottom:16 }}>Identidades visuales que respiran, reaccionan y evolucionan. De logotipos estáticos a ecosistemas dinámicos.</div>
        <div style={{ display:"flex", gap:8 }}>
          <NeonTag label="BRANDING"/><NeonTag label="LOGO"/>
        </div>
      </div>
    </CyberBG>
    <BottomNav active="servicios" />
  </Phone>
);

// ── Screen 3 · UI/UX ─────────────────────────────────────────────────────────
const Screen3 = () => (
  <Phone title="03 · Diseño de Producto UI/UX">
    <NavBar />
    <CyberBG style={{ flex:1, background:BG, padding:12 }}>
      <div style={{ background:CARD, borderRadius:14, padding:"22px 18px", border:`1px solid ${BORDER}`, position:"relative", overflow:"hidden" }}>
        <div style={{ position:"absolute", bottom:0, left:0, width:80, height:80, background:`radial-gradient(circle at bottom left, rgba(0,212,255,0.1), transparent 70%)` }}/>
        <div style={{ fontFamily:"'Orbitron',sans-serif", fontSize:38, fontWeight:900, color:"rgba(0,212,255,0.12)", lineHeight:1, marginBottom:10 }}>02</div>
        <div style={{ fontFamily:"'Orbitron',sans-serif", fontSize:16, fontWeight:900, color:"#fff", marginBottom:10, lineHeight:1.3, textShadow:`0 0 12px rgba(0,212,255,0.2)` }}>Diseño de Producto{"\n"}UI/UX</div>
        <div style={{ fontSize:11, color:MUTED, lineHeight:1.7, marginBottom:16 }}>Interfaces visualmente impactantes y flujos de usuario optimizados para la conversión y la experiencia.</div>
        <div style={{ display:"flex", gap:8 }}>
          <NeonTag label="UI/UX"/><NeonTag label="FIGMA"/>
        </div>
      </div>
    </CyberBG>
    <BottomNav active="servicios" />
  </Phone>
);

// ── Screen 4 · Full-Stack ─────────────────────────────────────────────────────
const Screen4 = () => (
  <Phone title="04 · Desarrollo Web Full-Stack">
    <NavBar />
    <CyberBG style={{ flex:1, background:BG, padding:12 }}>
      <div style={{ background:CARD, borderRadius:14, padding:"22px 18px", border:`1px solid ${BORDER}`, position:"relative", overflow:"hidden" }}>
        <div style={{ position:"absolute", top:"50%", left:"50%", transform:"translate(-50%,-50%)", width:120, height:120, borderRadius:"50%", background:`radial-gradient(circle, rgba(0,212,255,0.05), transparent 70%)`, pointerEvents:"none" }}/>
        <div style={{ fontFamily:"'Orbitron',sans-serif", fontSize:38, fontWeight:900, color:"rgba(0,212,255,0.12)", lineHeight:1, marginBottom:10 }}>03</div>
        <div style={{ fontFamily:"'Orbitron',sans-serif", fontSize:16, fontWeight:900, color:"#fff", marginBottom:10, lineHeight:1.3, textShadow:`0 0 12px rgba(0,212,255,0.2)` }}>Desarrollo Web{"\n"}Full-Stack</div>
        <div style={{ fontSize:11, color:MUTED, lineHeight:1.7, marginBottom:16 }}>Aplicaciones progresivas, robustas y escalables con las tecnologías más vanguardistas del mercado.</div>
        <div style={{ display:"flex", gap:8 }}>
          <NeonTag label="REACT"/><NeonTag label="NODE"/>
        </div>
      </div>
    </CyberBG>
    <BottomNav active="servicios" />
  </Phone>
);

// ── Screen 5 · IA / Video ─────────────────────────────────────────────────────
const Screen5 = () => (
  <Phone title="05 · Publicidad & Post-Producción IA">
    <NavBar />
    <CyberBG style={{ flex:1, background:BG, padding:12 }}>
      <div style={{ background:CARD, borderRadius:14, padding:"22px 18px", border:`1px solid rgba(255,45,120,0.25)`, position:"relative", overflow:"hidden", boxShadow:`inset 0 0 30px rgba(255,45,120,0.04)` }}>
        <div style={{ position:"absolute", top:0, right:0, width:80, height:80, background:`radial-gradient(circle at top right, rgba(255,45,120,0.12), transparent 70%)` }}/>
        <div style={{ fontFamily:"'Orbitron',sans-serif", fontSize:38, fontWeight:900, color:"rgba(255,45,120,0.15)", lineHeight:1, marginBottom:10 }}>04</div>
        <div style={{ fontFamily:"'Orbitron',sans-serif", fontSize:16, fontWeight:900, color:"#fff", marginBottom:10, lineHeight:1.3, textShadow:`0 0 12px rgba(255,45,120,0.3)` }}>Publicidad &{"\n"}Post-Producción IA</div>
        <div style={{ fontSize:11, color:MUTED, lineHeight:1.7, marginBottom:16 }}>Campañas digitales potenciadas con inteligencia artificial y producción audiovisual de vanguardia.</div>
        <div style={{ display:"flex", gap:8 }}>
          {["IA","VIDEO"].map(t => <span key={t} style={{ border:`1px solid ${ACCENT}`, borderRadius:4, padding:"6px 14px", fontSize:11, color:ACCENT, fontFamily:"'Orbitron',sans-serif", fontWeight:700, letterSpacing:1, background:"rgba(255,45,120,0.06)", boxShadow:`0 0 8px rgba(255,45,120,0.2)`, textShadow:`0 0 6px ${ACCENT}` }}>{t}</span>)}
        </div>
      </div>
    </CyberBG>
    <BottomNav active="servicios" />
  </Phone>
);

// ── Screen 6 · Contacto ───────────────────────────────────────────────────────
const Screen6 = () => (
  <Phone title="06 · Contacto">
    <NavBar />
    <CyberBG style={{ flex:1, background:"#070e1c", padding:12 }}>
      <div style={{ padding:"8px 4px 16px" }}>
        <div style={{ fontFamily:"'Orbitron',sans-serif", fontSize:22, fontWeight:900, color:"#fff", marginBottom:6, textShadow:`0 0 20px rgba(0,212,255,0.3)` }}>CONTACTO</div>
        <div style={{ width:50, height:2, background:`linear-gradient(90deg, ${NEON}, transparent)`, marginBottom:12, boxShadow:`0 0 8px ${NEON}` }}/>
        <div style={{ fontSize:11, color:MUTED, lineHeight:1.7, marginBottom:18 }}>Contanos sobre tu proyecto y te respondemos a la brevedad.</div>
        {[
          { icon:<svg width="18" height="18" fill="none" stroke={NEON} strokeWidth="2" viewBox="0 0 24 24" style={{filter:`drop-shadow(0 0 4px ${NEON})`}}><circle cx="12" cy="12" r="10"/><line x1="2" y1="12" x2="22" y2="12"/><path d="M12 2a15.3 15.3 0 010 20M12 2a15.3 15.3 0 000 20"/></svg>, label:"Web", value:"kubicstudiodigital.com", color: NEON },
          { icon:<svg width="18" height="18" fill="none" stroke={NEON} strokeWidth="2" viewBox="0 0 24 24" style={{filter:`drop-shadow(0 0 4px ${NEON})`}}><path d="M21 15a2 2 0 01-2 2H7l-4 4V5a2 2 0 012-2h14a2 2 0 012 2z"/></svg>, label:"WhatsApp", value:"Escribinos", color: NEON },
        ].map((c,i) => (
          <div key={i} style={{ background:CARD, borderRadius:10, padding:"12px 14px", marginBottom:8, display:"flex", alignItems:"center", gap:12, border:`1px solid ${BORDER}`, boxShadow:`0 0 10px rgba(0,212,255,0.06)` }}>
            <div>{c.icon}</div>
            <div>
              <div style={{ fontSize:9, color:MUTED, marginBottom:2, fontFamily:"'Orbitron',sans-serif", letterSpacing:1 }}>{c.label}</div>
              <div style={{ fontSize:12, fontWeight:700, color:c.color, fontFamily:"'Orbitron',sans-serif", textShadow:`0 0 6px ${c.color}` }}>{c.value}</div>
            </div>
          </div>
        ))}
      </div>
    </CyberBG>
    <BottomNav active="contacto" />
  </Phone>
);

// ── Screen 7 · Banner Hero ────────────────────────────────────────────────────
const Screen7 = () => (
  <Phone title="07 · Banner Hero Cyberpunk">
    <div style={{ background:"#020510", padding:"20px 14px 16px", position:"relative", overflow:"hidden", minHeight:170 }}>
      {/* grid */}
      <div style={{ position:"absolute", inset:0, backgroundImage:`linear-gradient(rgba(0,212,255,0.05) 1px, transparent 1px), linear-gradient(90deg, rgba(0,212,255,0.05) 1px, transparent 1px)`, backgroundSize:"18px 18px" }}/>
      {/* glow blobs */}
      <div style={{ position:"absolute", left:-20, top:"30%", width:100, height:100, borderRadius:"50%", background:"rgba(0,212,255,0.15)", filter:"blur(30px)" }}/>
      <div style={{ position:"absolute", right:-20, bottom:"20%", width:80, height:80, borderRadius:"50%", background:"rgba(255,45,120,0.15)", filter:"blur(25px)" }}/>
      {/* neon letters */}
      <div style={{ position:"absolute", left:4, top:"50%", transform:"translateY(-50%)", fontFamily:"'Orbitron',sans-serif", fontSize:52, fontWeight:900, color:"transparent", WebkitTextStroke:`1.5px rgba(0,212,255,0.5)`, filter:`drop-shadow(0 0 8px rgba(0,212,255,0.6))` }}>KU</div>
      <div style={{ position:"absolute", right:4, top:"50%", transform:"translateY(-50%)", fontFamily:"'Orbitron',sans-serif", fontSize:52, fontWeight:900, color:"transparent", WebkitTextStroke:`1.5px rgba(255,45,120,0.6)`, filter:`drop-shadow(0 0 8px rgba(255,45,120,0.6))` }}>IC</div>
      {/* center device */}
      <div style={{ position:"relative", display:"flex", flexDirection:"column", alignItems:"center", gap:4 }}>
        <div style={{ fontFamily:"'Orbitron',sans-serif", fontSize:8, letterSpacing:4, color:"rgba(0,212,255,0.5)", marginBottom:4, textShadow:`0 0 6px ${NEON}` }}>KUBIC</div>
        <div style={{ width:72, height:100, background:"linear-gradient(145deg,#c0ccd8,#90a0b0)", borderRadius:12, display:"flex", alignItems:"center", justifyContent:"center", boxShadow:`0 0 20px rgba(0,212,255,0.5), 0 0 40px rgba(255,45,120,0.2), 0 0 0 1px rgba(255,255,255,0.2)` }}>
          <div style={{ width:44, height:44, background:`linear-gradient(135deg, #00d4ff, #ff2d78, #00d4ff)`, borderRadius:8, display:"flex", alignItems:"center", justifyContent:"center", boxShadow:`0 0 16px rgba(0,212,255,0.8)` }}>
            <svg width="24" height="24" viewBox="0 0 24 24" fill="none">
              <rect x="1" y="1" width="9" height="9" rx="2" fill="rgba(0,0,0,0.7)"/>
              <rect x="14" y="1" width="9" height="9" rx="2" fill="rgba(0,0,0,0.7)"/>
              <rect x="1" y="14" width="9" height="9" rx="2" fill="rgba(0,0,0,0.7)"/>
              <rect x="14" y="14" width="9" height="9" rx="2" fill="rgba(0,0,0,0.7)"/>
            </svg>
          </div>
        </div>
      </div>
    </div>
    <div style={{ padding:"12px 14px 14px", background:"#07101e", borderTop:`1px solid ${BORDER}` }}>
      <div style={{ fontFamily:"'Orbitron',sans-serif", fontSize:13, fontWeight:900, color:"#fff", marginBottom:3, textShadow:`0 0 10px rgba(0,212,255,0.3)` }}>KUBIC STUDIO DIGITAL</div>
      <div style={{ fontSize:10, color:MUTED, fontFamily:"'Orbitron',sans-serif", letterSpacing:1 }}>Branding · Web · IA · Video</div>
    </div>
  </Phone>
);

// ── Main gallery ──────────────────────────────────────────────────────────────
export default function KubicCyberpunk() {
  const [active, setActive] = useState(null);

  const screens = [
    { id:1, comp:<Screen1/> },
    { id:2, comp:<Screen2/> },
    { id:3, comp:<Screen3/> },
    { id:4, comp:<Screen4/> },
    { id:5, comp:<Screen5/> },
    { id:6, comp:<Screen6/> },
    { id:7, comp:<Screen7/> },
  ];

  return (
    <>
      <style>{`
        @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Share+Tech+Mono&display=swap');
        * { box-sizing:border-box; margin:0; padding:0; }
        body { background:#020510; font-family:'Share Tech Mono',monospace; }
        ::-webkit-scrollbar { width:4px; }
        ::-webkit-scrollbar-track { background:#020510; }
        ::-webkit-scrollbar-thumb { background:#0d2a3a; border-radius:4px; }
        .mcard { transition:transform .2s, box-shadow .2s; cursor:pointer; }
        .mcard:hover { transform:translateY(-8px); }
        .mcard:hover > div { box-shadow: 0 0 0 1px #0d2a3a, 0 0 40px rgba(0,212,255,0.25), 0 30px 80px rgba(0,0,0,0.8) !important; }
        .overlay { position:fixed; inset:0; background:rgba(2,5,16,0.92); z-index:200; display:flex; align-items:center; justify-content:center; backdrop-filter:blur(10px); }
      `}</style>

      {/* Header */}
      <div style={{ padding:"40px 24px 20px", textAlign:"center", position:"relative" }}>
        <div style={{ position:"absolute", inset:0, backgroundImage:`linear-gradient(rgba(0,212,255,0.03) 1px, transparent 1px), linear-gradient(90deg, rgba(0,212,255,0.03) 1px, transparent 1px)`, backgroundSize:"24px 24px", pointerEvents:"none" }}/>
        <div style={{ display:"flex", alignItems:"center", justifyContent:"center", gap:12, marginBottom:10 }}>
          <svg width="30" height="30" viewBox="0 0 24 24" fill="none" style={{filter:`drop-shadow(0 0 8px ${NEON})`}}>
            <rect x="1" y="1" width="9" height="9" rx="2" fill={NEON}/>
            <rect x="14" y="1" width="9" height="9" rx="2" fill={NEON}/>
            <rect x="1" y="14" width="9" height="9" rx="2" fill={NEON}/>
            <rect x="14" y="14" width="9" height="9" rx="2" fill={NEON}/>
          </svg>
          <span style={{ fontFamily:"'Orbitron',sans-serif", fontSize:24, fontWeight:900, color:NEON, letterSpacing:4, textShadow:`0 0 20px ${NEON}, 0 0 40px rgba(0,212,255,0.4)` }}>KUBIC STUDIO</span>
        </div>
        <div style={{ fontFamily:"'Orbitron',sans-serif", fontSize:9, color:MUTED, letterSpacing:4, textTransform:"uppercase" }}>Mobile App Mockups · Cyberpunk Edition · 7 Pantallas</div>
      </div>

      {/* Grid */}
      <div style={{ display:"grid", gridTemplateColumns:"repeat(auto-fill,minmax(290px,1fr))", gap:36, padding:"16px 32px 60px", maxWidth:1200, margin:"0 auto" }}>
        {screens.map(s => (
          <div key={s.id} className="mcard" onClick={() => setActive(s.id)}>
            {s.comp}
          </div>
        ))}
      </div>

      {/* Lightbox */}
      {active && (
        <div className="overlay" onClick={() => setActive(null)}>
          <div onClick={e => e.stopPropagation()} style={{ position:"relative", transform:"scale(1.25)", transformOrigin:"center" }}>
            {screens.find(s=>s.id===active)?.comp}
            <button onClick={() => setActive(null)} style={{ position:"absolute", top:-38, right:0, background:"#0d1428", border:`1px solid ${NEON}`, color:NEON, borderRadius:4, padding:"5px 14px", fontSize:10, cursor:"pointer", fontFamily:"'Orbitron',sans-serif", fontWeight:700, letterSpacing:2, boxShadow:`0 0 10px rgba(0,212,255,0.3)`, textShadow:`0 0 6px ${NEON}` }}>✕ CERRAR</button>
          </div>
        </div>
      )}
    </>
  );
}
