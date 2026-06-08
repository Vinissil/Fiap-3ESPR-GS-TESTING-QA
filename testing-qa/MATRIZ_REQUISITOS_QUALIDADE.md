# Matriz de Requisitos e Qualidade - Mission Clear

## 1. Objetivo da matriz

Esta matriz conecta requisitos funcionais, requisitos não funcionais, componentes da solução, evidências esperadas e critérios de qualidade. O objetivo é facilitar a rastreabilidade da entrega de **Testing, Compliance & Quality Assurance**.

---

## 2. Requisitos funcionais

| Código | Requisito | Componente relacionado | Evidência esperada | Critério de aceite |
|---|---|---|---|---|
| RF01 | Consultar status da API. | `/api/status` | Print do endpoint. | Retorna `loading` ou `ready`. |
| RF02 | Listar destinos de missão. | `/api/destinations` | Resposta JSON. | Retorna destinos disponíveis. |
| RF03 | Listar detritos espaciais. | `/api/debris` | Resposta JSON. | Retorna lista de objetos orbitais. |
| RF04 | Exibir estatísticas de detritos. | `/api/debris/stats` | Print/resposta do endpoint. | Retorna estatísticas agregadas. |
| RF05 | Consultar detalhe de detrito. | `/api/debris/{id}` | Resposta do endpoint. | Retorna objeto solicitado ou erro controlado. |
| RF06 | Calcular janelas de lançamento. | LaunchWindowService | Resposta JSON. | Retorna slots com `risk_score`. |
| RF07 | Retornar melhores janelas. | `/api/launch-windows/best` | Resposta JSON. | Ordena por menor risco. |
| RF08 | Simular missão estática. | `/api/mission/simulate` | Print da resposta. | Retorna resultado imediato. |
| RF09 | Criar sessão dinâmica. | `/api/mission/session` | ID da sessão. | Sessão criada com sucesso. |
| RF10 | Transmitir eventos SSE. | `/api/mission/session/{id}/stream` | Print do stream/tela. | Eventos recebidos pelo cliente. |
| RF11 | Autenticar usuário. | AuthService/JwtService | Resposta de login. | Tokens retornados para credenciais válidas. |
| RF12 | Renovar token. | `/api/auth/refresh` | Resposta da API. | Novo access token retornado. |
| RF13 | Encerrar sessão. | `/api/auth/logout` | Resposta da API. | Refresh token invalidado. |
| RF14 | Exibir dashboard. | Mobile App/Dashboard Module | Print da tela. | Status, estatísticas ou alertas aparecem. |
| RF15 | Salvar histórico de missão. | MissionService/MySQL | Consulta do histórico. | Missão aparece para usuário autenticado. |
| RF16 | Persistir favoritos no mobile. | AsyncStorage/Favorites Module | Teste funcional. | Favorito permanece após reabrir o app. |

---

## 3. Requisitos não funcionais

| Código | Requisito | Justificativa | Componente relacionado | Como validar |
|---|---|---|---|---|
| RNF01 | Segurança com JWT. | Controlar acesso às rotas protegidas. | AuthService/JwtService | Testar acesso com e sem token. |
| RNF02 | Refresh token. | Permitir renovação segura da sessão. | AuthService/MySQL | Testar refresh válido e inválido. |
| RNF03 | Hash de senha com BCrypt. | Evitar senha em texto puro. | AuthService/User | Conferir armazenamento e login. |
| RNF04 | Tratamento global de exceções. | Padronizar respostas de erro. | GlobalExceptionMiddleware | Forçar erro e validar envelope. |
| RNF05 | Observabilidade. | Monitorar logs, traces e health checks. | OpenTelemetry/Aspire | Print do Aspire Dashboard. |
| RNF06 | Persistência segura no mobile. | Proteger tokens no dispositivo. | SecureStore | Conferir uso para tokens. |
| RNF07 | Separação por camadas. | Melhorar manutenção e testes. | Controllers/Services/Repositories | Revisão estrutural. |
| RNF08 | Testabilidade dos services. | Permitir testes unitários. | MissionClear.Tests | Executar testes. |
| RNF09 | JSON em `snake_case`. | Padronizar contrato da API. | DTOs/System.Text.Json | Validar respostas JSON. |
| RNF10 | Dados reais da CelesTrak. | Aumentar aderência ao problema. | TleIngestionService | Validar consumo HTTP. |
| RNF11 | Integração com MySQL. | Persistir usuários e missões. | EF Core/MySQL | Validar migrations e consultas. |
| RNF12 | Comunicação REST/SSE. | Suportar consumo mobile e stream. | API/Mobile | Testar endpoints e sessão dinâmica. |

---

## 4. Constraints

| Código | Restrição | Impacto na arquitetura | Como aparece no projeto |
|---|---|---|---|
| C01 | Backend em .NET. | Define runtime, Controllers e DI. | ASP.NET Core e .NET Aspire. |
| C02 | Mobile em React Native/Expo. | Define app multiplataforma e Expo. | Estrutura `src/` mobile. |
| C03 | Banco MySQL. | Define persistência relacional. | MySQL 8 + EF Core/Pomelo. |
| C04 | Uso da CelesTrak. | Requer integração HTTP externa. | TleIngestionService. |
| C05 | Uso de SGP4 por biblioteca. | Evita implementação manual de propagação. | OrbitalEngineService. |
| C06 | JWT e roles. | Define autenticação e autorização. | AuthController/JwtService. |
| C07 | SSE. | Define simulação dinâmica. | Mission Session Stream. |
| C08 | Aspire/OpenTelemetry. | Define observabilidade. | AppHost/ServiceDefaults. |
| C09 | Entrega no Teams. | Define documentos e arquivos obrigatórios. | Documento único, vídeo, `.archimate` e PDF. |

---

## 5. Matriz de qualidade

| Qualidade | Aplicação no Mission Clear | Evidência | Risco se não atender |
|---|---|---|---|
| Segurança | JWT, refresh token, BCrypt, roles. | Testes de autenticação. | Acesso indevido ou exposição de dados. |
| Confiabilidade | Tratamento de erros e health checks. | Respostas padronizadas e Aspire. | Falhas não controladas. |
| Manutenibilidade | Camadas separadas e DTOs. | Estrutura do projeto. | Dificuldade de evolução. |
| Testabilidade | Services isoláveis e projeto de testes. | `dotnet test`. | Baixa confiança em alterações. |
| Usabilidade | App mobile com dashboard e navegação. | Prints do app. | Usuário não compreende os dados. |
| Observabilidade | OpenTelemetry/Aspire. | Print do dashboard. | Falhas difíceis de investigar. |
| Rastreabilidade | Histórico de missões e matriz de requisitos. | Histórico e documentação. | Dificuldade de auditoria. |
| Interoperabilidade | REST, JSON e SSE. | Consumo pelo app mobile. | Integração instável. |

---

## 6. Riscos e mitigação

| Risco | Impacto | Mitigação | Teste relacionado |
|---|---|---|---|
| Falha ao carregar dados da CelesTrak. | API pode não ter dados orbitais atualizados. | Tratar erro e indicar status adequado. | Teste de integração API + CelesTrak. |
| Token inválido ou expirado. | Usuário perde acesso ou acessa indevidamente. | Refresh token e bloqueio de rotas protegidas. | Testes de autenticação. |
| Falha mobile/backend. | App não exibe dados. | Mensagem de erro e tratamento no Axios. | Testes mobile com API indisponível. |
| Erro no stream SSE. | Simulação dinâmica interrompida. | Encerrar stream com erro controlado. | Testes SSE. |
| Dados orbitais indisponíveis. | Cálculo de risco prejudicado. | Exibir status e impedir cálculo inválido. | Teste de `/api/status`. |
| Banco MySQL indisponível. | Usuários e histórico indisponíveis. | Tratamento de erro e logs. | Teste de falha de banco. |
| Usuário sem permissão acessa recurso restrito. | Risco de segurança. | Roles e autorização no backend. | Teste 403/rota protegida. |
| Secrets versionados por engano. | Exposição de credenciais. | Não versionar arquivos locais sensíveis. | Revisão de repositório. |
| Diagrama ArchiMate incompleto. | Perda de nota na entrega de arquitetura. | Usar checklist do roteiro. | Conferência antes do Teams. |

---

## 7. Requisitos ligados aos critérios do professor

| Critério da entrega | Evidência no pacote |
|---|---|
| Breve descritivo do projeto | Documento único, Seção 2. |
| Visão da arquitetura TOGAF | Documento único, Seção 3. |
| Arquitetura de negócio | Documento único, Seção 4. |
| Arquitetura de sistema | Documento único, Seção 5. |
| Arquitetura de tecnologia | Documento único, Seção 6. |
| Uso do Archi/ArchiMate | `ARCHIMATE_ROTEIRO.md`, `.archimate` e PDF a serem gerados. |
| Vídeo pitch | Link a inserir no documento único. |
| Documento único | `GS_TESTING_QA_DOCUMENTO_UNICO.md` e PDF gerado. |
| Nome e RM dos integrantes | Documento único, Seção 1. |
