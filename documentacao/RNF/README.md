# 🛡️ Requisitos Não Funcionais - Sedatines

Este documento define as restrições técnicas, padrões de qualidade e exigências de infraestrutura do projeto.

**Índice:**
- [1. Tecnologias e Stack](#1-tecnologias-e-stack-restrições-de-implementação)
- [2. Usabilidade e Interface](#2-usabilidade-e-interface-uxui)
- [3. Segurança e Proteção de Dados](#3-segurança-e-proteção-de-dados)
- [4. Confiabilidade e Infraestrutura](#4-confiabilidade-e-infraestrutura)
- [5. Arquitetura e Qualidade de Código](#5-arquitetura-e-qualidade-de-código)
- [6. Desempenho](#6-desempenho)
- [7. Voltar para o Índice da Documentação](../README.md)


> **Legenda de Prioridade:**
> * **Crítica:** O sistema não pode ser implantado sem isso.
> * **Alta:** O sistema precisa ter para uma versão estável.
> * **Média:** Necessário para uma boa experiência, mas pode ficar para v1.1.
> * **Baixa:** Melhoria contínua / Diferencial.

---

## 1. Tecnologias e Stack (Restrições de Implementação)

| ID | Título | Descrição | Prioridade | Requisitos Relacionados |
| :--: | :----: | :-------- | :--------: | :---------------------: |
| **RNF001** | **Backend Framework** | O sistema deve ser desenvolvido em **PHP 8.4** utilizando o framework **Laravel 12**. | Alta | - |
| **RNF002** | **Banco de Dados** | O SGDB deve ser **MySQL 8.0**, utilizando charset **utf8mb4** e collation `utf8mb4_unicode_ci` para suporte total a caracteres especiais. | Crítica | - |
| **RNF003** | **Ambiente de Desenvolvimento** | O projeto deve ser containerizado utilizando **Docker** (via Laravel Sail) para garantir paridade entre dev e produção (SO Linux). | Alta | - |
| **RNF004** | **Renderização do Frontend** | A estrutura das páginas deve ser renderizada no servidor (SSR) utilizando **Blade Templates**. | Alta | - |
| **RNF005** | **Interações do Frontend** | As ações de usuário (formulários, filtros, likes) devem ser processadas via JavaScript assíncrono (AJAX/Fetch) para evitar recarregamentos. | Alta | - |
| **RNF006** | **Controle de Versão** | O código deve ser versionado no Git, seguindo o padrão **Conventional Commits** nas mensagens de commit. | Alta | - |
| **RNF007** | **CSS** | A interface deve ser construída utilizando o framework **Tailwind CSS** para agilidade e padronização. | Média | - |
| **RNF008** | **Servidor Web** | A aplicação deve ser servida via **Nginx** (containerizado). | Média | - |
| **RNF009** | **Gerenciamento de Dependências** | As bibliotecas devem ser gerenciadas via Composer/NPM com **Lock Files** (`composer.lock`) commitados obrigatoriamente para garantir integridade. | Crítica | - |
| **RNF010** | **Framework de Testes** | Testes automatizados (Unitários e de Feature) devem ser escritos utilizando **Pest PHP**. | Média | - |
| **RNF011** | **Gestão de Configuração** | Variáveis de ambiente sensíveis (senhas, chaves de API) devem ser geridas exclusivamente via arquivo `.env`, nunca hardcoded no código. | Crítica | RNF006 |
| **RNF012** | **Padronização de Código** | O estilo de código deve seguir a norma **PSR-12**, validado automaticamente pela ferramenta **Laravel Pint**. | Alta | - |
| **RNF013** | **Versionamento de Schema** | Toda alteração no banco de dados deve ser feita via **Migrations**. Dados iniciais e de teste devem ser inseridos via **Seeders**. | Crítica | RNF002 |


## 2. Usabilidade e Interface (UX/UI)

| ID | Título | Descrição | Prioridade | Requisitos Relacionados |
| :--: | :----: | :-------- | :--------: | :---------------------: |
| **RNF101** | **Responsividade** | O layout deve ser fluido e adaptável (Responsive Web Design), garantindo usabilidade em Mobile, Tablet e Desktop. | Alta | - |
| **RNF102** | **Identidade Visual (Tema)** | O sistema deve adotar o tema "Dark Mode" como padrão, alinhado à estética de terror/mistério do projeto. | Média | - |
| **RNF103** | **Preferência de Tema Inteligente** | O sistema deve permitir alternar temas (Claro/Escuro), respeitando inicialmente a preferência do SO e salvando a escolha manual no LocalStorage. | Baixa | RNF102 |
| **RNF104** | **Feedback de Sistema** | Ações de sucesso devem exibir notificações flutuantes (Toasts). Erros críticos devem exibir Alertas/Modais. | Alta | RNF005 |
| **RNF105** | **Acessibilidade Aprimorada** | Além de atributos `alt` e `labels`, a interface deve garantir contraste mínimo (WCAG AA) e ser navegável via teclado. | Média | - |
| **RNF106** | **Indicadores de Carregamento** | Toda requisição assíncrona (AJAX) deve exibir um indicador visual (Spinner ou Skeleton) para evitar a sensação de travamento. | Alta | RNF005 |
| **RNF107** | **Internacionalização (L10n)** | A interface deve estar em **Português do Brasil (PT-BR)**. Datas e moedas devem seguir o formato local (dd/mm/aaaa, R$). | Alta | - |
| **RNF108** | **Navegação Global** | Com exceção das páginas de Auth/Erro, todas as telas devem possuir barra de navegação consistente e indicação clara da página ativa. | Alta | - |
| **RNF109** | **Hierarquia Visual** | Botões de ação primária (Ex: "Salvar") devem ter destaque visual claro sobre secundários. | Média | - |
| **RNF110** | **Proteção contra Erros (Undo/Confirm)** | Ações irreversíveis (Exclusão) devem exigir confirmação dupla. Se possível, implementar "Undo" (Desfazer) via Toast. | Alta | - |
| **RNF111** | **Estados Vazios (Empty States)** | Quando uma listagem ou busca não retornar resultados, o sistema deve exibir uma mensagem amigável em vez de uma tela em branco. | Média | - |
| **RNF112** | **Performance de Imagens (Lazy Loading)** | Listagens de entidades devem implementar **Lazy Loading** (carregamento sob demanda) para economizar banda. | Alta | RF204 |

## 3. Segurança e Proteção de Dados

| ID | Título | Descrição | Prioridade | Requisitos Relacionados |
| :--: | :----: | :-------- | :--------: | :---------------------: |
| **RNF201** | **Criptografia de Senhas** | Nenhuma senha deve ser armazenada em texto plano. Deve-se utilizar hash forte (**Argon2id** ou Bcrypt). | Crítica | RF202 |
| **RNF202** | **Proteção CSRF** | Todos os formulários de escrita (POST/PUT/DELETE) devem conter tokens de proteção contra Cross-Site Request Forgery. | Crítica | - |
| **RNF203** | **Sanitização (XSS)** | Todo input de usuário exibido em tela (comentários, lore) deve ser sanitizado/escapado para prevenir injeção de scripts maliciosos. | Crítica | - |
| **RNF204** | **Segurança de Uploads** | O sistema deve aceitar apenas formatos de imagem seguros (**JPEG, PNG, WEBP, AVIF**) com tamanho máximo de **5MB**. Arquivos executáveis ou vetoriais (SVG) devem ser rejeitados. | Crítica | RF105 |
| **RNF205** | **Proteção de Rotas (Middleware)** | As rotas administrativas e restritas devem ser protegidas por Middlewares que validem a autenticação antes de carregar o controlador. | Crítica | RF307 |
| **RNF206** | **Autorização de Ação (Policies)** | O sistema deve validar via Policies/Gates se o usuário tem permissão específica para o recurso alvo (Ex: "Usuário X pode editar o Post Y?"). | Crítica | RF307 |
| **RNF207** | **Persistência de Login (Lembrar-me)** | O sistema deve gerenciar sessões estendidas (ex: 30 dias) via cookie seguro caso o usuário marque a opção "Lembrar-me" no login. | Média | RF201 |
| **RNF208** | **Armazenamento de Sessão** | Tokens de autenticação devem ser armazenados exclusivamente em **Cookies HttpOnly/Secure**. É proibido o uso de LocalStorage para dados sensíveis. | Crítica | RF201 |
| **RNF209** | **Identificação Pública (Obfuscação)** | As URLs públicas não devem expor o ID sequencial (PK) do banco. Deve-se utilizar **UUIDs** ou **Slugs** únicos para prevenir enumeração de dados. | Alta | RF112, RF207 |
| **RNF210** | **Protocolo Seguro (HTTPS)** | Toda a comunicação entre cliente e servidor deve ser criptografada utilizando protocolo HTTPS (TLS 1.2+). | Crítica | - |
| **RNF211** | **Rate Limiting (Throttling)** | As rotas de Login e API devem possuir limite de requisições por minuto para mitigar ataques de Força Bruta e DDoS. | Alta | RF201 |
| **RNF212** | **Política de Senhas** | As senhas devem ter no mínimo 8 caracteres, exigindo a presença de letras e números (Alfanumérica). | Alta | RF202 |
| **RNF213** | **Headers de Segurança** | O servidor deve responder com headers de segurança configurados: `X-Frame-Options`, `X-Content-Type-Options` e `HSTS`. | Alta | - |
| **RNF214** | **Armazenamento de Uploads** | Arquivos enviados não devem manter o nome original. O sistema deve renomeá-los usando um Hash único (UUID/MD5) para evitar sobrescrita e execução maliciosa. | Alta | RF105 |
| **RNF215** | **Sanitização de Logs** | Os logs do sistema (Laravel Logs) não devem registrar dados sensíveis como senhas em texto plano ou tokens de acesso. | Alta | RF301 |
| **RNF216** | **Bloqueio por Tentativas** | Após 5 tentativas falhas de login consecutivas, o IP ou Usuário deve ser bloqueado temporariamente (Ex: 1 minuto) na camada de autenticação. | Alta | RF201 |

## 4. Confiabilidade e Infraestrutura

| ID | Título | Descrição | Prioridade | Requisitos Relacionados |
| :--: | :----: | :-------- | :--------: | :---------------------: |
| **RNF301** | **Rotina de Backup** | O sistema deve possuir uma rotina automatizada (Laravel Scheduler) para backup diário do banco de dados MySQL. | Alta | - |
| **RNF302** | **Páginas de Erro Customizadas** | O sistema deve tratar exceções HTTP (404, 403, 500) apresentando páginas amigáveis dentro do tema visual, sem expor Stack Traces (debug) em produção. | Baixa | - |
| **RNF303** | **Timeout de Requisições** | O servidor web (Nginx/PHP) deve ter um timeout configurado (ex: 60s) para evitar que processos travados consumam recursos indefinidamente. | Média | - |
| **RNF304** | **Health Check Endpoint** | O sistema deve expor um endpoint `/up` (nativo do Laravel 11+) para monitoramento externo de uptime e saúde da conexão com o banco. | Média | - |

## 5. Arquitetura e Qualidade de Código

| ID | Título | Descrição | Prioridade | Requisitos Relacionados |
| :--: | :----: | :-------- | :--------: | :---------------------: |
| **RNF401** | **Padrão de Arquitetura (MVC)** | O projeto deve seguir o padrão MVC. Lógica complexa deve ser movida para **Service Classes**, mantendo os Controllers limpos. | Alta | - |
| **RNF402** | **Validação Centralizada** | Toda validação de input deve ser feita através de **Form Requests** dedicados, proibindo validações manuais no Controller. | Alta | - |
| **RNF403** | **Tratamento Global de Exceções** | O sistema não deve "quebrar" na cara do usuário. Erros devem ser capturados e exibidos de forma amigável (Flash Messages). | Média | - |
| **RNF404** | **Padronização de Mensagens** | As mensagens de erro e sucesso devem seguir um padrão textual e visual consistente. | Média | - |
| **RNF405** | **Testes Automatizados (Pest)** | Implementar testes automatizados para as funcionalidades críticas (ex: Cadastro de Entidade), focando no "Caminho Feliz". | Média | - |
| **RNF406** | **Análise Estática (Linting)** | O código deve ser validado por ferramentas de análise estática (**Laravel Pint**) para garantir estilo PSR-12. | Alta | - |
| **RNF407** | **Pipeline CI/CD** | Configurar um workflow básico no GitHub Actions que execute os testes e a análise estática a cada Push. | Baixa | - |
| **RNF408** | **Verificação de Segurança** | Rodar ocasionalmente `composer audit` para verificar dependências vulneráveis. | Baixa | - |
6
## 6. Desempenho

| ID | Título | Descrição | Prioridade | Requisitos Relacionados |
| :--: | :----: | :-------- | :--------: | :---------------------: |
| **RNF501** | **Otimização de Imagens** | Imagens enviadas devem ser processadas no servidor (Intervention Image) para redimensionamento e conversão para formatos leves (**WebP**) antes do armazenamento. | Alta | RNF204 |
| **RNF502** | **Paginação / Carregamento sob Demanda** | Listagens extensas devem implementar paginação no backend e **Infinite Scroll** (ou "Carregar Mais") no frontend. | Alta | RNF005 |
| **RNF503** | **Tempo de Resposta (SLA)** | O tempo de processamento do servidor (TTFB) deve ser inferior a 500ms, e o carregamento visual completo (LCP) não deve exceder 2 segundos em 4G. | Média | - |
| **RNF504** | **Prevenção de N+1 (Eager Loading)** | Todas as consultas Eloquent que carregam relacionamentos devem utilizar **Eager Loading** (`with()`) para evitar múltiplas consultas ao banco. | Alta | - |
| **RNF505** | **Indexação de Banco de Dados** | Colunas utilizadas frequentemente em filtros, buscas (`WHERE`, `LIKE`) e ordenações (`ORDER BY`) devem possuir índices criados via Migration. | Alta | RF013 |
| **RNF506** | **Cache de Dados (Backend)** | Informações que mudam raramente (Configurações, Categorias) devem ser armazenadas em Cache (Redis ou File) com TTL definido. | Média | - |
| **RNF507** | **Minificação de Assets** | Em produção, arquivos CSS e JS devem ser minificados e versionados automaticamente pelo build (**Vite**). | Alta | - |
| **RNF508** | **Processamento Assíncrono (Queues)** | Tarefas pesadas (Processamento de Imagens, Envio de Emails) devem ser enviadas para filas (**Laravel Queues**) e processadas em background, nunca na requisição do usuário. | Crítica | RNF501, RF303 |
| **RNF509** | **Otimização de Queries (Select)** | Consultas devem selecionar apenas as colunas necessárias (`select('id', 'name')`) em vez de trazer o registro completo (`select *`), economizando memória. | Média | - |
| **RNF510** | **Otimização de Input (Debounce)** | Campos de busca e filtros devem implementar **Debounce** (atraso na execução) de ~300ms para evitar disparar requisições a cada tecla digitada. | Alta | RNF005 |
| **RNF511** | **Cache HTTP (Browser Caching)** | O servidor deve enviar headers de cache (`Cache-Control`, `ETag`) para recursos estáticos e respostas públicas para reduzir tráfego de rede. | Média | - |
| **RNF512** | **Testes de Carga** | Realizar testes de estresse básicos (ex: ferramenta K6 ou JMeter) para validar se a aplicação suporta concorrência sem degradar o tempo de resposta (RNF503). | Baixa | - |
---


