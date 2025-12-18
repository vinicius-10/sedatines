# 📋 Requisitos Funcionais - Sedatines

Este documento lista todas as funcionalidades que o sistema deve possuir para atender aos objetivos do projeto. A lista está dividida por módulos de acordo com o perfil de usuário que interage com a funcionalidade.

**Índice:**
- [1. Módulo Administrativo](#1-módulo-administrativo-dashboard)
- [2. Módulo do Criador](#2-módulo-do-criador-área-logada)
- [3. Módulo Público](#3-módulo-público-visitante--navegação)
- [4. Requisitos de Sistema](#4-requisitos-de-sistema-backend)

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
| **RF003** | **Gestão de Títulos (Ranks)** | CRUD de títulos. Cada título define: <br> 1. Limite de criação (`max_entities`). <br> 2. Limite de atributos (`max_stats_points`).<br> 3. Permissões especiais (criar categorias, editar lore global). | - | Média | [ ] |
| **RF004** | **Listagem de Usuários** | O admin deve poder listar todos os usuários cadastrados, com filtros por Título ou Status. | - | Alta | [ ] |
| **RF005** | **Atribuição de Títulos** | O admin deve poder alterar o título de qualquer usuário (Promoção/Rebaixamento). | RF003 | Média | [ ] |
| **RF006** | **Configuração de Título Padrão** | O admin deve definir qual o Título atribuído automaticamente a novos cadastros. | RF003 | Média | [ ] |
| **RF007** | **Moderação de Pendentes** | Listar todas as entidades com status `Pendente` para avaliação. | RF001 | Alta | [ ] |
| **RF008** | **Alteração de Status de Entidade** | O Admin deve poder alterar o status para: `Publicada`, `Rejeitada`, `Oculta` ou `Excluída` (exclusão lógica). O criador é notificado. | RF045 | Alta | [ ] |
| **RF009** | **Solicitar Revisão** | O admin pode solicitar alterações enviando feedback. O status muda para `Em Revisão` e o autor é notificado. | RF045 | Alta | [ ] |
| **RF010** | **Gestão de Denúncias** | Listar denúncias feitas pelos usuários contra entidades ou comentários ofensivos. | RF037 | Média | [ ] |
| **RF011** | **Gerir Bloqueios (Punição)** | O admin pode suspender privilégios de um usuário (banir login, banir criação ou comentários) com registro e notificação do motivo. | - | Média | [ ] |
| **RF012** | **Remover Bloqueio** | O admin pode reativar um usuário suspenso. | RF011 | Média | [ ] |
| **RF013** | **Gestão de Categorias** | CRUD de categorias/tags para as criaturas (Ex: Demônio, Espectro, Humano). | - | Baixa | [ ] |

## 2. Módulo do Criador (Área Logada)

Funcionalidades para usuários autenticados (Membros da Comunidade).

| ID | Título | Descrição | Req. Relacionado | Prioridade | Status |
|:---|:-------|:----------|:-----------------|:-----------|:-------|
| **RF014** | **Cadastro de Entidade** | O criador deve poder criar uma nova entidade. O status inicial depende do RF001. | RF001 | Alta | [ ] |
| **RF015** | **Validação de Cotas** | O sistema deve bloquear a criação se o usuário atingir o limite de entidades do seu Título. | RF003 | Alta | [ ] |
| **RF016** | **Validação de Atributos** | O sistema deve impedir que a soma dos atributos ultrapasse o limite permitido pelo Título. | RF003 | Média | [ ] |
| **RF017** | **Edição de Entidade** | O autor pode editar as suas próprias entidades. Em modo "Moderado", a edição reverte o status para `Pendente`. | - | Alta | [ ] |
| **RF018** | **Upload de Mídia** | O sistema deve permitir envio de imagens, redimensionar e salvar de forma otimizada. | - | Alta | [ ] |
| **RF019** | **Clonar Entidade (Template)** | O criador pode escolher uma entidade existente como modelo base para uma nova ficha. | RF014 | Baixa | [ ] |
| **RF020** | **Definir Relacionamentos** | O dono da entidade pode definir relacionamentos com outras entidades (Ex: "Inimigo de"). | - | Baixa | [ ] |
| **RF021** | **Gestão de Contos** | CRUD de histórias/contos literários vinculados ao universo. | - | Baixa | [ ] |
| **RF022** | **Vínculo de Personagens** | Ao criar um Conto, o autor pode selecionar quais Entidades participam na história. | RF021 | Baixa | [ ] |
| **RF023** | **Criação da História do Mundo** | Usuários com permissão elevada podem criar capítulos da Lore Global. | RF003 | Baixa | [ ] |
| **RF024** | **Edição da História do Mundo** | Usuários com permissão podem editar capítulos existentes da Lore Global. | RF023 | Baixa | [ ] |
| **RF025** | **Gestão de Perfil** | O usuário deve poder atualizar dados (Senha, Foto, Bio, Email). | - | Alta | [ ] |
| **RF026** | **Exclusão de Conta** | O usuário pode solicitar a exclusão da sua conta e dados pessoais. | - | Baixa | [ ] |
| **RF027** | **Favoritar Entidade** | O usuário deve poder adicionar entidades aos favoritos. | - | Baixa | [ ] |
| **RF028** | **Comentar em Entidade** | O usuário pode comentar na página de uma entidade. | - | Baixa | [ ] |
| **RF029** | **Responder Comentário (Thread)** | O usuário pode responder a um comentário existente (aninhamento). | RF028 | Baixa | [ ] |
| **RF030** | **Identificação do Dono** | Nos comentários, o dono da Entidade deve ter um destaque visual (Badge). | RF028 | Baixa | [ ] |
| **RF031** | **Marcação de Spoiler** | O usuário pode marcar partes do texto do comentário como "Spoiler", ocultando o conteúdo. | - | Média | [ ] |
| **RF032** | **Visualizar Spoiler** | Ao clicar na área oculta (RF031), o conteúdo deve ser revelado. | RF031 | Média | [ ] |

## 3. Módulo Público (Visitante & Navegação)

Funcionalidades acessíveis a qualquer pessoa (autenticada ou não).

| ID | Título | Descrição | Req. Relacionado | Prioridade | Status |
|:---|:-------|:----------|:-----------------|:-----------|:-------|
| **RF033** | **Autenticação** | Sistema deve permitir login via Email/User e Senha. | - | Alta | [ ] |
| **RF034** | **Cadastro** | O sistema deve permitir o cadastro de novos usuários com verificação de unicidade. | - | Alta | [ ] |
| **RF035** | **Recuperar Acesso** | O usuário pode redefinir a senha via link de email. | - | Alta | [ ] |
| **RF036** | **Galeria de Entidades** | Listagem das entidades com status `Publicada`, com paginação. | - | Alta | [ ] |
| **RF037** | **Denunciar Conteúdo** | Visitantes podem reportar entidades ou comentários ofensivos à administração. | RF010 | Média | [ ] |
| **RF038** | **Filtros e Pesquisa** | Permitir pesquisar por nome e/ou filtrar por Categoria, Autor e Rank. | - | Média | [ ] |
| **RF039** | **Visualização Detalhada** | Página única da entidade exibindo Lore, Autor, Gráfico de Atributos e Relacionamentos. | - | Alta | [ ] |
| **RF040** | **Linha do Tempo (Lore)** | Visualizar a "História do Mundo" filtrada por datas/eras. | RF023 | Baixa | [ ] |

## 4. Requisitos de Sistema (Backend)

Regras de negócio automatizadas pelo sistema.

| ID | Título | Descrição | Req. Relacionado | Prioridade | Status |
|:---|:-------|:----------|:-----------------|:-----------|:-------|
| **RF041** | **Log de Auditoria** | Registrar ações críticas (ex: Admin apagou entidade, Usuário banido) com timestamp e IP. | - | Baixa | [ ] |
| **RF042** | **Atribuição Inicial** | Ao se cadastrar, o sistema atribui automaticamente o Título padrão (RF006). | RF006 | Alta | [ ] |
| **RF043** | **Sistema de Notificação (Email)** | Envio de emails transacionais (Boas-vindas, Recuperação de Senha, Alertas). | - | Média | [ ] |
| **RF044** | **Unicidade de Usuário** | O sistema deve garantir que o Nome de Usuário e Email sejam únicos no banco de dados. | RF034 | Alta | [ ] |
| **RF045** | **Notificações Internas** | Alerta visual no dashboard (sininho) para feedback de aprovação, comentários ou denúncias. | - | Média | [ ] |
| **RF046** | **Validação de Email** | Quando um usuário se cadastrar ou atualizar email, deve ser enviado um email com código/link de confirmação obrigatório. | RF034, RF025 | Alta | [ ] |
| **RF047** | **Controle de Autorização** | O sistema deve validar permissões (Policies/Gates) com base no Título e flags antes de executar ações sensíveis. | - | Alta | [ ] |

---

## 📄 Documentação
[Voltar para o Índice da Documentação](./documentacao.md)
