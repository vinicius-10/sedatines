# 🛡️ Requisitos Não Funcionais - Sedatines

Este documento define as restrições técnicas, padrões de qualidade e exigências de infraestrutura do projeto.

**Índice:**
- [1. Tecnologis](#)
- []
- [2. Usabilidade e Interface](#)
- [3. Segurança e Dados](#)
- [4. Desempenho e Confiabilidade](#4)
- [5. Qualidade de Código e Documentação](#)

> **Legenda de Prioridade:**
> * **Critica** O sistema não pode ser implantado sem isso. 
> * **Alta:** O sistema precisa ter.
> * **Média:** Necessário para uma boa experiência do usuário.
> *  **Baixa:** Melhoria contínua.

---
<!-- | ** ** | ** ** | des | pri | RF0 | -->

## 1. Tecnologias e Stack (Restrições de Implementação)

| ID   | Título | Descrição  | Prioridade | Requisitos Relacionados |
| :--: | :----: | :--------: | :--------: | :---------------------: |
| **RNF001** | **Backend Framework** | O sistema deve ser desenvolvido em **PHP 8.4** utilizando o framework **Laravel 12**. | Alta | - | 
| **RNF002** | **Banco de Dados** | O SGDB utilizado deve ser **MySQL 8.0**. | Crítica | - |
| **RNF003** | **Ambiente de Desenvolvimento** | O projeto deve ser containerizado utilizando **Docker** (via Laravel Sail) para garantir paridade entre ambiente de dev e produção. | Alta | - |
| **RNF004** | **Renderização do Frontend** | A estrutura das páginas deve ser renderizada no servidor (SSR) utilizando Blade Templates. | Alta | - |
| **RFN005** | **Interaçoes do Frontend** | As ações de usuário (formulários, filtros, likes) devem ser processadas via JavaScript assíncrono (AJAX/Fetch) para evitar recarregamentos de página desnecessários. | Alta | - |
| **RNF006** | **Controle de Versão** | O código deve ser versionado no Git, seguindo o fluxo de branches definido (Main/Develop). | Alta | - |
| **RNF007** | **CSS** | A interface deve ser construída utilizando o framework Tailwind CSS para agilidade e padronização. | Média | - |
| **RNF008** | **Servidor web** | A aplicação deve ser servida via Nginx | Média | - |
| **RNF009** | **Gerenciamento de dependencia** | As bibliotecas de backend devem ser gerenciadas via Composer e as de frontend via NPM. | Alta | - |
| **RNF010** |**Framework de Testes** | **Testes automatizados (Unitários e de Feature) devem ser escritos utilizando Pest PHP (padrão moderno do Laravel).** |  Média | - |


## 2. Usabilidade e Interface (UX/UI)

| ID   | Título | Descrição | Prioridade | Requisitos Relacionados |
| :--: | :---: | :-------- | :--------: | :---------------------: |
| **RNF011** | **Responsividade** | O layout deve ser fluido e adaptável (Responsive Web Design), garantindo usabilidade em Mobile, Tablet e Desktop. | Alta | - |
| **RNF012** | **Identidade Visual (Tema)** | O sistema deve adotar o tema "Dark Mode" como padrão, alinhado à estética de terror/mistério do projeto. | Média | - |
| **RNF013** | **Seletor de Tema** | O usuário deve ter a opção de alternar entre tema Escuro e Claro, e a preferência deve ser salva no navegador (LocalStorage). | Baixa | RNF012 |
| **RNF014** | **Feedback de Sistema** | Ações de sucesso ou informativas devem exibir notificações não-bloqueantes (Toasts) que somem automaticamente. Erros críticos devem exibir Alertas/Modais. | Alta | RNF005 |
| **RNF015** | **Acessibilidade Básica** | Imagens devem ter atributos `alt` e inputs devem ter `labels` associados para suporte básico a leitores de tela. | Média | - |
| **RNF016** | **Indicadores de Carregamento** | Toda requisição assíncrona (AJAX) deve exibir um indicador visual de progresso (Spinner ou Skeleton) enquanto processa, para evitar sensação de travamento. | Alta | RNF005 |
| **RNF017** | **Idioma da Interface** | Toda a interface pública e administrativa deve estar escrita em **Português do Brasil (PT-BR)**. | Alta | - |
| **RNF018** | **Navegação Global** | Com exceção das páginas de Autenticação e Erro, todas as telas devem possuir uma barra de navegação (Menu) consistente. | Alta | - |
| **RNF019** | **Hierarquia Visual** | Botões de ação primária (Ex: "Salvar", "Criar") devem ter destaque visual claro (cor/tamanho) sobre botões secundários (Ex: "Cancelar"). | Média | - |

## 3. Segurança e Proteção de Dados

| ID | Título | Descrição | Prioridade | Requisitos Relacionados |
| :--: | :----: | :-------- | :--------: | :---------------------: |
| **RNF020** | **Criptografia de Senhas** | Nenhuma senha deve ser armazenada em texto plano. Deve-se utilizar hash forte (**Argon2id** ou Bcrypt). | Crítica | RF034 |
| **RNF021** | **Proteção CSRF** | Todos os formulários de escrita (POST/PUT/DELETE) devem conter tokens de proteção contra Cross-Site Request Forgery. | Crítica | - |
| **RNF022** | **Sanitização (XSS)** | Todo input de usuário exibido em tela (comentários, lore) deve ser sanitizado/escapado para prevenir injeção de scripts maliciosos. | Crítica | - |
| **RNF023** | **Segurança de Uploads** | O sistema deve aceitar apenas formatos de imagem seguros (**JPEG, PNG, WEBP, AVIF**) com tamanho máximo de **5MB**. Arquivos executáveis ou vetoriais (SVG) devem ser rejeitados. | Crítica | RF018 |
| **RNF024** | **Proteção de Rotas (Middleware)** | As rotas administrativas e restritas devem ser protegidas por Middlewares que validem a autenticação antes de carregar o controlador. | Crítica | RF047 |
| **RNF025** | **Autorização de Ação (Policies)** | O sistema deve validar via Policies/Gates se o usuário tem permissão específica para o recurso alvo (Ex: "Usuário X pode editar o Post Y?"). | Crítica | RF047 |
| **RNF026** | **Persistência de Login (Lembrar-me)** | O sistema deve gerenciar sessões estendidas (ex: 30 dias) via cookie seguro caso o usuário marque a opção "Lembrar-me" no login. | Média | RF033 |
| **RNF027** | **Armazenamento de Sessão** | Tokens de autenticação devem ser armazenados exclusivamente em **Cookies HttpOnly/Secure**. É proibido o uso de LocalStorage para dados sensíveis. | Crítica | RF033 |
| **RNF028** | **Identificação Pública (Obfuscação)** | As URLs públicas não devem expor o ID sequencial (PK) do banco. Deve-se utilizar **UUIDs** ou **Slugs** únicos para prevenir enumeração de dados. | Alta | RF025, RF039 |
| **RNF029** | **Protocolo Seguro (HTTPS)** | Toda a comunicação entre cliente e servidor deve ser criptografada utilizando protocolo HTTPS (TLS 1.2+). | Crítica | - |
| **RNF030** | **Rate Limiting (Throttling)** | As rotas de Login e API devem possuir limite de requisições por minuto para mitigar ataques de Força Bruta e DDoS. | Alta | RF033 |
| **RNF031** | **Política de Senhas** | As senhas devem ter no mínimo 8 caracteres, exigindo a presença de letras e números (Alfanumérica). | Alta | RF034, RF025 |
| **RNF032** | **Headers de Segurança** | O servidor deve responder com headers de segurança configurados: `X-Frame-Options`, `X-Content-Type-Options` e `HSTS`. | Alta | - |
| **RNF033** | **Armazenamento de Uploads** | Arquivos enviados não devem manter o nome original. O sistema deve renomeá-los usando um Hash único (UUID/MD5) para evitar sobrescrita e execução maliciosa. | Alta | RF018 |
| **RNF034** | **Sanitização de Logs** | Os logs do sistema (Laravel Logs) não devem registrar dados sensíveis como senhas em texto plano ou tokens de acesso. | Alta | RF041 |
| **RNF035** | **Bloqueio por Tentativas** | Após 5 tentativas falhas de login consecutivas, o IP ou Usuário deve ser bloqueado temporariamente (Ex: 1 minuto) na camada de autenticação. | Alta | RF033 |


## 4. Confiabilidade e Infraestrutura

| ID | Título | Descrição | Prioridade | Requisitos Relacionados |
| :--: | :----: | :-------- | :--------: | :---------------------: |
| **RNF036** | **Rotina de Backup** | O sistema deve possuir uma rotina automatizada (Laravel Scheduler) para backup diário do banco de dados MySQL. | Alta | - |
| **RNF037** | **Páginas de Erro Customizadas** | O sistema deve tratar exceções HTTP (404, 403, 500) apresentando páginas amigáveis dentro do tema visual, sem expor Stack Traces (debug) em produção. | Baixa | - |
| **RNF038** | **Timeout de Requisições** | O servidor web (Nginx/PHP) deve ter um timeout configurado (ex: 60s) para evitar que processos travados consumam recursos indefinidamente. | Média | - |
| **RNF039** | **Health Check Endpoint** | O sistema deve expor um endpoint `/up` (nativo do Laravel 11+) para monitoramento externo de uptime e saúde da conexão com o banco. | Média | - |

## 5. Arquitetura e Qualidade de Código

| ID | Título | Descrição | Prioridade | Requisitos Relacionados |
| :--: | :----: | :-------- | :--------: | :---------------------: |
| **RNF040** | **Padrão de Arquitetura (MVC)** | O projeto deve seguir estritamente o padrão MVC. A lógica de negócio complexa deve ser extraída dos Controllers para **Service Classes** ou **Actions**, mantendo os controladores "magros" (Skinny Controllers). | Crítica | - |
| **RNF041** | **Validação Centralizada** | Toda validação de input deve ser feita através de **Form Requests** dedicados, proibindo validações manuais (`$request->validate`) dentro dos métodos do Controller. | Alta | - |
| **RNF042** | **Tratamento Global de Exceções** | O sistema deve capturar exceções não tratadas via `ExceptionHandler` do Laravel, evitando "telas brancas" e registrando o erro nos logs antes de exibir uma mensagem amigável ao usuário. | Alta | - |
| **RNF043** | **Padronização de Mensagens** | As mensagens de erro e sucesso (Flash Messages) devem seguir um padrão textual e visual consistente (Ex: "Objeto [Nome] criado com sucesso" / "Falha ao salvar: [Motivo]"). | Média | - |
| **RNF044** | **Cobertura de Testes** | O código deve manter uma cobertura mínima de testes (Code Coverage) de **70%** nas camadas de Serviço e Modelos críticos, utilizando Pest PHP. | Alta | - |
| **RNF045** | **Análise Estática (Linting)** | O código deve ser validado por ferramentas de análise estática (**Laravel Pint** para estilo PSR-12 e **PHPStan** nível 5 para erros lógicos) antes de qualquer merge. | Alta | - |
| **RNF046** | **Pipeline CI/CD** | O repositório deve conter um workflow do GitHub Actions que execute automaticamente os testes (RNF044) e a análise estática (RNF045) a cada Push ou Pull Request. | Alta | - |
| **RNF047** | **Verificação de Segurança Automatizada** | O pipeline deve incluir verificação de dependências vulneráveis (via `composer audit`) e análise estática de segurança (procura por hardcoded secrets ou injeções óbvias). | Média | - |

## 4. Desempenho

| ID   | Título | Descrição  | Prioridade | Requisitos Relacionados |
| :--: | :----: | :--------  | :--------: | :---------------------: |
| **RNF015** | **Otimização de Imagens** | Imagens enviadas pelos usuários devem ser convertidas e comprimidas (preferencialmente WebP) no servidor para reduzir o tempo de carregamento. | Alta |
| **RNF016** | **Paginação** | Listagens que podem crescer indefinidamente (Entidades, Logs, Comentários) devem implementar paginação (máx 20 itens por página). | Alta |
| **RNF017** | **Tempo de Resposta** | O tempo de carregamento das páginas não deve exceder 2 segundos em conexões 4G estáveis. | Média |

## 5. Qualidade de Código e Documentação

| ID   | Título | Descrição  | Prioridade | Requisitos Relacionados |
| :--: | :----: | :--------  | :--------: | :---------------------: |
| **RNF018** | **Padrão PSR-12** | O código PHP deve seguir a norma PSR-12 de estilo e formatação. | Alta |
| **RNF019** | **Idioma do Código** | Variáveis, métodos e comentários de código devem ser escritos em **Inglês** (padrão de mercado). A documentação externa (MD) pode ser em Português. | Média |
| **RNF020** | **Docs as Code** | A documentação de requisitos e banco de dados deve estar no repositório e ser atualizada junto com as features. | Alta |

---

## 📄 Documentação
[Voltar para o Índice da Documentação](./README.md)
