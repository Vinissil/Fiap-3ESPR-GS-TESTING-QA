# GS - Testing, Compliance & Quality Assurance

## Mission Clear — Monitoramento de Detritos Espaciais e Simulação de Missões LEO Seguras

Documentação da entrega da disciplina **Testing, Compliance & Quality Assurance**, referente à **Global Solution 2026 — FIAP**.

O projeto **Mission Clear** é uma solução voltada ao monitoramento de detritos espaciais e à simulação de missões orbitais em órbita baixa terrestre, conhecida como **LEO — Low Earth Orbit**.

---

## Integrantes

| Nome                      | RM        |
| ------------------------- | --------- |
| Gustavo Bezerra Assumção  | RM 553076 |
| Jó Sales                  | RM 552679 |
| Miguel Garcez de Carvalho | RM 553768 |
| Vinicius Souza e Silva    | RM 552781 |
| Edson Leonardo            | RM 553737 |

---

## Links Oficiais

### Repositório Backend

https://github.com/FIAP-BitsNBytes/Fiap-3ESPR-GS-C

### Repositório Mobile

https://github.com/FIAP-BitsNBytes/Fiap-3ESPR-GS-Mobile

### Vídeo Pitch

https://youtu.be/k5pnDVZDgqw

---

## Objetivo da Entrega

Esta entrega tem como objetivo documentar a arquitetura da solução **Mission Clear** com foco em **Testing, Compliance & Quality Assurance**, utilizando uma visão estruturada baseada em TOGAF e representação arquitetural em ArchiMate.

A documentação apresenta:

* breve descritivo do projeto;
* arquitetura da solução;
* visão de negócio;
* visão de aplicação;
* visão de dados;
* visão de tecnologia;
* estratégia de testes;
* critérios de qualidade;
* requisitos e riscos;
* arquivo editável do Archi;
* PDF do diagrama de arquitetura.

---

## Descrição do Projeto

O **Mission Clear** aborda o problema do risco de colisão entre missões espaciais e detritos orbitais.

Detritos espaciais, como fragmentos de satélites, estágios de foguetes e objetos resultantes de colisões, podem cruzar a trajetória de uma missão em alta velocidade. Sem uma análise prévia, esse risco pode não ser percebido pelo operador da missão.

A solução proposta utiliza dados orbitais reais, processa informações de detritos espaciais, calcula riscos de conjunção e apresenta janelas de lançamento com menor risco para o destino escolhido.

O sistema é composto por duas partes principais:

1. **Backend**

   * API REST em .NET/C#.
   * Consumo de dados reais da CelesTrak.
   * Propagação orbital com SGP4.
   * Cálculo de risco de conjunção.
   * Geração de janelas de lançamento seguras.
   * Simulação de missão.
   * Autenticação JWT.
   * Persistência em MySQL.
   * Observabilidade com Aspire/OpenTelemetry.

2. **Mobile**

   * Aplicativo em React Native com Expo.
   * Dashboard orbital.
   * Consulta de detritos espaciais.
   * Simulação de missão.
   * Favoritos.
   * Histórico.
   * Consumo da API backend.
   * Persistência local de sessão e preferências.

---

## Arquitetura da Solução

A arquitetura foi organizada em quatro camadas principais:

1. Camada de Negócio.
2. Camada de Aplicação.
3. Camada de Dados.
4. Camada de Tecnologia.

Essa organização permite visualizar o relacionamento entre usuários, processos, componentes de software, dados e infraestrutura tecnológica.

---

## Camada de Negócio

A camada de negócio representa os principais papéis envolvidos e o processo central da solução.

### Papéis

* **Operador de Missão:** utiliza o sistema para simular missões e consultar janelas de lançamento seguras.
* **Pesquisador:** consulta informações orbitais e dados de detritos espaciais.
* **Administrador:** possui responsabilidades relacionadas à gestão e controle do sistema.

### Processo Principal

O processo principal representado na arquitetura é:

**Simular Missão Orbital Segura**

Esse processo contempla:

1. solicitação de simulação;
2. seleção de destino;
3. análise dos detritos orbitais;
4. cálculo de risco;
5. geração de janela de lançamento recomendada;
6. apresentação do resultado ao usuário.

---

## Camada de Aplicação

A camada de aplicação representa os componentes de software responsáveis pela execução da solução.

### Componentes Principais

* **Mission Clear Mobile App**

  * Interface utilizada pelo usuário final.
  * Permite acesso ao dashboard, detritos, favoritos, histórico e simulação de missão.

* **Mission Clear API**

  * API backend responsável pela regra de negócio, autenticação, cálculos orbitais e integração com dados externos.

* **Auth Service**

  * Responsável por autenticação, login, registro, JWT e refresh token.

* **Orbital Engine Service**

  * Responsável pelo processamento orbital e propagação de objetos espaciais.

* **TLE Ingestion Service**

  * Responsável por consumir dados orbitais da CelesTrak.

* **Launch Window Service**

  * Responsável por calcular janelas de lançamento com menor risco.

* **Conjunction Detector**

  * Responsável por detectar aproximações perigosas entre missão e detritos espaciais.

* **Mission Session Service**

  * Responsável por controlar sessões de simulação e eventos em tempo real.

---

## Camada de Dados

A camada de dados representa as principais informações manipuladas pela solução.

### Principais Dados

* **User**

  * Representa os usuários autenticados.

* **RefreshToken**

  * Representa os tokens utilizados para renovação de sessão.

* **Mission**

  * Representa uma missão simulada.

* **MissionSession**

  * Representa uma sessão de simulação dinâmica.

* **OrbitalObject**

  * Representa um objeto orbital ou detrito espacial.

* **LaunchWindow**

  * Representa uma janela de lançamento calculada.

* **ConjunctionAlert**

  * Representa um alerta de aproximação perigosa.

* **Destination**

  * Representa o destino orbital selecionado.

* **RiskScore**

  * Representa a pontuação de risco calculada.

* **MySQL Database**

  * Banco de dados relacional utilizado pela solução.

---

## Camada de Tecnologia

A camada de tecnologia representa os recursos técnicos utilizados para execução, comunicação e monitoramento da solução.

### Elementos Técnicos

* Smartphone ou emulador.
* Expo Runtime.
* Servidor backend .NET.
* ASP.NET Core Runtime.
* Servidor MySQL.
* MySQL 8.
* Internet.
* CelesTrak API.
* Biblioteca SGP4.
* Aspire Dashboard.
* GitHub.
* YouTube.
* Microsoft Teams.

---

## Tecnologias Utilizadas

### Backend

* .NET
* ASP.NET Core
* API REST
* MySQL
* Entity Framework Core
* JWT
* Refresh Token
* SGP4
* Server-Sent Events
* OpenTelemetry
* Aspire Dashboard
* xUnit

### Mobile

* React Native
* Expo
* TypeScript
* Axios
* AsyncStorage
* SecureStore
* Context API
* React Navigation

### Arquitetura e Documentação

* Archi
* ArchiMate
* TOGAF
* Markdown
* PDF

---

## Testing, Compliance & Quality Assurance

A documentação de QA foi elaborada para demonstrar como a solução pode ser validada em termos de funcionamento, segurança, rastreabilidade, qualidade e manutenção.

A estratégia considera diferentes grupos de testes e critérios de qualidade.

---

## Estratégia de Testes

Foram considerados os seguintes tipos de teste:

### Testes Unitários

Aplicados aos principais serviços do backend, como:

* AuthService.
* JwtService.
* LaunchWindowService.
* ConjunctionDetector.
* OrbitalEngineService.
* MissionService.
* UserService.

Objetivo: validar regras isoladas de negócio e reduzir o risco de falhas internas.

### Testes de Integração

Aplicados à comunicação entre componentes, como:

* API com MySQL.
* Repositories com Entity Framework Core.
* API com serviços internos.
* Backend com CelesTrak.
* Histórico de missões.
* Refresh token.

Objetivo: verificar se as partes do sistema funcionam corretamente em conjunto.

### Testes de API

Aplicados aos principais endpoints, como:

* `GET /api/status`
* `GET /api/destinations`
* `GET /api/debris`
* `GET /api/debris/stats`
* `GET /api/launch-windows`
* `GET /api/launch-windows/best`
* `POST /api/mission/simulate`
* `POST /api/mission/session`
* `GET /api/mission/session/{id}/stream`
* `POST /api/auth/register`
* `POST /api/auth/login`
* `POST /api/auth/refresh`
* `POST /api/auth/logout`
* `GET /api/users/me`
* `GET /api/missions`
* `GET /api/dashboard/summary`
* `GET /api/dashboard/alerts`

Objetivo: validar funcionamento, respostas, status HTTP, autenticação e tratamento de erro.

### Testes de Autenticação e Autorização

Incluem validações como:

* login válido;
* login inválido;
* cadastro;
* refresh token válido;
* refresh token expirado;
* logout;
* acesso com token;
* acesso sem token;
* permissões de Researcher;
* permissões de Administrator;
* bloqueio de operação não permitida.

Objetivo: garantir controle de acesso e proteção das funcionalidades autenticadas.

### Testes Mobile

Incluem validações como:

* login;
* registro;
* persistência de sessão;
* dashboard;
* listagem de detritos;
* detalhes de detrito;
* favoritos;
* simulação de missão;
* histórico;
* tema dark/light;
* erro de conexão com API.

Objetivo: validar a experiência do usuário e a integração com o backend.

### Testes de SSE

Incluem validações como:

* criação de sessão;
* conexão com stream;
* recebimento de heartbeat;
* recebimento de debris_update;
* recebimento de conjunction_alert;
* encerramento com session_complete;
* comportamento em caso de falha de conexão.

Objetivo: validar o fluxo de simulação em tempo real.

### Testes de Tratamento de Erro

Incluem validações como:

* erro de validação;
* erro de autenticação;
* erro de autorização;
* erro de recurso não encontrado;
* erro de domínio;
* erro inesperado;
* envelope padrão de erro com `error`, `message` e `timestamp`.

Objetivo: garantir respostas consistentes e rastreáveis em caso de falha.

---

## Compliance e Boas Práticas

A documentação considera práticas relacionadas a segurança, organização e rastreabilidade.

### Segurança

* Uso de JWT para autenticação.
* Uso de refresh token.
* Separação de permissões por papel de usuário.
* Proteção de dados sensíveis.
* Não versionamento de secrets.
* Armazenamento seguro de tokens no mobile.

### Rastreabilidade

* Registro de histórico de missões.
* Organização dos documentos de arquitetura.
* Relacionamento entre requisitos, componentes e evidências.

### Observabilidade

* Uso de Aspire Dashboard.
* OpenTelemetry.
* Health checks.
* Logs e traces da aplicação.

### Manutenibilidade

* Separação entre controllers, services, repositories e DTOs.
* Separação entre backend e mobile.
* Documentação dos componentes principais.
* Organização por camadas arquiteturais.

### Padronização

* API REST.
* JSON padronizado.
* Uso de DTOs.
* Tratamento global de exceções.
* Estrutura documentada em ArchiMate.

---

## Arquivos da Entrega

A pasta `docs/testing-qa/` contém os arquivos relacionados à entrega da disciplina.

| Arquivo                                | Descrição                                            |
| -------------------------------------- | ---------------------------------------------------- |
| `README.md`                            | Documento de apresentação da entrega no GitHub       |
| `GS_TESTING_QA_DOCUMENTO_UNICO.md`     | Documento principal em formato editável              |
| `GS_TESTING_QA_DOCUMENTO_UNICO.pdf`    | Documento principal em PDF                           |
| `Mission_Clear_Testing_QA.archimate`   | Arquivo editável criado no Archi                     |
| `Mission_Clear_Diagrama_ArchiMate.pdf` | Diagrama ArchiMate exportado em PDF                  |
| `ARCHIMATE_ROTEIRO.md`                 | Roteiro utilizado para montagem do diagrama no Archi |
| `TESTING_QA_CHECKLIST.md`              | Checklist de testes, compliance e qualidade          |
| `MATRIZ_REQUISITOS_QUALIDADE.md`       | Matriz de requisitos, qualidade e riscos             |

---

## Estrutura Recomendada no Repositório

```text
docs/
└── testing-qa/
    ├── README.md
    ├── GS_TESTING_QA_DOCUMENTO_UNICO.md
    ├── GS_TESTING_QA_DOCUMENTO_UNICO.pdf
    ├── Mission_Clear_Testing_QA.archimate
    ├── Mission_Clear_Diagrama_ArchiMate.pdf
    ├── ARCHIMATE_ROTEIRO.md
    ├── TESTING_QA_CHECKLIST.md
    └── MATRIZ_REQUISITOS_QUALIDADE.md
```

---

## Entrega no Teams

Para a entrega oficial no Teams, devem ser enviados os arquivos finais da atividade:

```text
GS_TESTING_QA_DOCUMENTO_UNICO.pdf
Mission_Clear_Testing_QA.archimate
Mission_Clear_Diagrama_ArchiMate.pdf
```

O documento principal deve conter:

* nome da matéria;
* nome do projeto;
* nomes e RMs dos integrantes;
* links dos repositórios;
* link do vídeo pitch;
* breve descritivo do projeto;
* visão da arquitetura;
* arquitetura de negócio;
* arquitetura de aplicação/sistema;
* arquitetura de dados;
* arquitetura de tecnologia;
* estratégia de Testing, Compliance & Quality Assurance.

---

## Status da Entrega

| Item                             | Status                           |
| -------------------------------- | -------------------------------- |
| Documento principal              | Concluído                        |
| Diagrama ArchiMate               | Concluído                        |
| Arquivo `.archimate`             | Concluído                        |
| PDF do diagrama                  | Concluído                        |
| README da documentação           | Concluído                        |
| Checklist de QA                  | Concluído                        |
| Matriz de requisitos e qualidade | Concluído                        |
| Vídeo pitch                      | Inserir link após publicação     |
| Link do vídeo no documento final | Pendente até publicação do vídeo |

---

## Observação Final

O arquivo `.archimate` representa o modelo editável criado no Archi.

O arquivo `Mission_Clear_Diagrama_ArchiMate.pdf` representa a visualização do diagrama completo.

O arquivo `GS_TESTING_QA_DOCUMENTO_UNICO.pdf` representa o documento principal da entrega.

O link do vídeo pitch deve ser inserido no README e no documento principal antes da entrega final.
