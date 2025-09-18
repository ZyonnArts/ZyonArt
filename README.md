<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Zyon Arts - Transformando Ideias em Arte Digital</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
    <!-- Chosen Palette: Modern & Creative Dark -->
    <!-- Application Structure Plan: A single-page, linear landing page designed for conversion. The structure guides the user from awareness (Hero) to consideration (Services, Portfolio) and finally to action (Contact Form). This top-to-bottom flow is proven for lead generation, minimizing distractions and focusing the user on the primary goal: making contact via WhatsApp. Key interaction is the smooth scroll from CTA buttons to the form, keeping the user engaged in a single context. -->
    <!-- Visualization & Content Choices: Report Info: 'Zyon Arts needs WhatsApp opt-ins'. Goal: Persuade and Convert. Presentation: Used sections for Hero, Services, Portfolio, Testimonials, and a final CTA form. Interaction: CTA buttons use vanilla JS for smooth scrolling to the form. The form submission opens a pre-filled WhatsApp chat, which is the most direct way to get an 'opt-in' and start a conversation. Justification: This approach is direct, visually engaging with a portfolio section, and builds trust through testimonials, leading to higher conversion rates for a creative agency. Method: HTML/Tailwind for structure, Vanilla JS for interactions. -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #111827;
            color: #F3F4F6;
        }
        .hero-bg {
            background: linear-gradient(rgba(17, 24, 39, 0.8), rgba(17, 24, 39, 0.8)), url('https://placehold.co/1920x1080/1a1a2e/e0e0e0?text=Arte+Abstrata') center center/cover no-repeat;
        }
        .cta-button {
            transition: all 0.3s ease;
        }
        .cta-button:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 20px rgba(251, 191, 36, 0.3);
        }
        .card {
            background-color: #1F2937;
            border: 1px solid #374151;
        }
        .portfolio-img {
            transition: transform 0.3s ease;
        }
        .portfolio-img:hover {
            transform: scale(1.05);
        }
        .modal-overlay {
            transition: opacity 0.3s ease-in-out;
        }
        .modal-content {
            transition: transform 0.3s ease-in-out, opacity 0.3s ease-in-out;
        }
        .loader {
            border: 4px solid #f3f3f3;
            border-top: 4px solid #f59e0b;
            border-radius: 50%;
            width: 32px;
            height: 32px;
            animation: spin 1s linear infinite;
        }
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
    </style>
</head>
<body class="antialiased">

    <header class="bg-gray-900/80 backdrop-blur-sm fixed top-0 left-0 right-0 z-50">
        <div class="container mx-auto px-6 py-3 flex justify-between items-center">
            <a href="#hero">
                <img src="data:image/jpeg;base64,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" alt="Zyon Arts Logo" class="h-12 w-auto">
            </a>
            <nav>
                <a href="#services" class="text-gray-300 hover:text-amber-400 mx-3">Serviços</a>
                <a href="#portfolio" class="text-gray-300 hover:text-amber-400 mx-3">Portfolio</a>
                <a href="#contact" class="bg-amber-500 text-gray-900 font-bold py-2 px-4 rounded-full hover:bg-amber-400 cta-button">Fale Conosco</a>
            </nav>
        </div>
    </header>

    <main>
        <section id="hero" class="hero-bg min-h-screen flex items-center">
            <div class="container mx-auto px-6 text-center">
                <h2 class="text-4xl md:text-6xl font-bold text-white leading-tight mb-4">Transformando Ideias em <br> <span class="text-amber-400">Arte Digital Inesquecível</span></h2>
                <p class="text-lg md:text-xl text-gray-300 max-w-3xl mx-auto mb-8">Criamos designs impactantes e experiências digitais que elevam sua marca e conectam você ao seu público.</p>
                <a href="#contact" class="bg-amber-500 text-gray-900 font-bold py-3 px-8 rounded-full text-lg hover:bg-amber-400 cta-button">Quero um Orçamento Gratuito</a>
            </div>
        </section>

        <section id="services" class="py-20">
            <div class="container mx-auto px-6">
                <div class="text-center mb-12">
                    <h3 class="text-3xl font-bold text-white">Nossos Serviços</h3>
                    <p class="text-gray-400 mt-2">Oferecemos soluções criativas para impulsionar o seu negócio.</p>
                </div>
                <div class="grid md:grid-cols-3 gap-8">
                    <div class="card p-8 rounded-lg text-center">
                        <div class="text-amber-400 mb-4">
                            <span class="text-5xl">🎨</span>
                        </div>
                        <h4 class="text-xl font-bold text-white mb-2">Design Gráfico</h4>
                        <p class="text-gray-400">Criação de logos, identidade visual e materiais de marketing que capturam a essência da sua marca.</p>
                    </div>
                    <div class="card p-8 rounded-lg text-center">
                        <div class="text-amber-400 mb-4">
                            <span class="text-5xl">📱</span>
                        </div>
                        <h4 class="text-xl font-bold text-white mb-2">UI/UX Design</h4>
                        <p class="text-gray-400">Desenvolvemos interfaces intuitivas e experiências de usuário memoráveis para sites e aplicativos.</p>
                    </div>
                    <div class="card p-8 rounded-lg text-center">
                        <div class="text-amber-400 mb-4">
                            <span class="text-5xl">💡</span>
                        </div>
                        <h4 class="text-xl font-bold text-white mb-2">Branding Estratégico</h4>
                        <p class="text-gray-400">Construímos marcas fortes e coerentes que se destacam no mercado e criam conexões duradouras.</p>
                    </div>
                </div>
            </div>
        </section>

        <section id="portfolio" class="py-20 bg-gray-900">
            <div class="container mx-auto px-6">
                <div class="text-center mb-12">
                    <h3 class="text-3xl font-bold text-white">Nosso Portfolio</h3>
                    <p class="text-gray-400 mt-2">Veja alguns dos projetos que tivemos o prazer de criar.</p>
                </div>
                <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
                    <div class="card rounded-lg overflow-hidden group">
                        <img src="https://placehold.co/600x400/1a1a2e/e0e0e0?text=Projeto+Alpha" alt="Projeto Alpha" class="w-full h-64 object-cover portfolio-img">
                        <div class="p-6">
                            <h4 class="text-xl font-bold text-white">Marca Alpha</h4>
                            <p class="text-gray-400">Identidade Visual</p>
                        </div>
                    </div>
                    <div class="card rounded-lg overflow-hidden group">
                        <img src="https://placehold.co/600x400/3d3d5c/e0e0e0?text=Projeto+Beta" alt="Projeto Beta" class="w-full h-64 object-cover portfolio-img">
                        <div class="p-6">
                            <h4 class="text-xl font-bold text-white">App Beta</h4>
                            <p class="text-gray-400">UI/UX Design</p>
                        </div>
                    </div>
                    <div class="card rounded-lg overflow-hidden group">
                        <img src="https://placehold.co/600x400/5a5a8a/e0e0e0?text=Projeto+Gamma" alt="Projeto Gamma" class="w-full h-64 object-cover portfolio-img">
                        <div class="p-6">
                            <h4 class="text-xl font-bold text-white">Campanha Gamma</h4>
                            <p class="text-gray-400">Marketing Digital</p>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <section id="social-proof" class="py-20">
            <div class="container mx-auto px-6">
                <div class="text-center mb-12">
                    <h3 class="text-3xl font-bold text-white">Resultados Reais, Impacto Visível</h3>
                    <p class="text-gray-400 mt-2">Veja como nossas criações ganham vida e geram valor para os nossos clientes.</p>
                </div>
                <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
                    <div class="card rounded-lg overflow-hidden">
                        <img src="https://placehold.co/600x450/1a1a2e/e0e0e0?text=Logo+em+Fachada" alt="Logo em fachada de loja" class="w-full h-auto object-cover">
                        <div class="p-4 bg-gray-800">
                            <p class="text-white font-semibold">Identidade visual aplicada para a <span class="text-amber-400">Cafeteria Aurora</span>.</p>
                        </div>
                    </div>
                    <div class="card rounded-lg overflow-hidden">
                        <img src="https://placehold.co/600x450/3d3d5c/e0e0e0?text=App+em+Uso" alt="Aplicativo sendo usado em um celular" class="w-full h-auto object-cover">
                        <div class="p-4 bg-gray-800">
                             <p class="text-white font-semibold">Interface do <span class="text-amber-400">App Beta</span> em pleno funcionamento.</p>
                        </div>
                    </div>
                    <div class="card rounded-lg overflow-hidden">
                        <img src="https://placehold.co/600x450/5a5a8a/e0e0e0?text=Post+em+Rede+Social" alt="Post de rede social em um feed" class="w-full h-auto object-cover">
                        <div class="p-4 bg-gray-800">
                            <p class="text-white font-semibold">Campanha de engajamento para <span class="text-amber-400">Social Media Zeta</span>.</p>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <section id="testimonials" class="py-20">
            <div class="container mx-auto px-6">
                 <div class="text-center mb-12">
                    <h3 class="text-3xl font-bold text-white">O Que Nossos Clientes Dizem</h3>
                    <p class="text-gray-400 mt-2">A satisfação de quem confia em nosso trabalho é nossa maior conquista.</p>
                </div>
                <div class="grid md:grid-cols-2 gap-8 max-w-4xl mx-auto">
                    <div class="card p-8 rounded-lg">
                        <p class="text-gray-300 italic mb-4">"A Zyon Arts revolucionou nossa presença online. O novo design é incrível e o feedback dos nossos clientes tem sido extremamente positivo. Profissionalismo e talento definem a equipe."</p>
                        <p class="font-bold text-white">- João Silva</p>
                        <p class="text-amber-400 text-sm">CEO, Tech Solutions</p>
                    </div>
                    <div class="card p-8 rounded-lg">
                        <p class="text-gray-300 italic mb-4">"O processo de criação da nossa nova identidade visual foi impecável. A Zyon Arts entendeu perfeitamente nossa visão e a traduziu em um design que superou todas as expectativas."</p>
                        <p class="font-bold text-white">- Maria Oliveira</p>
                        <p class="text-amber-400 text-sm">Fundadora, Café Aurora</p>
                    </div>
                </div>
            </div>
        </section>

        <section id="contact" class="py-20 bg-gray-900">
            <div class="container mx-auto px-6">
                <div class="max-w-3xl mx-auto text-center mb-8">
                     <h3 class="text-3xl font-bold text-white">Vamos Criar Algo Incrível Juntos?</h3>
                    <p class="text-gray-400 mt-2">Preencha o formulário abaixo ou use nosso assistente de IA para nos ajudar a entender sua visão.</p>
                     <button id="open-brief-assistant" class="mt-4 bg-transparent border border-amber-500 text-amber-500 font-bold py-2 px-6 rounded-full hover:bg-amber-500 hover:text-gray-900 transition-colors duration-300">
                        ✨ Usar Assistente de Briefing Criativo
                    </button>
                </div>

                <div class="card max-w-3xl mx-auto p-8 md:p-12 rounded-lg">
                    <form id="contact-form" class="space-y-4">
                        <div>
                            <input type="text" id="name" name="name" placeholder="Seu nome" class="w-full bg-gray-700 border border-gray-600 rounded-md py-3 px-4 text-white focus:outline-none focus:ring-2 focus:ring-amber-500" required>
                        </div>
                        <div>
                            <input type="tel" id="whatsapp" name="whatsapp" placeholder="Seu número de WhatsApp (com DDD)" class="w-full bg-gray-700 border border-gray-600 rounded-md py-3 px-4 text-white focus:outline-none focus:ring-2 focus:ring-amber-500" required>
                        </div>
                        <div>
                            <textarea id="idea" name="idea" placeholder="Descreva sua ideia ou cole o briefing gerado aqui..." rows="4" class="w-full bg-gray-700 border border-gray-600 rounded-md py-3 px-4 text-white focus:outline-none focus:ring-2 focus:ring-amber-500"></textarea>
                        </div>
                        <button type="submit" class="w-full bg-amber-500 text-gray-900 font-bold py-3 px-8 rounded-full text-lg hover:bg-amber-400 cta-button">
                            Entrar em Contato via WhatsApp
                        </button>
                    </form>
                    <p id="success-message" class="text-green-400 mt-4 hidden text-center">Ótimo! Redirecionando para o WhatsApp...</p>
                </div>
            </div>
        </section>
    </main>

    <footer class="bg-gray-900 border-t border-gray-800 py-6">
        <div class="container mx-auto px-6 text-center text-gray-400">
            <p>&copy; 2025 Zyon Arts. Todos os direitos reservados.</p>
        </div>
    </footer>

    <!-- Gemini AI Brief Assistant Modal -->
    <div id="brief-modal" class="fixed inset-0 z-50 flex items-center justify-center hidden">
        <div id="modal-overlay" class="absolute inset-0 bg-black bg-opacity-70 modal-overlay"></div>
        <div id="modal-content" class="card w-full max-w-2xl mx-4 p-8 rounded-lg z-10 transform scale-95 opacity-0 modal-content">
            <div class="flex justify-between items-center mb-4">
                <h4 class="text-2xl font-bold text-white">Assistente de Briefing Criativo ✨</h4>
                <button id="close-modal" class="text-gray-400 hover:text-white text-3xl">&times;</button>
            </div>
            <p class="text-gray-400 mb-6">Responda a estas perguntas e nossa IA irá gerar um rascunho de briefing para o seu projeto.</p>
            <div class="space-y-4">
                <input type="text" id="projectName" placeholder="Nome do seu projeto ou empresa" class="w-full bg-gray-700 border border-gray-600 rounded-md py-3 px-4 text-white focus:outline-none focus:ring-2 focus:ring-amber-500">
                <input type="text" id="targetAudience" placeholder="Quem é o seu público-alvo?" class="w-full bg-gray-700 border border-gray-600 rounded-md py-3 px-4 text-white focus:outline-none focus:ring-2 focus:ring-amber-500">
                <input type="text" id="projectStyle" placeholder="Estilo desejado (ex: moderno, rústico, divertido)" class="w-full bg-gray-700 border border-gray-600 rounded-md py-3 px-4 text-white focus:outline-none focus:ring-2 focus:ring-amber-500">
                <button id="generate-brief" class="w-full bg-amber-500 text-gray-900 font-bold py-3 rounded-md hover:bg-amber-400 cta-button flex items-center justify-center">
                    <span id="generate-brief-text">Gerar Briefing</span>
                    <div id="loader" class="loader hidden ml-3"></div>
                </button>
            </div>
            <div id="brief-result-container" class="mt-6 hidden">
                <h5 class="font-semibold text-white mb-2">Rascunho do Briefing Gerado:</h5>
                <textarea id="brief-result" rows="8" class="w-full bg-gray-800 border border-gray-600 rounded-md p-4 text-gray-300" readonly></textarea>
                <button id="copy-brief" class="mt-4 w-full bg-gray-600 text-white font-bold py-2 px-4 rounded-md hover:bg-gray-500 transition-colors">Copiar e Usar no Contato</button>
            </div>
             <p id="gemini-error" class="text-red-400 mt-4 text-center hidden">Ocorreu um erro ao gerar o briefing. Por favor, tente novamente.</p>
        </div>
    </div>


    <script>
        document.addEventListener('DOMContentLoaded', () => {
            document.querySelectorAll('a[href^="#"]').forEach(anchor => {
                anchor.addEventListener('click', function (e) {
                    e.preventDefault();
                    const targetId = this.getAttribute('href');
                    const targetElement = document.querySelector(targetId);
                    if (targetElement) {
                        targetElement.scrollIntoView({
                            behavior: 'smooth'
                        });
                    }
                });
            });

            const contactForm = document.getElementById('contact-form');
            const successMessage = document.getElementById('success-message');

            if (contactForm) {
                contactForm.addEventListener('submit', function(e) {
                    e.preventDefault();
                    const name = document.getElementById('name').value;
                    const idea = document.getElementById('idea').value;
                    
                    const businessPhoneNumber = '5567981383966'; 
                    let message = `Olá! Meu nome é ${name}. Tenho interesse nos serviços da Zyon Arts e gostaria de um orçamento.`;
                    if (idea) {
                        message += `\n\nResumo da minha ideia:\n${idea}`;
                    }
                    const whatsappUrl = `https://wa.me/${businessPhoneNumber}?text=${encodeURIComponent(message)}`;

                    if(successMessage) {
                        successMessage.classList.remove('hidden');
                    }
                    
                    setTimeout(() => {
                        window.open(whatsappUrl, '_blank');
                        contactForm.reset();
                        if(successMessage) {
                            successMessage.classList.add('hidden');
                        }
                    }, 1500);
                });
            }

            // Gemini AI Brief Assistant Logic
            const modal = document.getElementById('brief-modal');
            const overlay = document.getElementById('modal-overlay');
            const content = document.getElementById('modal-content');
            const openBtn = document.getElementById('open-brief-assistant');
            const closeBtn = document.getElementById('close-modal');
            const generateBtn = document.getElementById('generate-brief');
            const copyBtn = document.getElementById('copy-brief');
            const resultContainer = document.getElementById('brief-result-container');
            const resultTextarea = document.getElementById('brief-result');
            const ideaTextarea = document.getElementById('idea');
            const loader = document.getElementById('loader');
            const generateBtnText = document.getElementById('generate-brief-text');
            const geminiError = document.getElementById('gemini-error');

            const openModal = () => {
                modal.classList.remove('hidden');
                setTimeout(() => {
                    overlay.classList.remove('opacity-0');
                    content.classList.remove('scale-95', 'opacity-0');
                }, 10);
            };

            const closeModal = () => {
                overlay.classList.add('opacity-0');
                content.classList.add('scale-95', 'opacity-0');
                setTimeout(() => {
                    modal.classList.add('hidden');
                }, 300);
            };

            openBtn.addEventListener('click', openModal);
            closeBtn.addEventListener('click', closeModal);
            overlay.addEventListener('click', closeModal);
            
            generateBtn.addEventListener('click', async () => {
                const projectName = document.getElementById('projectName').value;
                const targetAudience = document.getElementById('targetAudience').value;
                const projectStyle = document.getElementById('projectStyle').value;

                if (!projectName || !targetAudience || !projectStyle) {
                    alert('Por favor, preencha todos os campos para gerar o briefing.');
                    return;
                }
                
                loader.classList.remove('hidden');
                generateBtnText.textContent = 'Gerando...';
                generateBtn.disabled = true;
                geminiError.classList.add('hidden');
                resultContainer.classList.add('hidden');

                const systemPrompt = `Aja como um diretor de criação experiente. Com base nas informações a seguir, escreva um breve briefing de design, conciso e bem estruturado em português. O briefing deve ser inspirador e claro, servindo como um excelente ponto de partida para um designer. Organize-o em seções curtas com títulos em negrito: '**Visão do Projeto**', '**Público-Alvo**' e '**Direção Criativa**'.`;
                const userQuery = `Nome do Projeto: ${projectName}\nPúblico-Alvo: ${targetAudience}\nEstilo Desejado: ${projectStyle}`;

                const apiKey = "";
                const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-05-20:generateContent?key=${apiKey}`;
                
                const payload = {
                    contents: [{ parts: [{ text: userQuery }] }],
                    systemInstruction: { parts: [{ text: systemPrompt }] },
                };

                try {
                    let response;
                    let retries = 3;
                    let delay = 1000;
                    for (let i = 0; i < retries; i++) {
                        response = await fetch(apiUrl, {
                            method: 'POST',
                            headers: { 'Content-Type': 'application/json' },
                            body: JSON.stringify(payload)
                        });
                        if (response.ok) break;
                        await new Promise(res => setTimeout(res, delay));
                        delay *= 2; 
                    }

                    if (!response.ok) {
                        throw new Error('A resposta da API não foi bem-sucedida.');
                    }
                    
                    const result = await response.json();
                    const text = result.candidates?.[0]?.content?.parts?.[0]?.text;

                    if (text) {
                        resultTextarea.value = text;
                        resultContainer.classList.remove('hidden');
                    } else {
                         throw new Error('Nenhum conteúdo gerado.');
                    }
                } catch (error) {
                    geminiError.classList.remove('hidden');
                } finally {
                    loader.classList.add('hidden');
                    generateBtnText.textContent = 'Gerar Briefing';
                    generateBtn.disabled = false;
                }
            });

            copyBtn.addEventListener('click', () => {
                resultTextarea.select();
                document.execCommand('copy');
                ideaTextarea.value = resultTextarea.value;
                closeModal();
                ideaTextarea.focus();
            });
        });
    </script>

</body>
</html>

