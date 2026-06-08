# Roteiro ArchiMate - Mission Clear

## 1. Objetivo do diagrama

Este roteiro orienta a montagem manual do diagrama oficial de arquitetura do **Mission Clear** no software **Archi**, usando a notação **ArchiMate** e a visão arquitetural solicitada na matéria **Testing, Compliance & Quality Assurance**.

O diagrama deve demonstrar como o projeto se organiza em quatro níveis:

1. arquitetura de negócio;
2. arquitetura de aplicação;
3. arquitetura de dados;
4. arquitetura de tecnologia.

O arquivo final esperado pela entrega é o modelo salvo em `.archimate` e a view exportada em PDF de alta resolução.

---

## 2. Organização visual sugerida

No Archi, crie uma view chamada:

```text
Arquitetura TOGAF - Mission Clear
```

Organize o desenho em quatro blocos horizontais ou verticais:

```text
[Camada de Negócio]
[Camada de Aplicação]
[Camada de Dados]
[Camada de Tecnologia]
```

Sugestão visual:

- deixe a camada de negócio na parte superior;
- deixe a camada de aplicação no centro;
- deixe os dados próximos aos serviços que os acessam;
- deixe a tecnologia na base do diagrama;
- evite cruzamento excessivo de linhas;
- use nomes curtos nos elementos e descrições no documento escrito.

---

## 3. Camada de negócio

### 3.1 Elementos sugeridos

| Elemento | Tipo ArchiMate sugerido | Descrição |
|---|---|---|
| Operador de Missão | Business Actor | Usuário que simula missão e consulta janelas de lançamento. |
| Pesquisador | Business Actor | Usuário que analisa dados orbitais, detritos e alertas. |
| Administrador | Business Actor | Usuário com permissões administrativas. |
| Simular Missão Orbital Segura | Business Process | Processo principal da solução. |
| Apoio à Decisão de Lançamento Seguro | Business Service | Serviço de negócio entregue pelo sistema. |
| Solicitação de Simulação | Business Event | Evento que inicia o processo de simulação. |
| Janela de Lançamento Recomendada | Outcome | Resultado esperado do processo. |

### 3.2 Relações da camada de negócio

| Origem | Relação | Destino | Justificativa |
|---|---|---|---|
| Operador de Missão | Assignment | Simular Missão Orbital Segura | O operador executa o processo principal. |
| Pesquisador | Association | Apoio à Decisão de Lançamento Seguro | O pesquisador consome os dados analíticos. |
| Administrador | Association | Apoio à Decisão de Lançamento Seguro | O administrador monitora e gerencia uso do sistema. |
| Solicitação de Simulação | Triggering | Simular Missão Orbital Segura | O processo começa quando o usuário solicita uma simulação. |
| Simular Missão Orbital Segura | Realization | Apoio à Decisão de Lançamento Seguro | O processo realiza o serviço de negócio. |
| Simular Missão Orbital Segura | Outcome | Janela de Lançamento Recomendada | O processo produz uma recomendação de janela segura. |

---

## 4. Camada de aplicação

### 4.1 Elementos sugeridos

| Elemento | Tipo ArchiMate sugerido | Descrição |
|---|---|---|
| Mission Clear Mobile App | Application Component | Aplicativo React Native/Expo usado pelo usuário. |
| Mission Clear API | Application Component | API ASP.NET Core responsável pelos endpoints REST e SSE. |
| Auth Service | Application Service | Serviço de autenticação, JWT, refresh token e roles. |
| Orbital Engine Service | Application Service | Serviço que propaga objetos orbitais com SGP4. |
| TLE Ingestion Service | Application Service | Serviço que consome dados orbitais da CelesTrak. |
| Launch Window Service | Application Service | Serviço que calcula janelas de lançamento. |
| Conjunction Detector | Application Service | Serviço que identifica aproximações perigosas. |
| Mission Session Service | Application Service | Serviço que gerencia simulação dinâmica via SSE. |
| Dashboard Module | Application Component | Módulo mobile para status, gráficos e alertas. |
| Debris Module | Application Component | Módulo mobile para busca e detalhes de detritos. |
| Favorites Module | Application Component | Módulo mobile para favoritos. |
| History Module | Application Component | Módulo mobile para histórico de missões. |

### 4.2 Relações da camada de aplicação

| Origem | Relação | Destino | Justificativa |
|---|---|---|---|
| Mission Clear Mobile App | Composition | Dashboard Module | O dashboard faz parte do app. |
| Mission Clear Mobile App | Composition | Debris Module | A busca de detritos faz parte do app. |
| Mission Clear Mobile App | Composition | Favorites Module | Favoritos fazem parte do app. |
| Mission Clear Mobile App | Composition | History Module | Histórico faz parte do app. |
| Mission Clear Mobile App | Serving/Used By | Operador de Missão | O app serve o usuário final. |
| Mission Clear Mobile App | Flow | Mission Clear API | O app consome a API via REST/SSE. |
| Mission Clear API | Composition | Auth Service | A API utiliza autenticação. |
| Mission Clear API | Composition | Orbital Engine Service | A API utiliza propagação orbital. |
| Mission Clear API | Composition | TLE Ingestion Service | A API carrega dados orbitais externos. |
| Mission Clear API | Composition | Launch Window Service | A API calcula janelas de lançamento. |
| Launch Window Service | Serving/Used By | Conjunction Detector | O cálculo da janela depende da avaliação de risco. |
| Mission Clear API | Composition | Mission Session Service | A API gerencia sessões dinâmicas. |

---

## 5. Camada de dados

### 5.1 Elementos sugeridos

| Elemento | Tipo ArchiMate sugerido | Descrição |
|---|---|---|
| User | Data Object | Usuário cadastrado. |
| RefreshToken | Data Object | Token usado para renovar sessão. |
| Mission | Data Object | Missão simulada e salva no histórico. |
| MissionSession | Data Object | Sessão dinâmica de simulação. |
| OrbitalObject | Data Object | Objeto orbital/detrito espacial. |
| LaunchWindow | Data Object | Janela de lançamento calculada. |
| ConjunctionAlert | Data Object | Alerta de aproximação. |
| Destination | Data Object | Destino orbital escolhido. |
| RiskScore | Data Object | Pontuação de risco calculada. |
| MySQL Database | Technology Service ou Node/Artifact | Banco relacional que persiste dados do sistema. |

### 5.2 Relações da camada de dados

| Origem | Relação | Destino | Justificativa |
|---|---|---|---|
| Auth Service | Access | User | Autenticação consulta e registra usuários. |
| Auth Service | Access | RefreshToken | Serviço cria e invalida refresh tokens. |
| Mission Session Service | Access | MissionSession | Serviço gerencia sessões dinâmicas. |
| Mission Session Service | Access | Mission | Serviço salva resultado final. |
| Launch Window Service | Access | LaunchWindow | Serviço gera janelas de lançamento. |
| Launch Window Service | Access | RiskScore | Serviço calcula risco. |
| Conjunction Detector | Access | ConjunctionAlert | Detector gera alertas. |
| Orbital Engine Service | Access | OrbitalObject | Motor propaga objetos orbitais. |
| Mission Clear API | Access | MySQL Database | API persiste e consulta dados relacionais. |

---

## 6. Camada de tecnologia

### 6.1 Elementos sugeridos

| Elemento | Tipo ArchiMate sugerido | Descrição |
|---|---|---|
| Smartphone ou Emulador | Device | Dispositivo onde o app mobile é executado. |
| Expo Runtime | System Software | Ambiente de execução do app mobile. |
| Servidor Backend .NET | Node | Ambiente que executa a API ASP.NET Core. |
| ASP.NET Core Runtime | System Software | Runtime do backend. |
| Servidor MySQL | Node | Ambiente do banco de dados relacional. |
| MySQL 8 | System Software | Software de banco de dados. |
| Internet | Communication Network | Rede para comunicação com CelesTrak e clientes. |
| CelesTrak API | Technology Service | Fonte externa de dados orbitais. |
| SGP4 Library | Artifact/System Software | Biblioteca usada para propagação orbital. |
| Aspire Dashboard | Technology Service | Observabilidade local com logs, traces e health checks. |
| GitHub | Technology Service | Hospedagem e versionamento dos repositórios. |
| YouTube | Technology Service | Hospedagem do vídeo pitch não listado. |
| Microsoft Teams | Technology Service | Plataforma de envio da entrega. |

### 6.2 Relações da camada de tecnologia

| Origem | Relação | Destino | Justificativa |
|---|---|---|---|
| Smartphone ou Emulador | Assignment | Mission Clear Mobile App | O app executa no dispositivo. |
| Servidor Backend .NET | Assignment | Mission Clear API | A API executa no servidor backend. |
| Servidor MySQL | Assignment | MySQL Database | O banco executa no servidor MySQL. |
| Mission Clear API | Flow | CelesTrak API | A API consome dados externos. |
| Orbital Engine Service | Association | SGP4 Library | O serviço usa a biblioteca de propagação orbital. |
| Aspire Dashboard | Association | Mission Clear API | O dashboard monitora a API. |
| Mission Clear Mobile App | Flow | Mission Clear API | Comunicação HTTP REST/SSE. |

---

## 7. Relações principais para montar no Archi

Use esta tabela como base prática para criar as linhas do diagrama.

| Origem | Relação ArchiMate sugerida | Destino |
|---|---|---|
| Operador de Missão | Assignment | Simular Missão Orbital Segura |
| Solicitação de Simulação | Triggering | Simular Missão Orbital Segura |
| Simular Missão Orbital Segura | Realization | Apoio à Decisão de Lançamento Seguro |
| Simular Missão Orbital Segura | Outcome | Janela de Lançamento Recomendada |
| Mission Clear Mobile App | Serving | Operador de Missão |
| Mission Clear Mobile App | Flow | Mission Clear API |
| Mission Clear API | Composition | Auth Service |
| Mission Clear API | Composition | Orbital Engine Service |
| Mission Clear API | Composition | TLE Ingestion Service |
| Mission Clear API | Composition | Launch Window Service |
| Mission Clear API | Composition | Mission Session Service |
| Launch Window Service | Serving/Used By | Conjunction Detector |
| TLE Ingestion Service | Flow | CelesTrak API |
| Orbital Engine Service | Association | SGP4 Library |
| Auth Service | Access | User |
| Auth Service | Access | RefreshToken |
| Mission Session Service | Access | MissionSession |
| Mission Session Service | Access | Mission |
| Launch Window Service | Access | LaunchWindow |
| Conjunction Detector | Access | ConjunctionAlert |
| Mission Clear API | Access | MySQL Database |
| Aspire Dashboard | Association | Mission Clear API |

---

## 8. Passo a passo no Archi

1. Abra o **Archi**.
2. Crie um novo modelo: `File > New > ArchiMate Model`.
3. Salve o modelo com o nome:

```text
Mission_Clear_Testing_QA.archimate
```

4. Crie uma nova view chamada:

```text
Arquitetura TOGAF - Mission Clear
```

5. Na parte superior da view, crie a **Camada de Negócio** com os atores, processo, evento, serviço e outcome.
6. No centro, crie a **Camada de Aplicação** com app mobile, API e serviços backend.
7. Próximo aos serviços, crie a **Camada de Dados** com os objetos de dados e o banco.
8. Na base, crie a **Camada de Tecnologia** com dispositivos, servidores, internet, CelesTrak, SGP4, Aspire, GitHub, YouTube e Teams.
9. Crie as relações usando a tabela da Seção 7.
10. Organize as linhas para não cruzarem demais.
11. Revise se todas as camadas solicitadas pelo professor aparecem.
12. Exporte a view em PDF:

```text
File > Export > View as Image > PDF
```

13. Salve o PDF como:

```text
Mission_Clear_Diagrama_ArchiMate.pdf
```

14. Salve novamente o modelo `.archimate`.

---

## 9. Conferência antes de exportar

Antes de gerar o PDF, confira:

- [ ] A camada de negócio possui atores, processo, evento, serviço e resultado.
- [ ] A camada de aplicação possui app mobile, API e serviços backend.
- [ ] A camada de dados possui objetos principais e MySQL.
- [ ] A camada de tecnologia possui dispositivo, servidor, banco, internet, CelesTrak, SGP4 e Aspire.
- [ ] O fluxo Mobile -> API -> Serviços -> Dados/Integrações está claro.
- [ ] O diagrama não possui excesso de cruzamento de linhas.
- [ ] O nome do projeto aparece no título da view.
- [ ] O arquivo `.archimate` foi salvo.
- [ ] O PDF foi exportado em alta resolução.

---

## 10. Resumo do que entregar

| Arquivo | Obrigatório | Observação |
|---|---|---|
| `Mission_Clear_Testing_QA.archimate` | Sim | Gerado manualmente no Archi. |
| `Mission_Clear_Diagrama_ArchiMate.pdf` | Sim | Exportado do Archi. |
| Documento único da entrega | Sim | Deve conter nomes, RMs e link do vídeo. |
| Link do vídeo pitch | Sim | Deve estar no documento. |
