import React, { useState, useEffect, useRef } from 'react';
import { Sparkles, Lock, ArrowRight, Fingerprint, Activity, Hexagon } from 'lucide-react';

const App = () => {
  const [mousePosition, setMousePosition] = useState({ x: 0, y: 0 });
  const [email, setEmail] = useState('');
  const [accessRequested, setAccessRequested] = useState(false);
  const [scrollProgress, setScrollProgress] = useState(0);

  // Urmărește cursorul pentru efectul de lanternă (Chiaroscuro)
  useEffect(() => {
    const updateMousePosition = (e) => {
      setMousePosition({ x: e.clientX, y: e.clientY });
    };
    
    const handleScroll = () => {
      const totalScroll = document.documentElement.scrollTop;
      const windowHeight = document.documentElement.scrollHeight - document.documentElement.clientHeight;
      const scroll = `${totalScroll / windowHeight}`;
      setScrollProgress(Number(scroll));
    }

    window.addEventListener('mousemove', updateMousePosition);
    window.addEventListener('scroll', handleScroll);

    return () => {
      window.removeEventListener('mousemove', updateMousePosition);
      window.removeEventListener('scroll', handleScroll);
    };
  }, []);

  const handleJoin = (e) => {
    e.preventDefault();
    if (email) {
      setTimeout(() => setAccessRequested(true), 800);
    }
  };

  return (
    <div className="min-h-screen bg-[#050505] text-stone-200 overflow-x-hidden font-sans selection:bg-[#D4AF37] selection:text-black">
      {/* Import Fonts */}
      <style>{`
        @import url('https://fonts.googleapis.com/css2?family=Cinzel:wght@400;600&family=Manrope:wght@200;300;400;600&family=Playfair+Display:ital,wght@0,400;0,600;1,400&display=swap');
        
        .font-serif-display { font-family: 'Playfair Display', serif; }
        .font-tech { font-family: 'Manrope', sans-serif; }
        .font-cinzel { font-family: 'Cinzel', serif; }

        .noise-bg {
          position: fixed;
          top: 0;
          left: 0;
          width: 100%;
          height: 100%;
          pointer-events: none;
          z-index: 50;
          opacity: 0.03;
          background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noiseFilter'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.65' numOctaves='3' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noiseFilter)' opacity='1'/%3E%3C/svg%3E");
        }
        
        .gold-glow {
          text-shadow: 0 0 20px rgba(212, 175, 55, 0.3);
        }

        /* Custom Scrollbar */
        ::-webkit-scrollbar {
          width: 6px;
        }
        ::-webkit-scrollbar-track {
          background: #0a0a0a;
        }
        ::-webkit-scrollbar-thumb {
          background: #333;
          border-radius: 3px;
        }
      `}</style>

      <div className="noise-bg"></div>

      {/* Spotlight Effect - Chiaroscuro */}
      <div 
        className="pointer-events-none fixed inset-0 z-30 transition-opacity duration-300"
        style={{
          background: `radial-gradient(600px circle at ${mousePosition.x}px ${mousePosition.y}px, rgba(255,255,255,0.03), transparent 40%)`
        }}
      />

      {/* Navigation / Header */}
      <nav className="fixed top-0 w-full z-40 px-6 py-6 flex justify-between items-center mix-blend-difference">
        <div className="text-xs font-tech tracking-[0.3em] opacity-60">NORFEA PROTOCOL</div>
        <div className="flex gap-2 items-center text-[#D4AF37] text-xs font-tech tracking-widest border border-[#D4AF37]/20 px-3 py-1 rounded-full backdrop-blur-md">
          <div className="w-1.5 h-1.5 bg-[#D4AF37] rounded-full animate-pulse"></div>
          STATUS: HIDDEN
        </div>
      </nav>

      {/* HERO SECTION */}
      <section className="relative h-screen flex flex-col justify-center items-center px-6 overflow-hidden">
        {/* VIDEO BACKGROUND */}
        <div className="absolute inset-0 z-0">
          <div className="absolute inset-0 bg-black/40 z-10"></div> {/* Overlay pentru lizibilitate */}
          <video 
            autoPlay 
            loop 
            muted 
            playsInline 
            className="w-full h-full object-cover opacity-90"
          >
            {/* Folosim fișierul încărcat de utilizator */}
            <source src="NORFEA 7.mp4" type="video/mp4" />
            {/* Fallback în cazul în care fișierul local nu este găsit în preview */}
            <source src="https://videos.pexels.com/video-files/3045163/3045163-hd_1920_1080_24fps.mp4" type="video/mp4" />
            Your browser does not support the video tag.
          </video>
        </div>
        
        <div className="z-20 text-center space-y-8 max-w-4xl opacity-0 animate-[fadeIn_2s_ease-out_forwards]">
          <h2 className="text-stone-300 font-tech text-xs md:text-sm tracking-[0.5em] uppercase mb-4 mix-blend-difference">
            Dincolo de Parfum
          </h2>
          {/* Logo Auriu */}
          <h1 className="font-cinzel text-6xl md:text-8xl lg:text-9xl tracking-tight text-[#D4AF37] pb-4 drop-shadow-2xl gold-glow">
            NORFEA
          </h1>
          <p className="font-serif-display italic text-xl md:text-2xl text-stone-200 max-w-2xl mx-auto leading-relaxed drop-shadow-lg">
            "If you know, you know."
          </p>
        </div>

        {/* Scroll Indicator */}
        <div className="absolute bottom-10 z-20 flex flex-col items-center gap-2 opacity-50 animate-bounce duration-[3000ms]">
          <span className="text-[10px] tracking-widest font-tech uppercase text-[#D4AF37]">Descoperă</span>
          <div className="w-[1px] h-12 bg-gradient-to-b from-transparent via-[#D4AF37] to-transparent"></div>
        </div>
      </section>

      {/* MANIFESTO SECTION - The Alchemist Letter & Artefact */}
      <section className="relative py-32 px-6 md:px-12 border-t border-white/5 bg-stone-950">
        <div className="max-w-6xl mx-auto grid grid-cols-1 md:grid-cols-2 gap-20 items-center">
          <div className="space-y-8 order-2 md:order-1">
            <div className="w-12 h-[1px] bg-[#D4AF37] mb-8"></div>
            <h3 className="font-cinzel text-3xl text-white mb-6">Buncărul de Identitate</h3>
            <div className="font-serif-display text-lg text-stone-400 space-y-6 leading-loose">
              <p>
                Lumea este saturată de zgomot. De arome dulci create pentru a plăcea maselor. 
                <strong className="text-stone-200 font-normal"> Norfea respinge validarea externă.</strong>
              </p>
              <p>
                Ceea ce construim aici este un <span className="text-[#D4AF37]/80 italic">Identity Tech</span>. 
                Un algoritm olfactiv care nu te întreabă ce flori preferi, ci analizează textura sufletului tău. 
                Piatră rece? Lemn ars? Metal încins?
              </p>
              <p>
                Artefactele noastre sunt create în regim <em>Chiaroscuro</em>: contrast absolut între lumină și întuneric. 
                Sticla Matte Obsidian ascunde esența, protejând-o de privirile celor neinițiați.
              </p>
            </div>
            <div className="pt-8">
              <div className="inline-flex items-center gap-4 text-xs font-tech tracking-widest text-stone-500">
                <Hexagon size={14} className="text-[#D4AF37]" />
                ALGORITMUL SONAR V1.0
              </div>
            </div>
          </div>
          
          {/* Visual Representation: Chiaroscuro Artefact (Bottle + Bracelet) */}
          <div className="order-1 md:order-2 relative group">
             {/* Container pentru efectul Chiaroscuro dramatic */}
             <div className="relative w-full aspect-square md:aspect-[4/5] overflow-hidden bg-black shadow-2xl shadow-black border border-stone-800/50">
                {/* Imaginea BRANDING.png încărcată de utilizator */}
                <img 
                  src="BRANDING.png" 
                  onError={(e) => {e.target.src = "/api/placeholder/600/800";}} // Fallback în caz de eroare
                  alt="Norfea Branding - Sticle și Brățări" 
                  className="w-full h-full object-cover opacity-80 group-hover:opacity-100 group-hover:scale-105 transition-all duration-1000 ease-out"
                />
                
                {/* Gradient Chiaroscuro (Umbră puternică) */}
                <div className="absolute inset-0 bg-gradient-to-t from-black via-transparent to-transparent opacity-80"></div>
                
                {/* Etichetă Tehnică */}
                <div className="absolute bottom-8 left-0 w-full text-center z-10">
                   <p className="font-tech text-[9px] tracking-[0.4em] text-[#D4AF37] mb-1">COLECȚIA COMPLETĂ</p>
                   <p className="font-cinzel text-xl text-white tracking-widest drop-shadow-md">IDENTITY ARTEFACTS</p>
                </div>
             </div>
          </div>
        </div>
      </section>

      {/* THE PROCESS / SONAR */}
      <section className="py-24 bg-stone-950 relative overflow-hidden">
        <div className="absolute inset-0 flex items-center justify-center opacity-[0.02]">
           <Fingerprint size={600} strokeWidth={0.5} />
        </div>

        <div className="max-w-6xl mx-auto px-6 relative z-10">
          <div className="grid grid-cols-1 md:grid-cols-3 gap-8">
            {[
              { 
                icon: Activity, 
                title: "SCANARE PSIHOGRAFICĂ", 
                desc: "Nu chestionar. O conversație abstractă cu AI-ul nostru pentru a mapa arhitectura minții tale." 
              },
              { 
                icon: Lock, 
                title: "ACCES GATED", 
                desc: "Luxul înseamnă raritate. Accesul la configurator este permis doar pe bază de invitație sau waitlist." 
              },
              { 
                icon: Sparkles, 
                title: "CONSTRUCȚIE ARTIZANALĂ", 
                desc: "Fiecare sticlă este sigilată manual. O fuziune între precizie laser și imperfecțiune umană." 
              }
            ].map((item, idx) => (
              <div key={idx} className="p-8 border border-white/5 bg-[#050505]/50 backdrop-blur-sm hover:border-[#D4AF37]/20 transition-colors group">
                <item.icon className="w-8 h-8 text-stone-600 mb-6 group-hover:text-[#D4AF37] transition-colors" />
                <h4 className="font-tech text-sm tracking-widest text-stone-300 mb-4">{item.title}</h4>
                <p className="font-serif-display text-stone-500 leading-relaxed text-sm">
                  {item.desc}
                </p>
              </div>
            ))}
          </div>
        </div>
      </section>

      {/* WAITLIST / ACCESS */}
      <section className="min-h-[80vh] flex flex-col justify-center items-center px-6 relative border-t border-white/5">
        <div className="max-w-xl w-full text-center space-y-10">
          
          <div className="space-y-4">
            <h2 className="font-cinzel text-4xl md:text-5xl text-white">
              Căutarea a început
            </h2>
            <p className="font-tech text-sm text-[#D4AF37] tracking-widest uppercase">
              Batch 01: Obsidian &mdash; 88/100 Locuri Ocupate
            </p>
          </div>

          <p className="font-serif-display text-stone-400 text-lg">
            Site-ul complet este un privilegiu, nu un drept.
            Lansăm în curând platforma de Identity Tech.
            <br />
            Solicită acces pentru a fi notificat când poarta se deschide.
          </p>

          {!accessRequested ? (
            <form onSubmit={handleJoin} className="relative w-full max-w-md mx-auto group">
              <input 
                type="email" 
                placeholder="ADRESA DE EMAIL"
                value={email}
                onChange={(e) => setEmail(e.target.value)}
                className="w-full bg-transparent border-b border-stone-700 py-4 px-2 text-center text-white font-tech tracking-wider focus:outline-none focus:border-[#D4AF37] transition-all placeholder:text-stone-800"
                required
              />
              <button 
                type="submit"
                className="mt-8 flex items-center justify-center gap-2 w-full py-4 bg-stone-900 hover:bg-[#D4AF37] text-stone-400 hover:text-black font-tech text-xs tracking-[0.2em] transition-all duration-500 uppercase border border-stone-800 hover:border-[#D4AF37]"
              >
                Solicită Acces <ArrowRight size={14} />
              </button>
            </form>
          ) : (
            <div className="animate-[fadeIn_1s_ease-out]">
              <div className="p-6 border border-[#D4AF37]/30 bg-[#D4AF37]/5 inline-block">
                <p className="font-cinzel text-xl text-[#D4AF37] mb-2">Identitate Înregistrată</p>
                <p className="font-tech text-xs text-stone-400 tracking-wider">VEI PRIMI SEMNALUL LA MOMENTUL POTRIVIT.</p>
              </div>
            </div>
          )}

          <div className="pt-12 opacity-30">
            <img src="/api/placeholder/100/50" alt="Norfea Sigil" className="mx-auto h-12 grayscale invert opacity-50" />
          </div>
        </div>
      </section>

      {/* FOOTER */}
      <footer className="py-12 border-t border-white/5 text-center">
        <div className="font-tech text-[10px] text-stone-600 tracking-[0.3em] uppercase space-y-2">
          <p>© 2026 NORFEA. IDENTITY TECH.</p>
          <p>BUCUREȘTI — PARIS — TOKYO</p>
          <div className="flex justify-center gap-4 mt-4 text-stone-700">
            <span className="hover:text-stone-400 cursor-pointer transition-colors">Instagram</span>
            <span className="hover:text-stone-400 cursor-pointer transition-colors">Manifesto</span>
            <span className="hover:text-stone-400 cursor-pointer transition-colors">Legal</span>
          </div>
        </div>
      </footer>
      
      {/* Global CSS keyframes for one-off animations */}
      <style>{`
        @keyframes fadeIn {
          from { opacity: 0; transform: translateY(20px); }
          to { opacity: 1; transform: translateY(0); }
        }
      `}</style>
    </div>
  );
};

export default App;
