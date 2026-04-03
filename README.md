# 🔬 QuizLab — Avaliação Diagnóstica Interativa

App de quiz para avaliações práticas em citopatologia, hematologia, parasitologia e outras disciplinas laboratoriais. Funciona 100% no navegador, sem necessidade de servidor.

---

## ✨ Funcionalidades

- **Quiz com mídia** — cada questão pode ter uma imagem ou vídeo
- **5 alternativas** por questão com feedback visual imediato
- **Score inteligente** — pontuação por velocidade de resposta (acerto rápido = mais pontos)
- **Coluna de acertos simples** — separada do score de velocidade
- **Anti-cola** — modo tela cheia, bloqueio de Alt+Tab, aba oculta e foco perdido
- **Envio automático** ao Google Sheets via Apps Script
- **Exportação CSV** dos resultados locais
- **Painel do professor** protegido por senha
- **Questões persistentes** no navegador (localStorage)
- **Funciona offline** após carregamento inicial

---

## 🚀 Como usar no GitHub Pages

1. Faça um fork ou clone este repositório
2. Vá em **Settings → Pages → Source: main branch / root**
3. Acesse via `https://seu-usuario.github.io/nome-do-repo`

---

## 👨‍🏫 Área do Professor

- Clique em **"⚙ Área do Professor"** na tela inicial
- Senha: configurada no código (`TEACHER_PASS`)
- No painel você pode:
  - Adicionar, editar e excluir questões
  - Configurar o tempo por questão
  - Colar a URL do Google Apps Script
  - Visualizar resultados locais
  - Exportar CSV

---

## 📊 Integração com Google Sheets

### Passo 1 — Criar a planilha

Crie uma planilha no Google Sheets com as seguintes colunas na linha 1:

| Timestamp | Nome | Turma | Acertos | Total | Aproveitamento% | Score |
|-----------|------|-------|---------|-------|-----------------|-------|

### Passo 2 — Apps Script

1. Abra a planilha → **Extensões → Apps Script**
2. Cole o código do arquivo `apps-script.js` deste repositório
3. Salve

### Passo 3 — Publicar como Web App

1. Clique em **Implantar → Nova implantação**
2. Tipo: **App da Web**
3. Executar como: **Eu (seu e-mail)**
4. Quem tem acesso: **Qualquer pessoa**
5. Clique em **Implantar** e autorize

### Passo 4 — Configurar no app

1. Copie a URL gerada (começa com `https://script.google.com/macros/s/...`)
2. No painel do professor → cole no campo **URL do Google Apps Script**
3. Salve as configurações

---

## 🎯 Cálculo do Score

```
Score por questão = 100 pontos (acerto) + bônus de velocidade
Bônus velocidade  = (1 - tempo_usado / tempo_limite) × 50
Score total       = soma de todos os pontos
```

- Resposta correta instantânea: **150 pontos**
- Resposta correta no limite: **100 pontos**
- Resposta errada ou sem resposta: **0 pontos**

---

## 🔒 Anti-Cola

| Evento | Ação |
|--------|------|
| Sair da aba (visibilitychange) | Lockout de 5 segundos |
| Perder foco (blur) | Lockout de 5 segundos |
| Sair do fullscreen | Reativação forçada |
| Menu de contexto (botão direito) | Bloqueado |
| Ctrl+C, Ctrl+U, F12 | Bloqueados |
| Alt+Tab | Bloqueado |

Violações são contadas e enviadas junto com o resultado.

---

## 📁 Estrutura

```
/
├── index.html       # App completo (single file)
├── apps-script.js   # Código para colar no Google Apps Script
└── README.md        # Este arquivo
```

---

## 🛠 Personalização

Para alterar a senha do professor, edite no `index.html`:

```js
const TEACHER_PASS = 'SuaSenhaAqui';
```

Para alterar categorias disponíveis, edite o `<select id="m-category">` no HTML.

---

## 📋 Requisitos

- Navegador moderno (Chrome, Firefox, Edge, Safari)
- Conexão com internet (apenas para carregar as fontes e enviar resultados)
- Conta Google (para o Google Sheets — opcional)
