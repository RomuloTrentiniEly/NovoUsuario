# Instruções para Agentes IA - SITECASS

## Visão Geral do Projeto
SITECASS é uma página de oferta/acesso com interface premium em glassmorphism. Componente front-end único com foco em experiência visual moderna e fluxo de cadastro estruturado.

## Arquitetura & Estrutura

### Stack Principal
- **Estrutura**: Single HTML file (INDEX.html)
- **Linguagem**: HTML5 + CSS3 puro (sem frameworks externos)
- **Design System**: CSS custom properties (--variables) para tema dark-mode
- **Padrão de Layout**: Centralizado em viewport com max-width 420px

### Sistema de Cores
Definido em `:root`:
- **Background**: `--bg0` (muito escuro), `--bg1` (escuro) com gradientes radiais
- **Acentos**: `--gold` (#d8b773) para destaques, `--green`/`--green2` para botões principais
- **Texto**: `--text` (claro), `--muted` (secundário) com opacidades para hierarquia

## Padrões Específicos do Projeto

### 1. Glassmorphism + Backdrop Filter
Cards e elementos usam `backdrop-filter: blur(22px) saturate(140%)` com fallback `-webkit-`:
```css
backdrop-filter: blur(22px) saturate(140%);
-webkit-backdrop-filter: blur(22px) saturate(140%); /* Safari/iOS */
```

### 2. Efeitos Visuais Compostos
- **Vinheta**: `body:before` com gradiente radial para escurecer bordas
- **Ruído**: `body:after` com padrão SVG fractal (mix-blend-mode: overlay)
- **Brilhos internos**: `::before` e `::after` em elementos principais para profundidade

### 3. Sombras & Profundidade
Usar múltiplas camadas:
```css
box-shadow:
  0 34px 90px rgba(0,0,0,.78),  /* sombra distante */
  0 10px 28px rgba(0,0,0,.55); /* sombra próxima */
```

### 4. Estrutura de Fluxo de Passos
A section `.how` usa:
- Linha vertical (`.flow:before`) conectando items
- Dots circulares (`dot` class) como pontos de parada
- Icons de emoji para representar etapas

## Convenções de Coding

### Nomeação CSS
- Classes em lowercase com hífen: `.primary`, `.secondary`, `.how`
- Modificadores de estado: não há (projeto estático)
- Pseudo-elementos para efeitos: `:before`, `:after`

### Responsive Design
- Base: mobile-first (max-width 420px)
- Sem media queries ainda - adicionar breakpoints se necessário

### HTML Semântico
- `<main>` para conteúdo principal
- `<section>` para agrupamento lógico
- `<ul>` para listas de passos
- Acessibilidade: labels implícitos, cores com suficiente contraste

## Pontos de Customização Comuns

1. **Cores**: Editar `:root` para novo tema
2. **Texto e Conteúdo**: Manter estrutura HTML, atualizar spans/p
3. **Efeitos**: Ajustar `blur()`, `saturate()`, opacidades em backdrop-filter
4. **Botões**: Modificar `.primary` e `.secondary` para novos estados
5. **Fluxo**: Adicionar/remover items em `.flow` preservando classe `.dot`

## Comandos e Workflows
- **Visualização**: Abrir INDEX.html em navegador moderno (Chrome 100+, Safari 15+)
- **Testing**: Testar em dispositivos com blur support; fallback em navegadores legados
- **Build**: Não há build process - arquivo estático pronto para deployment

## Nota sobre Performance
- CSS crítico inline (sem split)
- Sem JavaScript
- SVG fractal renderizado em CSS (não há requestAnimationFrame)
