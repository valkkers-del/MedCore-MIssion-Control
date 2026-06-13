<div align="center">

# 🏥 MedCore Mission Control

**PWA de despacho médico com dupla função — Central de comando hospitalar e unidade de campo para motoristas, com alertas em tempo real, transferência de arquivos, roteamento por mapa ao vivo e decisões clínicas por IA. Desenvolvido como um único arquivo HTML, funciona offline.**

<br/>

[![Demo](https://img.shields.io/badge/▶%20LIVE%20DEMO-00e5ff?style=for-the-badge&logoColor=black)](https://valkkers-del.github.io/medcore-mission-control)
[![PWA](https://img.shields.io/badge/PWA-OFFLINE%20READY-00ff9d?style=for-the-badge)](https://github.com/valkkers-del)
[![Zero Deps](https://img.shields.io/badge/DEPENDENCIES-ZERO-ffb800?style=for-the-badge)](https://github.com/valkkers-del)
[![Single File](https://img.shields.io/badge/BUILD-SINGLE%20HTML-bf5fff?style=for-the-badge)](https://github.com/valkkers-del)

<br/>

> 🛡 **VLS Systems®** | Developed by **Valquíria Lemes**
> *Healthcare · Logistics · Mission-critical PWAs*

</div>

---

## 📸 Visão Geral

MedCore Mission Control é um sistema operacional hospitalar simulado em tempo real, construído inteiramente como **um único arquivo `index.html`** — sem frameworks, sem bibliotecas externas, sem servidor. Abre e funciona.

O sistema conecta **três perfis de usuário** que operam simultaneamente no mesmo arquivo, comunicando-se via `localStorage` como um barramento de mensagens em tempo real:

```
🏥 Hospital  ←──── 💬 Comms Bus ────→  🚑 Driver
     ↕                                      ↕
🩺 Clinic   ←──── 💬 Comms Bus ────→  🏥 Hospital
```

---

## 🚀 Funcionalidades

### 👥 Três Perfis de Acesso

| Perfil | Acesso | Cor |
|--------|--------|-----|
| 🏥 **Hospital** | Comando total — despacho, monitoramento, IA, arquivos | Ciano |
| 🚑 **Driver** | Campo — recebe chamadas, navega, atualiza missão | Âmbar |
| 🩺 **Clinic** | Envia arquivos de pacientes, solicita transporte | Verde |

---

### ⚡ Sistema de Alertas Críticos
- Níveis **LOW / MEDIUM / HIGH / CRITICAL** com animação flash e glow vermelho
- Alertas surgem e expiram automaticamente em tempo real
- **Alertas de voz** via Web Speech API — fala o alerta crítico em voz alta
- Trilíngue: EN / PT-BR / ES com troca instantânea

### 🚨 Despacho de Chamadas — Estilo Uber
- Overlay de chamada recebida com **endereço completo do paciente**
- Fluxo completo: `PENDING → ACCEPTED → EN ROUTE → ON SCENE → COMPLETE`
- Barra de progresso animada durante o trajeto
- Status do motorista atualizado em tempo real para o hospital

### 💬 Comunicação Bidirecional
- Chat em tempo real entre **Hospital ↔ Driver ↔ Clinic**
- Persistência via `localStorage` — mensagens sobrevivem ao reload
- Badge de mensagens não lidas nas abas
- Enviado por qualquer perfil, recebido imediatamente pelo outro

### 📎 Transferência de Arquivos — Todos os Formatos
Suporta qualquer tipo de arquivo com ícone automático por extensão:

| Categoria | Formatos |
|-----------|----------|
| 🩻 Médico | `.dcm` (DICOM), `.ecg`, exames, laudos |
| 📄 Documentos | `.pdf`, `.doc`, `.docx`, `.txt` |
| 📊 Dados | `.xls`, `.xlsx`, `.csv`, `.json` |
| 🖼 Imagens | `.jpg`, `.png`, `.gif`, `.webp`, `.svg` |
| 🎬 Vídeo | `.mp4`, `.mov`, `.avi` |
| 🎵 Áudio | `.mp3`, `.wav` |
| 🗜 Arquivos | `.zip`, `.rar`, `.7z` |
| 💻 Código | `.html`, `.js`, `.py` |

O arquivo é lido via `FileReader` como base64 e armazenado para download real pelo destinatário.

### 🗺 Mapa ao Vivo — Canvas 2D (Zero Dependência)
- Malha viária de **Miami, FL** desenhada em coordenadas geográficas reais
- Biscayne Bay renderizada como polígono de água
- **Ambulâncias se movem suavemente** em tempo real com trilha tracejada
- **Modo Driver**: rota animada com curva Bézier do ponto atual ao destino
- Posição do veículo avança proporcionalmente ao progresso da missão
- Badge **● ONLINE / ○ OFFLINE** em tempo real via `navigator.onLine`
- Bússola N↑ e escala de distância no canvas

### ❤️ Monitor de Sinais Vitais
- **FC, PA, SpO₂, Temperatura** atualizados a cada 300ms
- Valores fora do range ficam vermelhos automaticamente (taquicardia, hipóxia)
- **ECG animado** desenhado em canvas com forma de onda QRS realista
- Disponível para o driver acompanhar o paciente durante o transporte

### 🧠 Motor de Decisão Clínica IA
- Cards de decisão com **tipo, ação recomendada, raciocínio clínico e % de confiança**
- Novos cards aparecem com animação e expiram automaticamente
- Dados clínicos reais: `HR 118 · BP 88/54 · Lactate 4.2`, `qSOFA 2`, `NIHSS 14`
- Trilíngue completo

### 📊 Capacidade Hospitalar
- **UTI / Emergência / Cirurgia / Internação** com ocupação variando em tempo real
- Barras coloridas por threshold: verde → ciano → âmbar → vermelho
- Atualização suave com CSS `transition`

### ⚙ Painel Logístico
- **Eficiência, Tempo de Resposta, Throughput, Recursos** com sparklines
- Métricas oscinam continuamente — nunca estático

### ☰ Menu de Navegação Overlay
- Menu fullscreen com **glassmorphism** (`backdrop-filter: blur(22px)`)
- Botões grandes com ícone, nome e descrição de cada aba
- Estado **ACTIVE** destacado com cor do perfil atual
- Fecha por clique no backdrop, botão ✕ ou tecla `Escape`
- Stagger animation escalonado por índice

### 📋 Logs de Missão
- Registro automático de cada ação: aceitar, partir, chegar, entregar, concluir
- Timestamp em cada entrada
- Persiste entre sessões via `localStorage`

---

## 🛠 Stack Técnica

```
Linguagem       Vanilla JavaScript ES6+ (sem frameworks)
Renderização    HTML5 + CSS3 (Glassmorphism, CSS Custom Properties)
Mapa            Canvas 2D API (geometria geográfica real, zero tiles)
ECG             Canvas 2D API (forma de onda QRS sintética)
Voz             Web Speech API (SpeechSynthesisUtterance)
Persistência    localStorage (barramento de mensagens + logs + status)
Arquivos        FileReader API (base64, download real)
PWA             offline-ready, installable via Add to Home Screen
Fontes          Google Fonts (Exo 2 · Share Tech Mono · DM Sans)
```

**Sem `npm install`. Sem build. Sem servidor. Sem CDN de lógica.**

---

## 📱 Instalação como PWA

### iOS (iPhone / iPad)
1. Abrir `index.html` no **Safari**
2. Tocar em **Compartilhar** → **Adicionar à Tela de Início**
3. O app abre em tela cheia, sem barra do browser

### Android
1. Abrir no **Chrome**
2. Menu → **Adicionar à tela inicial**
3. Funciona como app nativo

### Desktop
Abrir `index.html` diretamente no browser — funciona sem servidor.

---

## 🗂 Arquitetura Interna

O código de um único arquivo é organizado em módulos lógicos via objetos JavaScript:

```
index.html
│
├── /state          Objeto S — store de dados da simulação ao vivo
│
├── /i18n           Objeto T — strings EN / PT-BR / ES
│
├── /engine         Motor de simulação
│   ├── initEngine()     — inicializa todos os dados
│   ├── tickEngine()     — atualiza a cada 300ms
│   ├── spawnAlert()     — gera alertas aleatórios
│   ├── spawnAI()        — gera decisões clínicas
│   └── spawnDispatch()  — gera ordens de despacho
│
├── /comms          Barramento localStorage
│   ├── Bus.push()       — envia mensagem (qualquer perfil)
│   ├── Bus.markRead()   — marca lidas
│   ├── Bus.addLog()     — registra log de missão
│   └── Bus.setDrv()     — atualiza status do motorista
│
├── /map            Renderizador Canvas 2D
│   ├── mapInit()        — dimensiona o canvas
│   └── mapDraw()        — renderiza frame completo + rota
│
├── /ecg            Gerador de onda ECG
│   └── ecgDraw()        — forma QRS sintética animada
│
├── /views          Construtores de views (retornam HTML string)
│   ├── VIEWS.h0–h5      — Hospital: 6 abas
│   ├── VIEWS.d0–d4      — Driver: 5 abas
│   └── VIEWS.c0–c3      — Clinic: 4 abas
│
└── /ui             Camada de renderização
    ├── renderTab()      — renderização completa da aba atual
    └── partialUpdate()  — atualizações parciais (sem re-render total)
```

---

## 🎨 Sistema de Design

```
Paleta
  Ciano   #00e5ff  — Hospital / comandos primários
  Verde   #00ff9d  — Confirmações / Clinic / online
  Âmbar   #ffb800  — Driver / alertas de atenção
  Vermelho #ff2d55 — Crítico / emergência
  Roxo    #bf5fff  — IA / decisões

Tipografia
  Exo 2           — Display, títulos, valores numéricos
  Share Tech Mono — Dados, timestamps, labels, código
  DM Sans         — Corpo, mensagens, descrições

Efeitos
  backdrop-filter: blur(22px)  — Glassmorphism em painéis e overlay
  Canvas 2D                     — Mapa, ECG, sparklines
  CSS animations                — Flash crítico, pulse, slide-in, stagger
  CSS transitions               — Barras de capacidade, progresso de missão
```

---

## ▶ Como Usar

```bash
# 1. Clonar
git clone https://github.com/valkkers-del/medcore-mission-control

# 2. Abrir — é só isso
open index.html
```

**Para testar a comunicação bidirecional:**
1. Abrir `index.html` em **duas abas** do mesmo browser
2. Aba 1 → selecionar **Hospital**
3. Aba 2 → selecionar **Driver**
4. Enviar mensagens e arquivos entre as abas — chegam em tempo real

---

## 🏥 Caso de Uso Real

Desenvolvido como simulação de workflow para **grupos de ortopedia e clínicas ambulatoriais**:

- Hospital despacha ambulância com dados do paciente e endereço completo
- Motorista recebe overlay estilo Uber, aceita e navega pelo mapa
- Arquivos clínicos (Raio-X, laudos, formulários de transferência) enviados em tempo real
- Hospital monitora capacidade, logística e decisões de triagem da IA
- Todos os perfis compartilham o mesmo arquivo único — distribuído via link ou WhatsApp

---

## 📄 Licença

MIT — livre para usar, modificar e distribuir com atribuição.

---

<div align="center">

**🛡 VLS Systems® | Developed by Valquíria Lemes**

[![GitHub](https://img.shields.io/badge/GitHub-valkkers--del-00e5ff?style=flat-square&logo=github&logoColor=white)](https://github.com/valkkers-del)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Valquíria%20Lemes-0077b5?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/valqu%C3%ADria-lemes)

*Patient Care Representative · Self-taught Developer · PWA Specialist*
*Miami, FL — available for freelance on Workana & Upwork*

</div>
