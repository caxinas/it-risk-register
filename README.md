# IT Risk Register

Aplicação web de gestão de risco de segurança da informação. Ficheiro HTML standalone — sem servidor, sem base de dados, sem dependências externas além de Chart.js (carregado via CDN).

🔗 **[Abrir a aplicação](https://caxinas.github.io/it-risk-register)**

---

## Funcionalidades

### Biblioteca de Sistemas
- Registo de sistemas com classificação CIA (Confidencialidade, Integridade, Disponibilidade) em 4 níveis: Reduzido, Médio, Alto, Muito Alto
- Criticidade global calculada automaticamente a partir dos três vetores
- Tipos: Aplicação Web, API, Mobile, Infraestrutura, SaaS, Base de Dados, Rede

### Análise de Risco (Wizard 8 passos)
1. **CIA** — confirmação/ajuste da classificação para a análise
2. **Bibliotecas** — seleção múltipla de frameworks (OWASP Web, OWASP API, CIS Top 18, ISO 27001, NIST SP 800-53, ou bibliotecas personalizadas)
3. **Riscos** — exclusão de ameaças não aplicáveis
4. **Avaliação inerente** — probabilidade × impacto por risco (escala 1–5)
5. **Matriz inerente** — visualização dos riscos antes de controlos
6. **Controlos** — avaliação de eficácia 0–3 por controlo com feedback
7. **Resumo residual** — comparação inerente vs residual com auto-mitigação
8. **Matriz residual + planos** — posicionamento após controlos e criação de planos de mitigação

### Fórmulas de Risco

**Risco inerente:**
```
Score Inerente = Probabilidade × Impacto
```

**Risco residual** (afeta exclusivamente a probabilidade):
```
Eficácia média = média(eficácia dos controlos avaliados)
Redução = [0%, 20%, 50%, 75%] para eficácia [0, 1, 2, 3]
Probabilidade residual = max(1, round(Prob × (1 − Redução)))
Score Residual = Probabilidade residual × Impacto inerente
```

**Auto-mitigação** (ambos os critérios obrigatórios):
- Score residual ≤ 3 (nível Baixo)
- Eficácia média dos controlos ≥ 2.5

**Níveis de risco:**
| Score | Nível |
|-------|-------|
| 1–3   | Baixo |
| 4–9   | Médio |
| 10–16 | Alto  |
| 17–25 | Crítico |

### Bibliotecas de Riscos
| Biblioteca | Framework | Ameaças |
|-----------|-----------|---------|
| OWASP Top 10 Web | OWASP 2021 | 10 |
| OWASP API Top 10 | OWASP API 2023 | 10 |
| CIS Top 18 | CIS Controls | 10 |
| ISO 27001 Annex A | ISO/IEC 27001:2022 | 10 |
| NIST SP 800-53 | NIST Rev. 5 | 10 |

Possibilidade de criar bibliotecas personalizadas com riscos e controlos próprios.

### Outras funcionalidades
- **Registo de riscos** — tabela global com filtros por nível, sistema e estado
- **Planos de mitigação** — com responsável, data limite, histórico de atualizações e estados (Aberto / Em progresso / Concluído / Cancelado)
- **Matrizes de risco** — inerente e residual, com eixo Y = Impacto, eixo X = Probabilidade
- **Gestão de utilizadores** — 3 perfis (Administrador, Gestor de Risco, Apenas Leitura) com ocultação de abas por perfil
- **Exportar / Importar** — todos os dados em JSON

---

## Como usar

### GitHub Pages (recomendado)
A aplicação está disponível diretamente no URL do GitHub Pages. Não é necessária qualquer instalação.

### Localmente com Python
```bash
# Na pasta do repositório
python -m http.server 8080
# Abrir: http://localhost:8080
```

### Localmente com Node.js
```bash
npx serve .
# Abrir: http://localhost:3000
```

### Como ficheiro local
Abre `index.html` diretamente no browser. Funciona, mas o `localStorage` pode estar limitado dependendo do browser e sistema operativo.

---

## Persistência de dados

Os dados são guardados automaticamente no `localStorage` do browser. Para backup ou partilha, usa os botões **⬇ Exportar** e **⬆ Importar** no cabeçalho da aplicação — geram/leem um ficheiro JSON com todo o estado.

> **Nota:** os dados ficam no browser onde a aplicação é acedida. Cada browser/dispositivo tem o seu próprio estado local.

---

## Tecnologias

- HTML5 + CSS3 + JavaScript vanilla (sem frameworks)
- [Chart.js 4.4.1](https://www.chartjs.org/) — gráficos do dashboard
- Zero dependências de backend

---

## Licença

Uso interno. Adapta livremente às necessidades da tua organização.
