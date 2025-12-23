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
| **RF101** | **Cadastro de Entidade** | Criar uma nova entidade. O status inicial depende do RF001. | RF001 | Alta | [ ] |
| **RF102** | **Validação de Cotas** | Bloquear criação ao atingir limite do Título. | RF003 | Alta | [ ] |
| **RF103** | **Validação de Atributos** | Impedir ultrapassar limite de atributos do Título. | RF003 | Média | [ ] |
| **RF104** | **Edição de Entidade** | Editar entidades próprias; pode voltar a `Pendente`. | - | Alta | [ ] |
| **RF105** | **Upload de Mídia** | Envio e otimização de imagens. | - | Alta | [ ] |
| **RF106** | **Clonar Entidade** | Criar entidade a partir de um template. | RF101 | Baixa | [ ] |
| **RF107** | **Definir Relacionamentos** | Definir relacionamentos entre entidades. | - | Baixa | [ ] |
| **RF108** | **Gestão de Contos** | CRUD de histórias/contos. | - | Baixa | [ ] |
| **RF109** | **Vínculo de Personagens** | Vincular entidades a contos. | RF108 | Baixa | [ ] |
| **RF110** | **Criação da História do Mundo** | Criar capítulos da Lore Global. | RF003 | Baixa | [ ] |
| **RF111** | **Edição da História do Mundo** | Editar capítulos existentes da Lore Global. | RF110 | Baixa | [ ] |
| **RF112** | **Gestão de Perfil** | Atualizar senha, foto, bio e email. | - | Alta | [ ] |
| **RF113** | **Exclusão de Conta** | Solicitar exclusão da conta e dados pessoais. | - | Baixa | [ ] |
| **RF114** | **Favoritar Entidade** | Adicionar entidades aos favoritos. | - | Baixa | [ ] |
| **RF115** | **Comentar em Entidade** | Comentar na página de uma entidade. | - | Baixa | [ ] |
| **RF116** | **Responder Comentário** | Responder comentários (thread). | RF115 | Baixa | [ ] |
| **RF117** | **Identificação do Dono** | Destacar dono da entidade nos comentários. | RF115 | Baixa | [ ] |
| **RF118** | **Marcação de Spoiler** | Marcar partes do texto como spoiler. | - | Média | [ ] |
| **RF119** | **Visualizar Spoiler** | Revelar conteúdo oculto. | RF118 | Média | [ ] |

## 3. Módulo Público (Visitante & Navegação)

Funcionalidades acessíveis a qualquer pessoa (autenticada ou não).

| ID | Título | Descrição | Req. Relacionado | Prioridade | Status |
|:---|:-------|:----------|:-----------------|:-----------|:-------|
| **RF201** | **Autenticação** | Login via Email/User e Senha. | - | Alta | [ ] |
| **RF202** | **Cadastro** | Cadastro de novos usuários com validação. | - | Alta | [ ] |
| **RF203** | **Recuperar Acesso** | Redefinição de senha via email. | - | Alta | [ ] |
| **RF204** | **Galeria de Entidades** | Listagem de entidades publicadas com paginação. | - | Alta | [ ] |
| **RF205** | **Denunciar Conteúdo** | Denunciar entidades ou comentários ofensivos. | RF010 | Média | [ ] |
| **RF206** | **Filtros e Pesquisa** | Pesquisa por nome, categoria, autor e rank. | - | Média | [ ] |
| **RF207** | **Visualização Detalhada** | Página completa da entidade. | - | Alta | [ ] |
| **RF208** | **Linha do Tempo (Lore)** | Visualizar a História do Mundo. | RF110 | Baixa | [ ] |

## 4. Requisitos de Sistema (Backend)

Regras de negócio automatizadas pelo sistema.

| ID | Título | Descrição | Req. Relacionado | Prioridade | Status |
|:---|:-------|:----------|:-----------------|:-----------|:-------|
| **RF301** | **Log de Auditoria** | Registrar ações críticas com IP e timestamp. | - | Baixa | [ ] |
| **RF302** | **Atribuição Inicial** | Atribuir título padrão ao cadastrar usuário. | RF006 | Alta | [ ] |
| **RF303** | **Sistema de Notificação (Email)** | Envio de emails transacionais. | - | Média | [ ] |
| **RF304** | **Unicidade de Usuário** | Garantir unicidade de usuário e email. | RF202 | Alta | [ ] |
| **RF345** | **Notificações Internas** | Alertas internos no dashboard. | - | Média | [ ] |
| **RF306** | **Validação de Email** | Confirmação obrigatória de email. | RF202, RF112 | Alta | [ ] |
| **RF307** | **Controle de Autorização** | Validação de permissões por Título/flags. | - | Alta | [ ] |

---

