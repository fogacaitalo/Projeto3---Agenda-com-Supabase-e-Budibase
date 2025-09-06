Agenda de Contatos Institucionais
Este projeto é uma aplicação web criada para substituir uma planilha de contatos complexa. A solução foi desenvolvida utilizando a plataforma low-code Budibase como interface de usuário (frontend) e o Supabase como banco de dados (backend), proporcionando um sistema seguro, eficiente e fácil de usar.

O objetivo principal foi transformar uma lista de contatos estática e frágil em uma aplicação dinâmica com funcionalidades de busca, edição controlada e múltiplos níveis de acesso para usuários.

✨ Funcionalidades Principais
Gerenciamento Completo de Contatos (CRUD): Adicione, visualize, edite e delete contatos através de uma interface intuitiva.

Categorização por Origem: Contatos são classificados em grupos maiores (ex: Associações, Autarquias, Autoridades Militares) para melhor organização.

Busca Inteligente: Um campo de busca que filtra em tempo real a tabela de contatos, pesquisando em múltiplas colunas (nome, cargo, e-mail, origem) sem diferenciar maiúsculas de minúsculas.

Controle de Acesso Baseado em Permissões (RBAC): A aplicação conta com três níveis de acesso de usuário:

Leitor (leitor): Apenas visualiza os contatos.

Editor (editor): Pode visualizar, adicionar e editar contatos.

Administrador (admin): Permissão total, incluindo a capacidade de deletar contatos.

Segurança de Credenciais: As chaves de conexão com o banco de dados são gerenciadas de forma segura através de "Bindings" (variáveis de ambiente), garantindo que nenhuma informação sensível seja exposta no código-fonte.

🛠️ Tecnologias Utilizadas
Frontend (Interface): Budibase

Backend (Banco de Dados): Supabase (PostgreSQL)

🚀 Como Configurar e Rodar o Projeto
Para rodar este projeto, você precisará de uma conta no Supabase e uma no Budibase.

1. Configuração do Backend (Supabase)
Crie um novo projeto no Supabase.

Guarde bem as credenciais do seu banco de dados (Host, Nome do Banco, Usuário, Senha).

No seu projeto Supabase, vá para o "SQL Editor" e execute o script abaixo para criar toda a estrutura de tabelas necessária:

SQL

-- Tabela para as Origens (Grupos Maiores)
CREATE TABLE origens (
    id_origem SERIAL PRIMARY KEY,
    nome_origem VARCHAR(255) NOT NULL UNIQUE
);

-- Tabela para os Contatos
CREATE TABLE contatos (
    id_contato SERIAL PRIMARY KEY,
    nome VARCHAR(255),
    cargo TEXT,
    telefone VARCHAR(100),
    email VARCHAR(255),
    nome_origem VARCHAR(255)
);

-- Tabela para os Usuários da Aplicação e suas permissões
CREATE TABLE usuarios (
    id_usuario SERIAL PRIMARY KEY,
    email_usuario VARCHAR(255) NOT NULL UNIQUE,
    nivel_acesso VARCHAR(50) NOT NULL CHECK (nivel_acesso IN ('admin', 'editor', 'leitor'))
);
2. Configuração do Frontend (Budibase)
Crie uma conta no Budibase.

No painel principal, use a opção "Import app" e selecione o arquivo de exportação .budibase deste projeto.

Durante a importação, o Budibase irá detectar que a aplicação precisa de credenciais de banco de dados. Ele solicitará que você preencha os valores para os seguintes "Bindings":

SUPABASE_HOST: O Host do seu banco de dados Supabase.

SUPABASE_DATABASE: O nome do banco (geralmente postgres).

SUPABASE_USER: O usuário do banco (geralmente postgres).

SUPABASE_PASSWORD: A senha do seu banco de dados que você anotou.

Após fornecer as credenciais, finalize a importação.

👤 Uso da Aplicação
Publicar: Dentro do editor do Budibase, clique em "Publish" para que a aplicação fique online.

Cadastrar Usuários: Para que um usuário tenha uma permissão específica, seu e-mail e nível de acesso (admin, editor ou leitor) devem ser cadastrados manualmente na tabela usuarios no Supabase.

Convidar Usuários: No painel de gerenciamento do Budibase, convide os usuários (com a permissão "Basic") para que eles possam acessar a aplicação.
