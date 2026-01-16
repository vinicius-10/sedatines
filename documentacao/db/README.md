## Banco de dados

## 📑 Sumário
- [MER](#-Modelo-entidade-relacionamento)
- [Dicionario de dados user](#-)
- [Dicionario de dados ](#-)
- [Dicionario de dados ](#-)
- [Dicionario de dados ](#-)
- [Dicionario de dados ](#-)
- [Dicionario de dados ](#-)
- [Documetação](../README.md)

---

<!-- 

|o	o|	0/1
||	||	1/1
}o	o{	0/n
}|	|{	1/n

-->

## Modelo entidade relacionamento
```mermaid
erDiagram
    titles ||--|{ users : "define permissoes"
    users ||--|{ entities : "cria (dono)"
    categories ||--|{ entities : "classifica"
    users ||--|{ comments : "escreve"
    users ||--|{ audit_logs : "causa"
    
    entities ||--o{ comments : "recebe (polimorfico)"
    world_events ||--o{ comments : "recebe (polimorfico)"
    
    entities }|--|{ entities : "relaciona (pivot: entity_relationships)"
    users }|--|{ entities : "favorita (pivot: favorites)"
    
    users ||--|{ world_events : "escreve"
    users ||--|{ stories : "escreve"
    stories }|--|{ entities : "menciona (pivot: story_entity)"
    users ||--|{ reports : "reporta"

    titles {
        int 🗝️id PK
        string name
        string slug "Unique"
        int max_entities
        int max_stats_points
        json permissions "ACL"
    }

    users {
        bigint id PK
        foreign_key title_id
        string name
        string email "Unique, Index"
        string password
        string bio
        string avatar_path
        timestamp email_verified_at
        boolean is_banned "Default: false"
        timestamp last_login_at
    }

    entities {
        bigint id PK
        foreign_key user_id
        foreign_key category_id
        string name
        string slug "Unique, Index"
        text lore
        string image_path
        json stats "{força: 10, ...}"
        enum status "draft, pending, published, rejected, hidden"
        timestamp deleted_at "SoftDelete"
    }

    entity_relationships {
        bigint id PK
        foreign_key from_entity_id
        foreign_key to_entity_id
        string type "Ex: inimigo, irmão"
    }

    comments {
        bigint id PK
        foreign_key user_id
        morph commentable_type "Entity ou WorldEvent"
        bigint commentable_id
        foreign_key parent_id "Para threads"
        text content
        boolean is_spoiler
        timestamp deleted_at
    }

    audit_logs {
        bigint id PK
        foreign_key user_id "Quem fez"
        string action "Ex: delete_entity"
        json old_values
        json new_values
        string ip_address
    }
```


## 📕 Dicionário de Dados

## 
| Coluna | Tipo | PK/FK? | Obrigatório? | Descrição |
| :--- | :--- | :---: | :---: | :--- |
| `id` | INT | **PK** | Sim | Identificador único auto-incremento. |
| `name` | VARCHAR(100) | | Sim | Nome completo do usuário. |
| `email` | VARCHAR(255) | | Sim | Deve ser único no sistema. |
| `role_id` | INT | **FK** | Sim | Referência à tabela `roles`. |
| `created_at` | DATETIME | | Não | Data de criação do registro. |
