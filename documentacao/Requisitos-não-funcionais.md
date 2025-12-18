# 🛡️ Requisitos Não Funcionais - Sedatines

Este documento define as restrições técnicas, padrões de qualidade e exigências de infraestrutura do projeto.

**Índice:**
- [1. Tecnologis e Stack](#)
- [2. Usabilidade e Interface](#)
- [3. Segurança e Dados](#)
- [4. Desempenho e Confiabilidade](#4)
- [5. Qualidade de Código e Documentação](#)

> **Legenda de Prioridade:**
> * **Crítica:** O sistema não pode ser implantado sem isso.
> * **Alta:** Necessário para uma boa experiência do usuário.
> * **Média:** Melhoria contínua.

---
<!-- | ** ** | ** ** | des | pri | rf | -->

## 1. Tecnologias e Stack (Restrições de Implementação)

| ID   | Título | Descrição  | Prioridade | Requisitos Relacionados |
| :--: | :----: | :--------: | :--------: | :---------------------: |
| **RNF001** | **Backend Framework** | O sistema deve ser desenvolvido em **PHP 8.4** utilizando o framework **Laravel 12**. | Crítica | | 
| **RNF002** | **Banco de Dados** | O SGDB utilizado deve ser **MySQL 8.0**. | Crítica | |
| **RNF003** | **Ambiente de Desenvolvimento** | O projeto deve ser containerizado utilizando **Docker** (via Laravel Sail) para garantir paridade entre ambiente de dev e produção. | Alta ||
| **RNF004** | **Renderização do Frontend** | A estrutura das páginas deve ser renderizada no servidor (SSR) utilizando Blade Templates. | Alta | |
| **RFN005** | **Interaçoes do Frontend** | As ações de usuário (formulários, filtros, likes) devem ser processadas via JavaScript assíncrono (AJAX/Fetch) para evitar recarregamentos de página desnecessários. | Alta | |
| **RNF006** | **Controle de Versão** | O código deve ser versionado no Git, seguindo o fluxo de branches definido (Main/Develop). | Crítica | |
| **RNF007** | **CSS** | A interface deve ser construída utilizando o framework Tailwind CSS para agilidade e padronização. | Média |  |
| **RNF008** | **Servidor web** | A aplicação deve ser servida via Nginx | Média |  |
| **RNF009** | **Gerenciamento de dependencia** | As bibliotecas de backend devem ser gerenciadas via Composer e as de frontend via NPM. | Alta |  |
| **Framework de Testes** | **Testes automatizados (Unitários e de Feature) devem ser escritos utilizando Pest PHP (padrão moderno do Laravel).** |  | Média |  |

## 2. Usabilidade e Interface (UX/UI)

| ID   | Título | Descrição  | Prioridade | Requisitos Relacionados |
| :--: | :----: | :--------  | :--------: | :---------------------: |
| **RNF006** | **Responsividade** | O layout deve ser responsivo, adaptando-se a dispositivos móveis (smartphones), tablets e desktops. | Alta |
| **RNF007** | **Identidade Visual (Tema)** | O sistema deve utilizar uma paleta de cores escura ("Dark Mode") por padrão, alinhada à temática sobrenatural/terror. | Média |
| **RNF008** | **Feedback de Sistema** | Toda ação do usuário (salvar, excluir, erro) deve gerar um feedback visual (Toasts ou Flash Messages) em menos de 1 segundo. | Alta |
| **RNF009** | **Acessibilidade** | As imagens devem possuir atributos `alt` e os formulários devem seguir boas práticas de semântica HTML para leitores de tela. | Média |

## 3. Segurança e Confiabilidade

| ID   | Título | Descrição  | Prioridade | Requisitos Relacionados |
| :--: | :----: | :--------  | :--------: | :---------------------: |
| **RNF010** | **Criptografia de Senhas** | Nenhuma senha deve ser armazenada em texto plano. Deve-se utilizar hash forte (Bcrypt ou Argon2). | Crítica |
| **RNF011** | **Proteção CSRF** | Todos os formulários de escrita (POST/PUT/DELETE) devem conter tokens de proteção contra Cross-Site Request Forgery. | Crítica |
| **RNF012** | **Sanitização (XSS)** | Todo input de usuário exibido em tela (comentários, lore) deve ser escapado para prevenir Cross-Site Scripting. | Crítica |
| **RNF013** | **Validação de Uploads** | O sistema deve validar o tipo MIME (apenas jpg, png, webp) e o tamanho máximo (ex: 2MB) dos arquivos enviados para evitar execução de scripts maliciosos. | Crítica |
| **RNF014** | **Permissões (ACL)** | As rotas administrativas e de edição devem ser protegidas por Middlewares que verifiquem o Título e as permissões do usuário. | Crítica |

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
