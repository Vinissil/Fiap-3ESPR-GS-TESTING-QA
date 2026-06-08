# GS - Testing, Compliance & Quality Assurance

## Mission Clear — Monitoramento de Detritos Espaciais e Simulação de Missões LEO Seguras

Documentação da entrega da disciplina **Testing, Compliance & Quality Assurance**, referente à **Global Solution 2026 — FIAP**.

O projeto **Mission Clear** tem como objetivo apoiar a segurança de missões em órbita baixa terrestre, utilizando dados de detritos espaciais, simulação de risco orbital e análise de janelas de lançamento mais seguras.

---

## Integrantes

| Nome | RM |
|---|---|
| Gustavo Bezerra Assumção | RM 553076 |
| Jó Sales | RM 552679 |
| Miguel Garcez de Carvalho | RM 553768 |
| Vinicius Souza e Silva | RM 552781 |
| Edson Leonardo | RM 553737 |

---

## Links do Projeto

### Repositório Backend

https://github.com/FIAP-BitsNBytes/Fiap-3ESPR-GS-C

### Repositório Mobile

https://github.com/FIAP-BitsNBytes/Fiap-3ESPR-GS-Mobile

### Vídeo Pitch

**PENDENTE:** inserir aqui o link do YouTube publicado como **não listado**.

---

## Descrição do Projeto

O **Mission Clear** é uma solução tecnológica voltada ao monitoramento de detritos espaciais e à simulação de missões orbitais em órbita baixa terrestre, conhecida como LEO.

O problema abordado pelo projeto é o risco de colisão entre missões espaciais e detritos orbitais, como fragmentos de satélites, estágios de foguetes e objetos resultantes de colisões anteriores. Esses objetos podem cruzar a trajetória de uma missão em alta velocidade, tornando necessária uma análise prévia de risco.

A solução utiliza dados orbitais reais, processa informações de detritos espaciais, calcula riscos de conjunção e apresenta janelas de lançamento com menor risco para o destino escolhido. O sistema também permite simulação de missões, acompanhamento de alertas e consulta de informações orbitais por meio de uma aplicação mobile.

---

## Arquitetura da Solução

A arquitetura foi documentada seguindo uma organização inspirada no padrão TOGAF, com representação em ArchiMate.

A solução foi dividida em quatro camadas principais:

### 1. Camada de Negócio

- Operador de missão.
- Pesquisador.
- Administrador.
- Processo de simulação de missão orbital segura.
- Resultado esperado: janela de lançamento recomendada.

### 2. Camada de Aplicação

- Aplicativo mobile Mission Clear.
- API Mission Clear.
- Serviço de autenticação.
- Serviço de motor orbital.
- Serviço de ingestão de TLEs.
- Serviço de cálculo de janelas de lançamento.
- Detector de conjunções.
- Serviço de sessão de missão.

### 3. Camada de Dados

- Usuários.
- Tokens de autenticação.
- Missões.
- Sessões de missão.
- Objetos orbitais.
- Janelas de lançamento.
- Alertas de conjunção.
- Banco de dados MySQL.

### 4. Camada de Tecnologia

- Smartphone ou emulador.
- Servidor backend .NET.
- Servidor MySQL.
- Internet.
- CelesTrak API.
- Biblioteca SGP4.
- Aspire Dashboard.

---

## Tecnologias Utilizadas

### Backend

- .NET / ASP.NET Core
- API REST
- MySQL
- Entity Framework Core
- JWT e Refresh Token
- SGP4
- Server-Sent Events
- OpenTelemetry
- Aspire Dashboard
- xUnit

### Mobile

- React Native
- Expo
- TypeScript
- Axios
- AsyncStorage
- SecureStore
- Context API
- React Navigation

### Documentação e Arquitetura

- Archi
- ArchiMate
- TOGAF
- Markdown
- PDF

---

## Testing, Compliance & Quality Assurance

A documentação de QA do projeto contempla a análise de qualidade da solução, considerando testes, segurança, rastreabilidade, observabilidade e organização arquitetural.

Foram considerados os seguintes grupos de validação:

- Testes unitários.
- Testes de integração.
- Testes de API.
- Testes de autenticação.
- Testes de autorização por perfil de usuário.
- Testes mobile.
- Testes de Server-Sent Events.
- Testes de tratamento de erro.
- Testes de regressão.
- Critérios de aceite.
- Compliance e boas práticas de segurança.

---

## Arquivos desta Pasta

| Arquivo | Descrição |
|---|---|
| `README.md` | Resumo da documentação da disciplina no repositório |
| `GS_TESTING_QA_DOCUMENTO_UNICO.md` | Documento principal em formato editável |
| `GS_TESTING_QA_DOCUMENTO_UNICO.pdf` | Documento principal em PDF |
| `Mission_Clear_Testing_QA.archimate` | Arquivo editável do Archi/ArchiMate |
| `Mission_Clear_Diagrama_ArchiMate.pdf` | PDF do diagrama de arquitetura |
| `ARCHIMATE_ROTEIRO.md` | Roteiro usado para montar o diagrama no Archi |
| `TESTING_QA_CHECKLIST.md` | Checklist de testes, qualidade e compliance |
| `MATRIZ_REQUISITOS_QUALIDADE.md` | Matriz de requisitos, critérios de qualidade e riscos |

---

## Entrega no Teams

Para a entrega final no Teams, os arquivos essenciais são:

```text
GS_TESTING_QA_DOCUMENTO_UNICO.pdf
Mission_Clear_Testing_QA.archimate
Mission_Clear_Diagrama_ArchiMate.pdf
```

O documento principal deve conter:

- Nome da matéria.
- Nome do projeto.
- Nome e RM dos integrantes.
- Links dos repositórios.
- Link do vídeo pitch.
- Breve descritivo do projeto.
- Arquitetura TOGAF.
- Arquitetura de negócio.
- Arquitetura de sistema.
- Arquitetura de tecnologia.
- Estratégia de Testing, Compliance & Quality Assurance.
- Referência ao arquivo ArchiMate e ao PDF do diagrama.

---

## Observação Final

O arquivo `.archimate` representa o modelo editável criado no Archi.

O arquivo `Mission_Clear_Diagrama_ArchiMate.pdf` representa a versão visual do diagrama para conferência e leitura.

O documento `GS_TESTING_QA_DOCUMENTO_UNICO.pdf` é o documento principal que consolida a entrega da disciplina.
