# Amazon Title Adjuster

Painel web para ajuste automático de títulos de anúncios da Amazon para até 75 caracteres. Processa planilhas CSV/XLSX com visualização em tempo real.

**🔗 Demo ao vivo:** [painel será publicado via Netlify]

---

## Features

✅ Upload de CSV ou XLSX  
✅ Auto-detecção da coluna de títulos  
✅ Visualização lado-a-lado (original vs ajustado)  
✅ Estatísticas: total de títulos, quantos foram cortados, caracteres removidos  
✅ Download em CSV ou XLSX  
✅ 100% processamento local (sem envio de dados)  
✅ Responsivo (mobile/desktop)  

---

## Setup no GitHub + Netlify

### 1. **Fork ou criar o repositório**

```bash
# Clone ou crie um novo repo chamado `amazon-title-adjuster`
git clone https://github.com/YOUR-USERNAME/amazon-title-adjuster.git
cd amazon-title-adjuster
```

### 2. **Estrutura do repo**

```
amazon-title-adjuster/
├── index.html          # O painel (renomear amazon-title-adjuster.html)
├── README.md           # Este arquivo
└── .gitignore         # (opcional)
```

### 3. **Fazer push para GitHub**

```bash
git add .
git commit -m "Initial commit: Amazon Title Adjuster painel"
git push origin main
```

### 4. **Deploy no Netlify**

**Opção A: Via GitHub (recomendado)**

1. Vá para [netlify.com](https://netlify.com)
2. Clique em **"New site from Git"**
3. Conecte seu repositório GitHub
4. Netlify detectará `index.html` automaticamente
5. Deploy concluído! Você receberá uma URL como `amazon-title-adjuster.netlify.app`

**Opção B: Deploy manual**

```bash
npm install -g netlify-cli
netlify login
netlify deploy --prod --dir=.
```

---

## Como usar

### Upload de Planilha

1. Clique para selecionar ou arraste um arquivo CSV/XLSX
2. O painel detecta automaticamente a coluna de títulos
3. Se houver múltiplas colunas, selecione manualmente no dropdown

### Processamento

- Títulos com **até 75 caracteres** = ✅ OK
- Títulos com **mais de 75** = ✂️ Ajustados (truncados)

### Download

- **CSV**: para importar em planilhas simples
- **XLSX**: para manter formatação mais complexa

---

## Estrutura de Dados

### Input Esperado

Qualquer planilha com uma coluna de títulos:

| Título | SKU | Marketplace |
|--------|-----|-------------|
| Produto XYZ - Descrição Muito Longa Do Seu Artigo Com Várias Palavras | SKU001 | Amazon |

### Output

| Título_original | Título_adjusted | status |
|---|---|---|
| Produto XYZ - Descrição Muito Longa Do Seu Artigo Com Várias Palavras | Produto XYZ - Descrição Muito Longa Do Seu Artig | Ajustado |

Todas as outras colunas são preservadas no download.

---

## Integração com n8n (opcional)

Se quiser automatizar via webhook com n8n:

### Setup do Webhook n8n

1. Crie um workflow no n8n com trigger **"Webhook"**
2. Configure o método POST
3. Aponte para esse webhook do seu painel (editar JS)

### Exemplo de Payload esperado

```json
{
  "titles": [
    { "original": "Título muito longo...", "sku": "ABC123" },
    { "original": "Outro título...", "sku": "ABC124" }
  ]
}
```

### Resposta esperada

```json
{
  "results": [
    {
      "original": "Título muito longo...",
      "adjusted": "Título muito lon...",
      "status": "Adjusted"
    }
  ]
}
```

---

## Customizações

### Alterar limite de caracteres

No `index.html`, procure por `substring(0, 75)` e altere `75` para outro número:

```javascript
const adjusted = original.substring(0, 75); // Alterar aqui
```

### Adicionar colunas adicionais (SKU, ASIN, etc)

O painel já preserva todas as colunas da planilha original no download. Nenhuma alteração necessária.

### Estilo/Cores

Altere as variáveis CSS no `<style>`:

```css
/* Cor principal (azul claro) */
background: linear-gradient(135deg, #38bdf8, #06b6d4);

/* Fundo escuro */
background: linear-gradient(135deg, #0f172a 0%, #1e293b 100%);
```

---

## Browser Support

- ✅ Chrome/Chromium 90+
- ✅ Firefox 88+
- ✅ Safari 14+
- ✅ Edge 90+

---

## Troubleshooting

### "Planilha vazia"
- Certifique-se que o arquivo tem dados além do header
- Tente salvar como CSV (às vezes XLSX corrompido)

### "Erro ao ler o arquivo"
- Verifique que é CSV ou XLSX (não XLS antigo)
- Tente fazer upload novamente

### Coluna de títulos não foi detectada
- Selecione manualmente no dropdown
- Se o dropdown não aparecer, verifique se o arquivo tem headers

---

## Próximas Melhorias

- [ ] Integração direta com Amazon API (ler títulos atuais)
- [ ] Sugerir títulos automáticos via AI (GPT/Gemini)
- [ ] Histórico de processamentos
- [ ] Integração com n8n via webhook bidirecional
- [ ] Dark mode (já tem, adicionar toggle)

---

## License

MIT - Use livremente para SellersFlow

---

## Suporte

Para dúvidas ou bugs, abra uma issue no GitHub.

**Desenvolvido para SellersFlow** | Amazon Marketplace Management  
Vanessa Rodrigues | Gerenciamento de Projetos
