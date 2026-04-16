<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Segurança e Cidadania | Portal Institucional</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <header role="banner">
        <nav class="container" aria-label="Menu Principal">
            <div class="logo">Força & Ordem</div>
            <div class="accessibility-controls">
                <button onclick="changeFontSize('increase')" aria-label="Aumentar fonte">A+</button>
                <button onclick="changeFontSize('decrease')" aria-label="Diminuir fonte">A-</button>
                <button id="contrast-toggle" aria-label="Alternar alto contraste">🌓</button>
            </div>
        </nav>
    </header>

    <main>
        <section id="hero" class="reveal">
            <div class="container">
                <h1>Servir e Proteger</h1>
                <p>Compromisso com a segurança pública e o bem-estar social.</p>
                <a href="#servicos" class="btn">Conheça nosso trabalho</a>
            </div>
        </section>

        <section id="servicos" class="container reveal">
            <h2>Nossas Atuações</h2>
            <div id="services-grid" class="grid-layout">
                </div>
        </section>

        <section id="faq" class="container reveal">
            <h2>Dúvidas Frequentes</h2>
            <div id="accordion-container">
                </div>
        </section>
    </main>

    <footer class="container">
        <p>&copy; 2026 Portal de Segurança Pública. Conteúdo informativo.</p>
    </footer>

    <script src="script.js"></script>
</body>/* --- DESIGN SYSTEM & VARIABLES --- */
:root {
    --primary-color: #1a2a6c;
    --secondary-color: #b21f1f;
    --text-color: #333;
    --bg-color: #f4f4f4;
    --white: #ffffff;
    --radius: 8px;
    --transition: 0.3s ease-in-out;
    --font-base: 16px;
}

/* --- ALTO CONTRASTE --- */
body.high-contrast {
    --primary-color: #ffff00;
    --secondary-color: #ffff00;
    --bg-color: #000000;
    --text-color: #ffffff;
    --white: #000000;
}

* { margin: 0; padding: 0; box-sizing: border-box; }

body {
    font-size: var(--font-base);
    font-family: 'Segoe UI', Tahoma, sans-serif;
    background-color: var(--bg-color);
    color: var(--text-color);
    line-height: 1.6;
    transition: background 0.3s, color 0.3s;
}

/* --- LAYOUT --- */
.container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 2rem;
}

.grid-layout {
    display: grid;
    gap: 1.5rem;
    /* Mobile: 1 coluna */
    grid-template-columns: 1fr;
}

/* Desktop: 3 colunas */
@media (min-width: 768px) {
    .grid-layout {
        grid-template-columns: repeat(3, 1fr);
    }
}

/* --- COMPONENTES --- */
header {
    background: var(--primary-color);
    color: white;
    padding: 1rem 0;
    position: sticky;
    top: 0;
    z-index: 100;
}

.card {
    background: var(--white);
    padding: 1.5rem;
    border-radius: var(--radius);
    border-bottom: 4px solid var(--primary-color);
    box-shadow: 0 4px 6px rgba(0,0,0,0.1);
}

/* --- ANIMAÇÃO DE SCROLL --- */
.reveal {
    opacity: 0;
    transform: translateY(30px);
    transition: all 0.8s ease-out;
}
/* --- GESTÃO DE DADOS --- */
const servicosData = [
    { titulo: "Ronda Ostensiva", desc: "Prevenção e patrulhamento urbano constante." },
    { titulo: "Investigação", desc: "Inteligência aplicada à resolução de crimes complexos." },
    { titulo: "Apoio Comunitário", desc: "Projetos sociais e integração com a vizinhança." }
];

/* --- RENDERIZAÇÃO DINÂMICA --- */
function renderContent() {
    const grid = document.getElementById('services-grid');
    
    servicosData.forEach(item => {
        const card = document.createElement('article');
        card.className = 'card';
        card.innerHTML = `
            <h3>${item.titulo}</h3>
            <p>${item.desc}</p>
        `;
        grid.appendChild(card);
    });
}

/* --- ACESSIBILIDADE: FONTE --- */
let currentFontSize = 16;
function changeFontSize(action) {
    const body = document.body;
    if(action === 'increase') currentFontSize += 2;
    else currentFontSize -= 2;
    
    body.style.fontSize = currentFontSize + 'px';
}

/* --- ACESSIBILIDADE: CONTRASTE --- */
document.getElementById('contrast-toggle').addEventListener('click', () => {
    document.body.classList.toggle('high-contrast');
});

/* --- SCROLL REVEAL LOGIC --- */
const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
        if (entry.isIntersecting) {
            entry.target.classList.add('active');
        }
    });
}, { threshold: 0.1 });

/* --- INICIALIZAÇÃO --- */
document.addEventListener('DOMContentLoaded', () => {
    renderContent();
    document.querySelectorAll('.reveal').forEach(el => observer.observe(el));
});
.reveal.active {
    opacity: 1;
    transform: translateY(0);
}

</html>
