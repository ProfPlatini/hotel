## Execução
- Backend e ponto de entrada: `app.py`; frontend está em `static/index.html`, servido por `GET /`.
- Ambiente Windows já incluído em `.venv`: `.venv\Scripts\python.exe -m pip install -r requirements.txt` e `.venv\Scripts\python.exe app.py`.
- O Flask escuta em `0.0.0.0:8000` com `debug=True`.
- Não há testes, lint, build, CI ou outro executor configurado; a verificação disponível é iniciar o servidor e exercitar as rotas.

## Configuração
- `app.py` chama `load_dotenv()` e exige `SUPABASE_URL`, `SUPABASE_KEY` e a chave da API da OpenAI no ambiente; não leia nem exponha `.env`.
- O cliente Supabase é criado na importação e usa a tabela `reservas`; sem credenciais válidas o backend não inicia corretamente.

## Contratos E Arquitetura
- `app.py` concentra Flask, Agno (`OpenAIChat` com `gpt-4o-mini`), Supabase e todas as rotas; não há separação em pacotes.
- `POST /agente` e `POST /perguntar` recebem JSON com `pergunta` e chamam o mesmo agente, mas retornam chaves diferentes: `resposta` e `mensagem`, respectivamente.
- `POST /reservas` insere o JSON recebido em `reservas`; `GET /reservas` retorna os registros da tabela. O frontend usa diretamente `/agente` e `/reservas`.
- Não altere a `description` do agente: ela é a fonte dos quartos, preços e serviços também apresentados no frontend.

## Restrições
- Preserve a lógica e o comportamento existentes quando a tarefa não pedir explicitamente uma mudança; não adicione dependências sem necessidade.
- Responda em PT-BR e mantenha comentários curtos em código novo quando ajudarem iniciantes a entender a lógica.
