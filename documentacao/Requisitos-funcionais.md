# 📋 Requisitos Funcionais - Sedatines

Este documento lista todas as funcionalidades que o sistema deve possuir para atender aos objetivos do projeto. A lista está dividida por módulos de acordo com o perfil de usuário que interage com a funcionalidade.

**Índice:**
- [1. Módulo Administrativo](#1-módulo-administrativo-dashboard)
- [2. Módulo do Criador](#2-módulo-do-criador-área-logada)
- [3. Módulo Público](#3-módulo-público-visitante--navegação)
- [4. Requisitos de Sistema](#4-requisitos-de-sistema-backend)
- [5. Voltar para o Índice da Documentação](./README.md)


> **Legenda de Prioridade:**
> * **Alta:** Essencial para o MVP (Mínimo Produto Viável).
> * **Média:** Importante, mas pode ficar para a versão 1.1.
> * **Baixa:** Desejável, funcionalidade extra.

---
<!-- | **RF** | ** ** | des | rel | pri | [ ] | -->
## 1. Módulo Administrativo (Dashboard)

Funcionalidades exclusivas para usuários com a flag `is_admin`.

| ID | Título | Descrição | Req. Relacionado | Prioridade | Status |
|:---|:-------|:----------|:-----------------|:-----------|:-------|
| **RF001** | **Configuração Global (Modo de Publicação)** | O admin deve poder alternar entre publicação "Livre" (imediata) e "Moderada" (requer aprovação). | - | Alta | [ ] |
| **RF002** | **Modo de Manutenção** | O admin deve poder colocar o site em "Manutenção", impedindo o acesso público exceto para admins. | - | Baixa | [ ] |
| **RF003** | **Gestão de Títulos (Ranks)** | CRUD de títulos, definindo limites e permissões especiais. | - | Média | [ ] |
| **RF004** | **Listagem de Usuários** | Listar todos os usuários cadastrados, com filtros por Título ou Status. | - | Alta | [ ] |
| **RF005** | **Atribuição de Títulos** | Alterar o título de qualquer usuário. | RF003 | Média | [ ] |
| **RF006** | **Configuração de Título Padrão** | Definir o título atribuído automaticamente a novos cadastros. | RF003 | Média | [ ] |
| **RF007** | **Moderação de Pendentes** | Listar entidades com status `Pendente` para avaliação. | RF001 | Alta | [ ] |
| **RF008** | **Alteração de Status de Entidade** | Alterar status da entidade e notificar o criador. Opçoes:  `Publicada`, `Rejeitada`, `Oculta` ou `Excluída` (exclusão lógica) | RF345 | Alta | [ ] |
| **RF009** | **Solicitar Revisão** | Solicitar ajustes e mudar status para `Em Revisão`. | RF345 | Alta | [ ] |
| **RF010** | **Gestão de Denúncias** | Listar denúncias feitas por usuários. | RF237 | Média | [ ] |
| **RF011** | **Gerir Bloqueios (Punição)** | Suspender privilégios de usuários com registro e notificação. | - | Média | [ ] |
| **RF012** | **Remover Bloqueio** | Reativar um usuário suspenso. | RF011 | Média | [ ] |
| **RF013** | **Gestão de Categorias** | CRUD de categorias/tags para entidades. | - | Baixa | [ ] |

## 2. Módulo do Criador (Área Logada)

Funcionalidades para usuários autenticados (Membros da Comunidade).

| ID | Título | Descrição | Req. Relacionado | Prioridade | Status |
|:---|:-------|:----------|:-----------------|:-----------|:-------|
| **RF101** | **Gestão de Entidade** | Permitir o CRUD (Criar, Ler, Atualizar, Excluir) de entidades. O status inicial é definido pelas regras do RF001. | RF001 | Alta | [ ] |
| **RF102** | **Validação de Cotas** | Bloquear a criação de novas entidades caso o usuário atinja o limite permitido pelo seu Título/Nível. | RF003 | Alta | [ ] |
| **RF103** | **Validação de Atributos** | Validar e impedir que os atributos da entidade ultrapassem os limites definidos pelo Título/Nível do usuário. | RF003 | Média | [ ] |
| **RF104** | **Edição de Entidade** | Permitir edição de entidades próprias. Se o sistema estiver em modo "Moderação", a edição reverte o status para `Pendente`. | - | Alta | [ ] |
| **RF105** | **Upload de Mídia** | Permitir o envio (upload) de imagens para compor a galeria ou avatar de uma entidade. | - | Média | [ ] |
| **RF106** | **Clonar Entidade** | Permitir a criação de uma nova entidade baseada nos dados de uma existente (duplicação). | RF101 | Baixa | [ ] |
| **RF107** | **Definir Relacionamentos** | Permitir estabelecer vínculos ou conexões entre diferentes entidades. | - | Baixa | [ ] |
| **RF108** | **Gestão de Contos (Entidade)** | CRUD de histórias específicas da entidade, organizadas por capítulos. | - | Baixa | [ ] |
| **RF109** | **Vínculo de Personagens** | Permitir associar entidades (personagens) participantes dentro dos contos. | RF108 | Baixa | [ ] |
| **RF110** | **Nomes Alternativos** | Permitir cadastrar múltiplos nomes, apelidos ou pseudônimos para uma mesma entidade. | RF101 | Média | [ ] |
| **RF111** | **Gestão de Lore/Mundo** | CRUD da história geral do mundo, dividida em capítulos (conforme permissão do Título do usuário). | - | Baixa | [ ] |
| **RF112** | **Gestão de Perfil** | Permitir ao usuário atualizar suas informações cadastrais e de perfil. | - | Alta | [ ] |
| **RF113** | **Exclusão de Conta** | Permitir ao usuário solicitar a exclusão permanente de sua conta e dados pessoais. | - | Baixa | [ ] |
| **RF114** | **Favoritar Entidade** | Permitir adicionar entidades de outros usuários a uma lista de favoritos. | - | Baixa | [ ] |
| **RF115** | **Comentar em Entidade** | Permitir a publicação de comentários na página de uma entidade. | - | Baixa | [ ] |
| **RF116** | **Responder Comentário** | Permitir responder a comentários existentes, criando uma discussão encadeada (thread). | RF115 | Baixa | [ ] |
| **RF117** | **Identificação do Dono** | Destacar visualmente os comentários feitos pelo criador (dono) da entidade. | RF115 | Baixa | [ ] |
| **RF118** | **Marcação de Spoiler** | Permitir que o autor do comentário oculte trechos do texto marcando-os como spoiler. | - | Média | [ ] |
| **RF119** | **Visualizar Spoiler** | Permitir revelar o conteúdo oculto por spoiler mediante interação do usuário. | RF118 | Média | [ ] |
| **RF120** | **Títulos da Entidade** | Permitir atribuir múltiplos títulos honoríficos ou cargos a uma entidade. | RF101 | Média | [ ] |

## 3. Módulo Público (Visitante & Navegação)

Funcionalidades acessíveis a qualquer pessoa (autenticada ou não).

| ID | Título | Descrição | Req. Relacionado | Prioridade | Status |
|:---|:-------|:----------|:-----------------|:-----------|:-------|
| **RF201** | **Autenticação** | Realizar login no sistema utilizando E-mail e Senha. | - | Alta | [ ] |
| **RF202** | **Cadastro de Usuário** | Registrar novos usuários no sistema, com validação de dados obrigatórios. | - | Alta | [ ] |
| **RF203** | **Recuperação de Senha** | Permitir a redefinição de senha através de confirmação por e-mail. | - | Alta | [ ] |
| **RF204** | **Galeria de Entidades** | Listar todas as entidades publicadas (públicas), com suporte a paginação. | - | Alta | [ ] |
| **RF205** | **Denúncia de Conteúdo** | Permitir que usuários denunciem entidades ou comentários ofensivos/inadequados. | RF010 | Média | [ ] |
| **RF206** | **Busca e Filtros** | Pesquisar e filtrar entidades por nome, categoria, autor e classificação (rank). | - | Média | [ ] |
| **RF207** | **Detalhes da Entidade** | Exibir a página completa contendo todas as informações públicas de uma entidade. | - | Alta | [ ] |
| **RF208** | **Visualização de Lore** | Exibir a "História do Mundo" (Lore) e cronologias disponíveis para leitura. | RF111 | Baixa | [ ] |

## 4. Requisitos de Sistema (Backend)

Regras de negócio automatizadas e processos de fundo do sistema.

| ID | Título | Descrição | Req. Relacionado | Prioridade | Status |
|:---|:-------|:----------|:-----------------|:-----------|:-------|
| **RF301** | **Log de Auditoria** | Registrar automaticamente ações críticas do sistema, armazenando o IP de origem e o Timestamp. | - | Baixa | [ ] |
| **RF302** | **Atribuição Inicial** | Atribuir automaticamente o Título/Nível padrão ao finalizar o cadastro de um novo usuário. | RF006 | Alta | [ ] |
| **RF303** | **Envio de E-mails** | Gerenciar o envio de e-mails transacionais (recuperação de senha, boas-vindas, validação). | - | Média | [ ] |
| **RF304** | **Unicidade de Dados** | Validar e garantir a unicidade dos campos "Nome de Usuário" e "E-mail" no banco de dados. | RF202 | Alta | [ ] |
| **RF305** | **Notificações Internas** | Gerar e persistir alertas internos para serem exibidos no dashboard do usuário. | - | Média | [ ] |
| **RF306** | **Validação de E-mail** | Bloquear recursos específicos até que a verificação do e-mail seja concluída (Token/Link). | RF202, RF112 | Alta | [ ] |
| **RF307** | **Controle de Acesso** | Interceptar requisições (Middleware) para validar permissões baseadas no Título ou Flags do usuário. | - | Alta | [ ] |
| **RF308** | **Processamento de Imagens** | Otimizar, converter e renomear (com hash único) as imagens enviadas antes do armazenamento definitivo. | RF105 | Média | [ ] |
---

