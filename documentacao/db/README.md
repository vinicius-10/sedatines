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
    ranks ||--|{ users : "define permissoes"
    users ||--|{ entities : "cria (dono)"
    categories ||--|{ entities : "classifica"
    users ||--|{ comments : "escreve"
    users ||--|{ audit_logs : "causa"
    users ||--o{user_bans : "banida"
    
    entities ||--o{ comments : "recebe (polimorfico)"
    world_events ||--o{ comments : "recebe (polimorfico)"
    
    entities }|--|{ entities : "relaciona (pivot: entity_relationships)"
    users }|--|{ entities : "favorita (pivot: favorites)"
    entities }o--|| entity_image : "posui"
    
    users ||--|{ world_events : "escreve"
    users ||--|{ stories : "escreve"
    stories }|--|{ entities : "menciona (pivot: story_entity)"
    users ||--|{ reports : "reporta"

    ranks {
        bigInt id PK
        string rank
        string slug "Unique"
        int max_entity
        int max_attributes
        json permissions
        timestap created_at
        timestap updated_at
    }

    users {
        bigInt id PK
        bigInt ranks_id FK
        string name
        string email "Unique, Index"
        string password
        string avatar_path
        boolean deleted_at nullable
        timestamp email_verified_at nullable
        timestap created_at
        timestap updated_at
    }

    user_bans{
        bigInt id PK
        bigInt user_id FK
        int admin_id
        text reason
        timestap expires_at nullable
        timestap created_at
        timestap updated_at
    }

    entities {
        bigInt id PK
        bigInt user_id
        bigInt category_id
        string name
        string slug "Unique, Index"
        text description
        json stats 
        enum status "draft, pending, published, rejected, hidden"
        timestamp deleted_at "SoftDelete"
        timestap created_at
        timestap updated_at
    }

    entity_image {
        "Big int" id PK
        "Big int" entity_id FK
        string image_path
        string alt_text
        int order
        timestap created_at
        timestap updated_at
    }

    entity_relationships {
        "big int" id PK
        "big int" from_entity_id
        "big int" to_entity_id
        string type "Ex: inimigo, irmão"
        timestap created_at
        timestap updated_at
    }

    comments {
        "big int" id PK
        "big int"  user_id
        morph commentable_type "Entity ou WorldEvent"
        bigint commentable_id
        "big int" parent_id "Para threads"
        text content
        boolean is_spoiler
        timestamp deleted_at
        timestap created_at
        timestap updated_at
    }

    audit_logs {
        "big int" id PK
        "big int" user_id "Quem fez"
        string action "Ex: delete_entity"
        json old_values
        json new_values
        string ip_address
        timestap created_at
        timestap updated_at
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
