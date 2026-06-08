# Checklist de Testing, Compliance & Quality Assurance - Mission Clear

## 1. Objetivo

Este checklist serve para validar qualidade, segurança, conformidade, funcionamento e evidências da solução **Mission Clear**. Ele cobre backend, mobile, autenticação, API, SSE, banco de dados, tratamento de erros e documentação de entrega.

---

## 2. Testes unitários

| Item testado | Objetivo do teste | Resultado esperado | Prioridade |
|---|---|---|---|
| AuthService | Validar cadastro, login e regras de credencial. | Usuário válido autentica; inválido é recusado. | Crítica |
| JwtService | Validar geração e expiração de tokens. | Access token e refresh token emitidos conforme regra. | Crítica |
| LaunchWindowService | Validar cálculo de janelas em slots e risk_score. | Janelas retornadas com classificação coerente. | Crítica |
| ConjunctionDetector | Validar identificação de aproximação perigosa. | Alertas gerados quando houver risco definido no projeto. | Crítica |
| OrbitalEngineService | Validar integração lógica com SGP4. | Retorno de posição, altitude e velocidade sem erro. | Alta |
| MissionSessionService | Validar criação, atualização e finalização de sessão. | Sessão executa fluxo e encerra corretamente. | Alta |
| MissionService | Validar simulação e registro de histórico. | Missão simulada e persistida quando aplicável. | Alta |
| UserService | Validar consulta e atualização de perfil. | Dados do usuário autenticado retornados corretamente. | Média |

---

## 3. Testes de integração

| Integração | Objetivo | Resultado esperado | Prioridade |
|---|---|---|---|
| API + MySQL | Validar conexão, migrations e consultas. | Dados gravados e lidos sem inconsistência. | Crítica |
| Repositories + EF Core | Validar mapeamento de Entities. | Repositories retornam dados corretos. | Alta |
| API + CelesTrak | Validar consumo dos dados orbitais externos. | Dados carregados ou erro tratado adequadamente. | Alta |
| API + OrbitalCache | Validar cache carregado e disponível. | `/api/status` indica estado adequado. | Alta |
| API + Serviços internos | Validar DI entre Controllers, Services e Repositories. | Requisições atravessam camadas sem falha. | Alta |
| API + SSE | Validar transmissão de eventos da sessão. | Eventos recebidos até encerramento da simulação. | Alta |
| Mobile + API | Validar consumo real dos endpoints. | App apresenta dados ou erro controlado. | Alta |

---

## 4. Testes de API

| Endpoint | Validação | Resultado esperado |
|---|---|---|
| GET `/api/status` | API disponível e estado dos TLEs. | Retorna `loading` ou `ready`. |
| GET `/api/destinations` | Destinos de missão. | Retorna ISS, LEO genérica e/ou SSO conforme backend. |
| GET `/api/debris` | Listagem de detritos. | Retorna coleção de objetos orbitais. |
| GET `/api/debris/stats` | Estatísticas. | Retorna agregações por tipo/faixa. |
| GET `/api/debris/{id}` | Detalhe do objeto. | Retorna dados do NORAD ID solicitado ou 404. |
| GET `/api/launch-windows` | Geração de janelas. | Retorna slots de lançamento com risco. |
| GET `/api/launch-windows/best` | Melhores janelas. | Retorna janelas ordenadas por menor risco. |
| POST `/api/mission/simulate` | Simulação estática. | Retorna resultado imediato. |
| POST `/api/mission/session` | Sessão dinâmica. | Retorna identificador da sessão. |
| GET `/api/mission/session/{id}/stream` | SSE. | Retorna stream de eventos. |
| POST `/api/mission/session/{id}/complete` | Encerrar sessão. | Sessão finalizada e salva se aplicável. |
| POST `/api/auth/register` | Cadastro. | Usuário criado com role padrão. |
| POST `/api/auth/login` | Login. | Access token e refresh token retornados. |
| POST `/api/auth/refresh` | Renovação. | Novo access token gerado. |
| POST `/api/auth/logout` | Logout. | Refresh token invalidado. |
| GET `/api/users/me` | Perfil. | Dados do usuário autenticado. |
| PUT `/api/users/me` | Atualização de perfil. | Dados atualizados com validação. |
| GET `/api/missions` | Histórico. | Lista paginada de missões do usuário. |
| GET `/api/missions/{id}` | Detalhe da missão. | Retorna missão específica ou 404. |
| GET `/api/missions/stats` | Estatísticas de missões. | Retorna dados agregados do usuário. |
| DELETE `/api/missions/{id}` | Exclusão conforme permissão. | Respeita regra de autorização. |
| GET `/api/dashboard/summary` | Dashboard. | Retorna resumo operacional. |
| GET `/api/dashboard/alerts` | Alertas. | Retorna alertas ativos. |

---

## 5. Testes de autenticação e autorização

| Cenário | Resultado esperado | Prioridade |
|---|---|---|
| Cadastro com dados válidos | Usuário criado. | Alta |
| Cadastro com e-mail já usado | Erro controlado. | Alta |
| Login válido | Tokens emitidos. | Crítica |
| Login inválido | Acesso negado sem expor dados sensíveis. | Crítica |
| Access token expirado | Requisição protegida recusada ou renovada com refresh. | Crítica |
| Refresh token válido | Novo access token emitido. | Crítica |
| Refresh token inválido/expirado | Sessão recusada. | Crítica |
| Logout | Refresh token invalidado. | Alta |
| Rota protegida sem token | Acesso bloqueado. | Crítica |
| Usuário Researcher | Acessa apenas recursos permitidos. | Alta |
| Usuário Administrator | Acessa recursos administrativos previstos. | Alta |
| Researcher tentando ação restrita | Retorno 403 ou bloqueio equivalente. | Alta |

---

## 6. Testes mobile

| Área | Teste | Resultado esperado |
|---|---|---|
| Autenticação | Login e registro. | Usuário acessa fluxo autenticado. |
| Sessão | Fechar e reabrir o app. | Sessão preservada quando token válido. |
| Dashboard | Carregar status, gráficos e alertas. | Dados exibidos ou erro tratado. |
| Detritos | Listar e consultar detalhes. | Informações orbitais exibidas corretamente. |
| Favoritos | Adicionar/remover favorito. | Persistência local funcionando. |
| Simulação | Escolher destino e iniciar simulação. | Resultado apresentado ao usuário. |
| SSE | Acompanhar stream. | Eventos recebidos em tempo real. |
| Histórico | Consultar missões. | Lista aparece para usuário autenticado. |
| Tema | Alternar dark/light mode. | Preferência aplicada e persistida. |
| Erro de conexão | API indisponível. | App não trava e informa falha. |
| Token expirado | Requisição autenticada após expiração. | Interceptor tenta refresh ou direciona ao login. |

---

## 7. Testes SSE

| Evento/fluxo | Validação | Resultado esperado |
|---|---|---|
| Criação de sessão | POST cria sessão dinâmica. | Retorna ID de sessão. |
| Abertura de stream | App conecta no endpoint SSE. | Conexão estabelecida. |
| `heartbeat` | Manutenção da conexão. | Evento recebido periodicamente. |
| `debris_update` | Atualização de detritos próximos. | Dados recebidos pelo app. |
| `conjunction_alert` | Alerta sob demanda. | Alerta exibido quando houver risco. |
| `session_complete` | Encerramento da sessão. | Stream finaliza corretamente. |
| Falha de rede | Interrupção de stream. | App exibe erro ou tenta reconectar. |

---

## 8. Testes de tratamento de erro

| Tipo de erro | Validação | Resultado esperado |
|---|---|---|
| Validação de entrada | Payload incompleto ou inválido. | Erro claro e controlado. |
| Autenticação | Token ausente/inválido. | Retorno 401 ou equivalente. |
| Autorização | Usuário sem permissão. | Retorno 403 ou equivalente. |
| Recurso não encontrado | ID inexistente. | Retorno 404 ou equivalente. |
| Erro de domínio | Regra de negócio violada. | Envelope `{ error, message, timestamp }`. |
| Falha CelesTrak | Serviço externo indisponível. | Erro tratado sem travar API. |
| Falha MySQL | Banco indisponível. | Erro controlado e logado. |
| Erro inesperado | Exceção não prevista. | Sem stack trace exposto ao cliente. |

---

## 9. Testes de compliance

| Item | Validação esperada |
|---|---|
| Proteção de tokens | Tokens não aparecem em logs, tela ou mensagens de erro. |
| SecureStore | Tokens armazenados no mobile em armazenamento seguro. |
| AsyncStorage | Usado apenas para preferências/favoritos e dados não sensíveis. |
| Senhas | Nunca armazenar senha em texto puro. |
| Secrets | Não versionar `appsettings.Development.json` com segredos reais. |
| Roles | Separação entre Researcher e Administrator respeitada. |
| Logs | Logs úteis para auditoria, sem expor credenciais. |
| Histórico | Missões salvas associadas ao usuário correto. |
| Padronização de erros | Erros retornam envelope padronizado. |
| GitHub | Repositório não deve conter dados sensíveis. |

---

## 10. Critérios de aceite

A entrega pode ser considerada adequada quando:

- [ ] o backend executa sem erro crítico;
- [ ] a API responde aos endpoints principais;
- [ ] o app mobile consegue consumir a API;
- [ ] autenticação, refresh e logout funcionam;
- [ ] a simulação de missão funciona;
- [ ] o stream SSE é demonstrado ou documentado com evidência;
- [ ] o dashboard apresenta dados ou mensagens de erro controladas;
- [ ] os testes principais foram executados;
- [ ] o diagrama foi montado no Archi;
- [ ] o arquivo `.archimate` foi salvo;
- [ ] o PDF do diagrama foi exportado;
- [ ] o documento único contém link do vídeo, nomes e RMs.

---

## 11. Matriz de criticidade

| Criticidade | Exemplos | Tratamento |
|---|---|---|
| Crítica | Login, JWT, simulação, SSE, banco, cálculo de risco. | Deve funcionar para entrega segura. |
| Alta | Dashboard, histórico, favoritos, ingestão CelesTrak. | Deve ser validado com evidência. |
| Média | Tema visual, filtros, detalhes complementares. | Pode ter ajustes menores. |
| Baixa | Melhorias visuais e textos auxiliares. | Não deve impedir entrega. |

---

## 12. Evidências esperadas

| Evidência | Arquivo/print sugerido |
|---|---|
| API rodando | Print do terminal ou navegador em `/api/status`. |
| Testes backend | Print do `dotnet test`. |
| Aspire Dashboard | Print do dashboard com serviços ativos. |
| App mobile | Prints de dashboard, detritos, simulação e histórico. |
| Autenticação | Print de login ou resposta da API. |
| SSE | Print de stream/eventos ou tela da simulação. |
| Diagrama | PDF exportado do Archi. |
| Arquivo fonte | `.archimate`. |
| Vídeo pitch | Link do YouTube não listado no documento. |
