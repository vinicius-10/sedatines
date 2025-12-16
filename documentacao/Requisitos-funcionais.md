# 📋 Requisitos Funcionais - Sedatines

Este documento lista todas as funcionalidades que o sistema deve possuir para atender aos objetivos do projeto.

> **Legenda de Prioridade:**
> * **Alta:** Essencial para o MVP (Mínimo Produto Viável).
> * **Média:** Importante, mas pode ficar para uma versão 1.1.
> * **Baixa:** Desejável, "Nice to have".

---

## 1. Módulo Administrativo (Dashboard)

Funcionalidades exclusivas para usuários com a flag `is_admin`.

| ID | Descrição | Prioridade | Status |
|:---|:----------|:-----------|:-------|
| **RF001** | **Gestão de Configuração Global:** O admin deve poder alternar o modo de publicação do site entre "Livre" (publicação imediata) e "Moderado" (requer aprovação). | Alta | [ ] |
| **RF002** | **Gestão de Títulos (Ranks):** CRUD de títulos de usuário (Ex: Iniciado, Mestre). Cada título deve definir: <br> 1. Limite de entidades (`max_entities`). <br> 2. Limite de pontos de atributos (`max_stats_points`). | Média | [ ] |
| **RF003** | **Atribuição de Títulos:** O admin deve poder alterar o título de qualquer usuário registrado (Promoção/Rebaixamento). | Média | [ ] |
| **RF004** | **Moderação de Entidades:** Listar entidades com status `pending` e permitir aprovar (`published`) ou rejeitar (retornar a `draft`). | Alta | [ ] |
| **RF005** | **Gestão de Categorias:** Criar e editar categorias/tags para as criaturas (Ex: Demônio, Espectro, Humano). | Baixa | [ ] |

## 2. Módulo do Criador (Área Logada)

Funcionalidades para usuários autenticados (Membros da Comunidade).

| ID | Descrição | Prioridade | Status |
|:---|:----------|:-----------|:-------|
| **RF006** | **Cadastro de Entidade:** O usuário deve poder criar uma nova entidade informando: Nome, Descrição (Lore), Imagem de Capa e Atributos de RPG. | Alta | [ ] |
| **RF007** | **Validação de Limites:** O sistema deve bloquear a criação de novas entidades se o usuário atingir o limite do seu Título atual (`user.entities_count >= title.limit`). | Alta | [ ] |
| **RF008** | **Distribuição de Atributos:** O sistema deve validar se a soma dos atributos da entidade não ultrapassa o limite permitido pelo Título do usuário. | Média | [ ] |
| **RF009** | **Edição de Entidade:** O usuário pode editar apenas as entidades que ele criou. Se o site estiver em modo "Moderado", a edição volta o status para `pending`. | Alta | [ ] |
| **RF010** | **Upload de Mídia:** O sistema deve permitir envio de imagem (JPG/PNG), redimensionar e salvar otimizado. | Alta | [ ] |

## 3. Módulo Público (Visitante)

Funcionalidades acessíveis a qualquer pessoa sem login.

| ID | Descrição | Prioridade | Status |
|:---|:----------|:-----------|:-------|
| **RF011** | **Galeria de Entidades:** Listagem das entidades com status `published`, com paginação. | Alta | [ ] |
| **RF012** | **Filtros e Busca:** Permitir buscar por nome ou filtrar por Categoria/Autor. | Média | [ ] |
| **RF013** | **Visualização Detalhada:** Página única da entidade exibindo Lore completa, Autor (com seu Título) e Gráfico de Atributos. | Alta | [ ] |
| **RF014** | **Autenticação:** Sistema de Login e Registro de novos usuários. | Alta | [ ] |

## 4. Requisitos de Sistema (Back-end)

| ID | Descrição | Prioridade | Status |
|:---|:----------|:-----------|:-------|
| **RF015** | **Log de Atividades:** Registrar quem criou ou alterou uma entidade (para auditoria). | Baixa | [ ] |

## Voltar
[Voltar para documentação](./documentacao.md)
