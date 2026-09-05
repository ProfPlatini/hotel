## Stack principal
- Linguagem de programação: Python
- Frameworks: Agno, OpenAi, Supabase, Flask, Flask-Cors
- FrontEnd: HTML, CSS e JS

## Como rodar
- Executar o servidor: `python app.py` (sobe Flask na porta `8000`).
- Usar o ambiente virtual já existente: `.venv` (ativação: `.venv\Scripts\activate` no Windows).
- Não há `requirements.txt` nem build/lint/test configurados; o projeto não tem testes nem CI.

## Arquitetura
- `app.py` é o único backend (single-file): contém o agente Agno (OpenAIChat `gpt-4o-mini`), o cliente Supabase e todas as rotas Flask.
- Frontend fica em `static/index.html` (CSS e JS inline, sem bibliotecas). É servido na rota raiz `/` via `app.send_static_file`.
- Config do Supabase vem do `.env` (`SUPABASE_URL`, `SUPABASE_KEY`) via `load_dotenv()`.
- Rotas: `POST /agente` e `POST /perguntar` (duplicadas, ambas chamam `agente.run`), `POST /reservas` (insere na tabela `reservas` do Supabase) e `GET /reservas` (lista reservas).

## Railguards
- Não alterar a lógica do projeto.
- Não alterar e criar arquivos sem pedir permissão.
- Não instalar bibliotecas desnecessárias.
- Não expor e não ler arquivos do `.env` e do `.gitignore`.
- Não alterar a `description` do agente de hotel (contém quartos, preços e serviços citados também no frontend).

## Preferências
- Responder sempre em PT-BR.
- Colocar comentários nos códigos, facilitando a leitura de um programador iniciante.
