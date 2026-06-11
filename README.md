# Portal de Transparência — Remuneração dos Servidores por Sindicato dos Servidores Públicos de Embu das Artes - SP

Visualização interativa dos dados públicos de remuneração dos servidores municipais de Embu das Artes, com foco em transparência, acessibilidade e fiscalização cidadã.

## O que é

Este projeto reúne e organiza os dados de remuneração publicados mensalmente pela Prefeitura, transformando planilhas brutas em uma interface de consulta pública acessível por qualquer cidadão — no celular ou no computador.

Os dados oficiais, apesar de públicos, são disponibilizados em formatos pouco amigáveis (CSVs e planilhas soltas), sem ferramentas de busca, comparação ou análise. Este portal resolve isso.

## O que você encontra aqui

**Consulta por nome ou matrícula** — pesquise qualquer servidor e veja remuneração bruta, líquida e indenizações.

**Filtro por cargo** — selecione uma das 110 funções e veja todos os servidores daquele cargo, com média salarial e totais.

**Filtro por indenizações** — identifique quem recebe indenizações, filtre por faixa de valor ou visualize o ranking dos maiores valores.

**Painel de indenizações** — card de destaque mostrando o total de indenizações do mês, com detalhamento por cargo ao expandir.

**Gráficos** — distribuição salarial por faixa, proporção percentual e ranking dos 10 maiores cargos por quantidade de servidores.

**Dados mês a mês** — navegação entre os meses disponíveis com carregamento sob demanda.

## Dados disponíveis

| Mês | Servidores | Folha Bruta | Média Bruta | Indenizações | Com Inden. |
|-----|-----------|-------------|-------------|--------------|------------|
| Janeiro/2026 | 4.535 | 30.081.665,78 | 6.633,22 | 1.001.143,77 | 369 |
| Fevereiro/2026 | 4.506 | 29.915.790,65 | 6.639,10 | 905.233,04 | 263 |
| Abril/2026 | 4.716 | 32.169.114,87 | 6.821,27 | 914.489,16 | 219 |
| Maio/2026 | 4.673 | 31.432.961,37 | 6.726,51 | 834.764,19 | 242 |

Março/2026 não está disponível porque a Prefeitura não publicou os dados deste mês.

Todos os valores estão em Reais (R$).

## Tratamento dos dados

Os dados brutos passaram pelas seguintes etapas antes da publicação:

- **Remoção de duplicatas exatas** — registros idênticos (mesma matrícula, cargo e valores) que apareciam repetidos nos arquivos originais foram removidos. Em janeiro, por exemplo, 303 linhas duplicadas foram eliminadas.
- **Preservação de vínculos múltiplos** — servidores com mais de uma matrícula (múltiplos vínculos com cargos diferentes) foram mantidos como registros separados, pois representam vínculos legítimos.
- **Limpeza de caracteres** — caracteres especiais e espaços não-padrão nos nomes de cargos foram normalizados.
- **Nenhum dado foi alterado, estimado ou inferido** — os valores exibidos são exatamente os publicados pela Prefeitura, apenas organizados e limpos.

## Estrutura dos arquivos

```
portal_transparencia.html    ← Página principal (38 KB)
dados_janeiro.json           ← Dados de Janeiro/2026 (485 KB)
dados_fevereiro.json         ← Dados de Fevereiro/2026 (482 KB)
dados_abril.json             ← Dados de Abril/2026 (516 KB)
dados_maio.json              ← Dados de Maio/2026 (503 KB)
README.md                    ← Este arquivo
```

O HTML é leve e carrega os dados sob demanda via `fetch`. Quando o usuário seleciona um mês, apenas o JSON correspondente é baixado — os demais ficam em cache no navegador.

## Como funciona

O portal é um arquivo HTML único com CSS e JavaScript embutidos — sem frameworks, sem dependências pesadas, sem backend. Os dados ficam em arquivos JSON estáticos servidos pelo GitHub Pages.

No celular, a tabela de dados é substituída por cards empilhados verticalmente para eliminar scroll horizontal. No desktop, aparece a tabela tradicional com ordenação por coluna.

A única dependência externa é o Chart.js (carregado via CDN) para os gráficos na aba de visualização.

## Como adicionar um novo mês

1. Obtenha o CSV ou XLSX de remuneração do mês
2. Processe o arquivo gerando um JSON no mesmo formato dos existentes (campos: `data`, `func`, `dist`, `stats`)
3. Nomeie como `dados_[mes].json` (ex: `dados_junho.json`)
4. No `portal_transparencia.html`, adicione a entrada no objeto `FILES` e o botão correspondente no seletor de meses
5. Faça upload dos arquivos atualizados no repositório

## Limitações conhecidas

- **Dados dependem da publicação oficial** — se a Prefeitura não publica, o mês fica indisponível.
- **Março/2026 ausente** — até o momento, os dados deste mês não foram disponibilizados.
- **Cargos comissionados sem detalhamento** — todos aparecem sob a designação genérica "COMISSIONADO", sem informação sobre função exercida, secretaria ou local de trabalho.
- **Portarias de nomeação e exoneração** — não são publicadas em formato digital para consulta pública, dificultando o acompanhamento dos cargos comissionados ativos.

## Fonte dos dados

Todos os dados são provenientes do Portal de Transparência da Prefeitura Municipal e são de domínio público, conforme a Lei de Acesso à Informação (Lei nº 12.527/2011).

## Licença

Os dados são públicos. O código desta visualização é de uso livre.
