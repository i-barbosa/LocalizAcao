# LocalizAção — Trajeto Seguro

**Hackathon Recriando a Cidade** · Trilha Segurança · Desafio #5 (também toca o Desafio #6 — denúncia)
Prefeitura do Recife / Emprel · 19/09/2026 · Uninassau Graças

Equipe: LATec FICR / Matryz — estudantes de Sistemas para Internet / ADS da FICR (Faculdade Católica Imaculada Conceição do Recife), Porto Digital.

---

## Sumário

- [O problema](#o-problema)
- [Pergunta norteadora](#pergunta-norteadora)
- [Metodologia da pesquisa](#metodologia-da-pesquisa)
- [Dados coletados](#dados-coletados)
- [Depoimentos](#depoimentos)
- [Dados de apoio (fontes externas)](#dados-de-apoio-fontes-externas)
- [A solução](#a-solução)
- [Fluxo de dados](#fluxo-de-dados)
- [Protótipos ao vivo](#protótipos-ao-vivo)
- [Arquitetura técnica / stack de produção](#arquitetura-técnica--stack-de-produção)
- [Estimativa de custo](#estimativa-de-custo)
- [Requisitos para produção (LGPD e afins)](#requisitos-para-produção-lgpd-e-afins)
- [Modelo de negócio e roadmap](#modelo-de-negócio-e-roadmap)
- [Perguntas que a banca fez](#perguntas-que-a-banca-fez)
- [Notas para uma próxima versão](#notas-para-uma-próxima-versão)
- [Créditos](#créditos)

---

## O problema

A percepção de insegurança durante o deslocamento, especialmente no período noturno, afeta a rotina dos estudantes universitários da Região Metropolitana do Recife (RMR). Não é só estatística de crime: é gente trocando de curso, largando matéria noturna, gastando mais com transporte por aplicativo, mudando de rota — o medo em si já é o problema, além da violência que o origina.

## Pergunta norteadora

> Como garantir segurança e autonomia no deslocamento noturno dos estudantes da RMR?

Tags do desafio oficial: **Playable**, **Inclusive**.

---

## Metodologia da pesquisa

A coleta rodou em dois canais paralelos e independentes, propositalmente — é a mesma lógica que o produto final usaria em produção:

1. **Formulário próprio ("Conectar")** — disfarçado de tela de login de Wi-Fi público, nome de rede "Trajeto Seguro". Captura geolocalização do navegador (com consentimento, e a pessoa pode recusar e enviar mesmo assim). Salvo num banco compartilhado.
2. **Google Forms / Google Sheets** — canal oficial, é o que geraria o link enviado por SMS/WhatsApp da prefeitura em produção.

Os dois nunca se misturam na origem — são somados só na hora de gerar o painel.

**Nota de reconciliação de número:** a planilha, numa leitura intermediária, tinha 78 respostas; o slide do pitch fechado cita 83 — provavelmente entrou mais gente depois da última puxada, ou os dois cálculos vieram de momentos diferentes da coleta. Os dois números de "inseguro no trajeto" bateram quase exato (80,8% vs 81%). O de "já foi vítima" divergiu mais (25,6% vs 21%) — essa reconciliação não chegou a ser fechada antes da apresentação; fica registrada aqui como pendência de quem revisitar os dados.

---

## Dados coletados

### Visão geral — 83 respostas (número do slide, mais recente)

| Métrica | Valor |
|---|---|
| Não se sentem seguros no trajeto pra faculdade | **81%** |
| Já foram assaltados, roubados ou ameaçados indo/voltando | **21%** |
| Mudaram de rota ou horário por sensação de insegurança | **25%** |

### Recortes adicionais — 78 respostas (última leitura da planilha, ainda não refletidos no slide)

- Dependem de transporte público: **84,6%** (67 de 78)
- Vitimização por gênero: mulheres **26,2%** (11 de 42) · homens **22,9%** (8 de 35) — diferença menor do que a amostra pequena inicial sugeria (era 2,15x com n=27, caiu pra ~1,14x com n=78)
- Insegurança por turno: **matutino 96,4%** (27 de 28) · noturno 78,4% (29 de 37) · diurno 58,3% (7 de 12)
  → achado que contraria a intuição de "só de noite é perigoso" — o matutino ficou consistentemente pior nas duas leituras da coleta
- Principais demandas dos estudantes (múltipla escolha, n=55 respostas): **agentes de segurança** e **movimento de pessoas** empatados em 74,5%, iluminação das ruas 69,1%, comércio aberto 52,7%, transporte público 36,4%, calçadas/espaço urbano 29,1%
- **Achado orgânico**: dois respondentes diferentes, em momentos distintos, sem qualquer pergunta direcionada, citaram o mesmo ponto exato de risco — o trecho entre Recife Antigo e Graças/Agamenon, perto do cemitério de Santo Amaro, com postes de luz apagados. Validação cruzada espontânea de um ponto de risco real — é o tipo de coisa que o mapa do produto acharia sozinho em escala.

---

## Depoimentos

- **Luísa, estudante da FICR** — "Já presenciei assaltos, até com agentes próximos, e casos de assédio em veículos lotados."
- **Jonathan, 25 anos, usuário de tecnologia assistiva (Associação Pernambucana de Cegos)** — foi seguido até o ônibus e assediado; passou a mudar de rota depois do episódio.
- **Relato anônimo, Praça Tiradentes** — sofreu assédio verbal ao descer do ônibus perto da faculdade, antes de aula noturna; relatou medo de o agressor saber onde ela estuda e em que horário.
- **Raquel, estudante universitária do Recife** — insegurança por invasão de espaço; desconfia do sistema de segurança do entorno por não conhecer sua atuação nem localização.
- **Homem, 25 a 34 anos, volta de bicicleta à noite** — trecho entre Recife Antigo e Graças, perto do cemitério de Santo Amaro, com postes normalmente apagados; pede prioridade na manutenção pelo risco de acidente grave.
- **Mulher, 18 a 24 anos, desloca de manhã** — já sofreu assédio em transporte público lotado e presenciou assalto durante o dia mesmo com agentes de segurança próximos; pede mais efetivo, frota e policiamento nos BRTs.

---

## Dados de apoio (fontes externas)

**Nacional**
- 98% das estudantes brasileiras têm a rotina de estudos afetada quando matriculadas em curso noturno, por insegurança no trajeto casa-faculdade — influencia inclusive a escolha de curso e instituição (Correio Braziliense, 16/09/2026, citando pesquisa nacional)
- Datafolha: 39% dos brasileiros se sentem muito inseguros andando à noite nas ruas; em região metropolitana sobe pra 52%
- PNAD Sensação de Segurança: 89,5% se sentem seguros em casa, caindo pra 54,6% na cidade — o medo cresce conforme o espaço fica mais público

**Pernambuco / RMR**
- SDS-PE: 65,9 mortes violentas por 100 mil habitantes no Recife em 2023 (577 casos)
- Assaltos a ônibus na RMR: 507 casos entre jan-out/2023, alta de 33,4% sobre 2022; outubro sozinho subiu 152%

**Campus (prova de conceito acadêmica)**
- Estudo UFPE/Zenodo cruzou iluminação pública com percepção de insegurança no campus Recife da UFPE, usando GNSS de smartphone + questionário. Identificou pontos de risco concreto perto de CCS, Biblioteca Central, NIATE/CFCH e Casa do Estudante — valida que o método (mapa + percepção) já funciona em Recife, dentro de universidade.

**Contexto de acessibilidade da cidade**
- Recife é a 9ª capital brasileira com maior número de pessoas com deficiência: 182 mil (Plano Recife 500 anos)

---

## A solução

**LocalizAção** é uma plataforma que transforma percepção de insegurança em dado acionável: coleta relato geolocalizado do estudante, agrega em tempo real e entrega num painel público pra gestão da cidade decidir onde investir (iluminação, policiamento, ponto de ônibus).

Duas frentes:
1. **Coleta** — formulário curto (~1 min), com localização opcional, acessível por dois canais diferentes (ver abaixo).
2. **Painel LocalizAção** — dashboard com 5 abas: Painel Geral, Por Gênero, Por Turno, Demandas, Depoimentos. Atualiza ao vivo conforme chegam respostas.

### Regras de identidade visual do produto
- Fundo escuro, verde de marca (#22C55E) como accent, azul (#4C8DFF) pros dados, tipografia Archivo
- Nada de gradiente pesado, ícone genérico de biblioteca (lucide), sombra pronunciada, ou "bento grid" decorativo sem função — o visual segue um padrão editorial/dashboard funcional, não um template de marketing

---

## Fluxo de dados

Duas formas de chegar ao mesmo tipo de formulário — convergem antes do painel:

```
Cadastro na rede Wi-Fi          SMS/WhatsApp da prefeitura
   (demo do hackathon)                 (canal de produção)
        │                                     │
        ▼                                     ▼
Formulário "Conectar"              Formulário Google Forms
  (10 perguntas + GPS)                  (canal oficial)
        │                                     │
        ▼                                     ▼
 Banco compartilhado                Planilha Google Sheets
   (Claude DB, ao vivo)                (respostas oficiais)
        │                                     │
        └───────────────┬─────────────────────┘
                         ▼
              Claude soma os dados
              (recalcula estatísticas)
                         │
                         ▼
              Painel LocalizAção
    (Geral · Gênero · Turno · Demandas · Depoimentos)
```

Em produção, a camada "Claude soma os dados" vira agregação automática via **pg_cron** direto no Postgres (ver stack abaixo) — o recálculo manual foi só o método usado durante o hackathon.

---

## Protótipos ao vivo

- **Painel/dashboard (Figma Make)**: https://www.figma.com/make/KIEXOUv4EaYGUo3sJUy6jm/Landing-Page-dados---MVP-Hackaton--Recriando-a-Cidade
- **Tela de conectar + formulário (código-fonte, GitHub)**: https://github.com/i-barbosa/trajeto-seguro-wifi
  — se o GitHub Pages estiver ativado nas configurações do repo, fica público em `https://i-barbosa.github.io/trajeto-seguro-wifi/`
- **Protótipo completo funcional (conectar → formulário → painel, tudo num link)**: gerado durante o hackathon via Claude Artifacts — pedir o link atualizado ao time se for reapresentar
- **Painel LocalizAção isolado, com dado ao vivo da planilha**: idem acima

---

## Arquitetura técnica / stack de produção

| Camada | Tecnologia | Por quê |
|---|---|---|
| Front + back | **Next.js + TypeScript** | um único time cobre as duas pontas; mão de obra abundante no mercado nacional, fácil de contratar/manter depois |
| Banco de dados | **PostgreSQL** | agregação (GROUP BY, COUNT) nativa pros indicadores do painel — NoSQL obrigaria a somar tudo no código |
| Agregação | **pg_cron** (extensão nativa do Postgres) | recalcula estatísticas periodicamente numa tabela própria; o painel nunca faz cálculo pesado na hora de carregar |
| Tempo real (opcional) | **Supabase self-hosted** (Docker, na infra da própria prefeitura — não o SaaS pago) | camada de tempo real sobre Postgres, sem depender de serviço cobrado em dólar |
| Hospedagem | Infra da Emprel, ou nuvem nacional / VPS cobrado em real | evita custo imprevisível por câmbio; sem lock-in de fornecedor único |
| Envio de aviso | **WhatsApp Business API**, categoria **Utilidade** | ~R$0,05–0,07/msg com margem do BSP — 6 a 7x mais barato que categoria Marketing (~R$0,31–0,38); é o enquadramento correto pra aviso institucional, não propaganda |
| Fallback de envio | SMS | ~R$0,08–0,15/msg, alcança quem não usa WhatsApp — questão de inclusão digital, não só custo |

**Por que não Vercel/Supabase-cloud/Firebase como destino final:** cobram em dólar, o custo varia com câmbio, ruim pra orçamento público planejado em real. Bom pra prototipar, não pra quem vai manter por anos.

---

## Estimativa de custo

**Infraestrutura recorrente:** ~R$ 50–250/mês (VPS + Postgres gerenciado; domínio `.gov.br` e SSL são gratuitos)

**Disparo de mensagem — piloto de 10 mil estudantes:**
- Só WhatsApp (categoria Utilidade): ~R$ 600
- Só SMS: ~R$ 1.000
- Misto (WhatsApp primário + SMS de inclusão): ~R$ 700–900

A stack inteira é open source, sem custo de licença — o gasto real é quase todo no disparo de mensagem, não na infraestrutura.

---

## Requisitos para produção (LGPD e afins)

**Funcionais:** formulário validado, geolocalização com consentimento explícito (nunca bloqueante), dois canais de entrada, painel só com dado agregado (nunca individual exposto), exportação de dado agregado pra outras secretarias.

**Infraestrutura:** hospedagem com datacenter no Brasil (obrigatório por dado sensível), Postgres com backup e replicação automática, deploy em Docker, ambiente de homologação separado, monitoramento de disponibilidade.

**LGPD — bloqueador antes de qualquer linha de código em produção:**
- Base legal definida (provavelmente interesse público / exercício de política pública)
- Coleta mínima: nada de nome, CPF ou telefone atrelado à resposta
- Anonimização/agregação antes de qualquer exibição pública
- Localização armazenada com precisão reduzida (bairro) quando possível
- Prazo de retenção definido pra apagar dado bruto após virar estatística
- Criptografia em repouso e em trânsito (TLS)
- Parecer do DPO/encarregado de dados da prefeitura antes do lançamento
- Aviso de privacidade visível no momento da coleta

**Segurança:** rate limiting no endpoint de envio, validação de schema no backend (nunca confiar só no front), controle de acesso por perfil no painel administrativo, log de acesso sem logar dado pessoal desnecessário.

**Acessibilidade:** funcional em conexão 3G, compatível com leitor de tela, mensagem de SMS/WhatsApp curta com link oficial (nunca encurtador de terceiro).

---

## Modelo de negócio e roadmap

**Modelo B2G** — cliente principal são prefeituras e secretarias (Segurança, Turismo, Infraestrutura). Modelo "figital": une intervenção urbana e gestão digital.

**Concorrentes mapeados:** Conecta Recife, Google Maps, colab.gov, apps de acessibilidade genéricos — nenhum, segundo levantamento próprio, cruza percepção de insegurança georreferenciada com rota sugerida especificamente pro público estudantil.

**Diferenciais declarados:** solução mais completa (mede percepção, não só ocorrência registrada), escalável pra outras regiões, custo-benefício (stack aberta, sem licença), oportunidade de participação direta da população na coleta do próprio dado.

### Fases

- **Fase 1 — Piloto e validação institucional:** teste em recorte definido (ex.: RMR, estudantes), validação direta com secretarias envolvidas, coleta de indicadores de impacto social.
- **Fase 2 — Formalização e expansão municipal:** ampliação pra outros públicos/áreas, contrato de manutenção e auditoria contínua.
- **Fase 3 — Política pública e legado:** integração a um plano municipal de segurança/mobilidade e a um dashboard de gestão urbana mais amplo, posicionando o Recife como referência.

---

## Créditos

Projeto desenvolvido no Hackathon **Recriando a Cidade** (Prefeitura do Recife), pela equipe **Reação** (criado na hora), onde juntou estudantes da CESAR SCHOOL, FICR e outras instituições de ensino em recife e proximidades.