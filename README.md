# API de Gestão de Participantes

Este projeto é uma API desenvolvida em Python utilizando o framework FastAPI. Inicialmente, ele foi criado para atender às demandas de um processo seletivo de estágio. Por esse motivo, algumas partes do código original foram modificadas para não expor informações da empresa.

Ainda assim, a proposta principal permanece: oferecer um sistema para importação, listagem, atualização e exclusão de dados de participantes.

A API também implementava um endpoint que simulava o funcionamento de um webhook. No entanto, essa parte foi substituída por um endpoint local, que apenas calcula automaticamente a idade com base na data de nascimento fornecida.

---

## Estrutura do Projeto

```
Teste-API/
├── Teste/
│   ├── __pycache__/
│   ├── database.py
│   ├── main.py
│   └── models.py
├── Cadastros.xlsx
├── .gitattributes
└── README.md
```

---

## Tecnologias utilizadas

- Python 3.9
- FastAPI
- SQLite
- SQLAlchemy
- Pandas
- Requests

---

## Como executar o projeto

1. Navegue até a pasta onde está o projeto:
```bash
cd Teste-API/Teste
```

2. Instale as dependências:
```bash
pip install -r requirements.txt
```

3. Execute o servidor FastAPI:
```bash
uvicorn main:app --reload
```

4. Acesse a documentação interativa:
```
http://127.0.0.1:8000/docs
```

---

## Arquivo Cadastros.xlsx

O arquivo `Cadastros.xlsx`, localizado na raiz do projeto, contém os dados dos participantes fornecidos pelo próprio PDF do processo seletivo. Ele pode ser utilizado para testar o endpoint de importação da planilha.

---

## Endpoints disponíveis

### POST `/upload-excel/`
Importa os dados da planilha Excel enviada. A planilha deve conter as seguintes colunas:

- Nome completo
- Data de Nascimento
- Sexo
- E-mail
- Celular (opcional)

O arquivo esperado deve ser do tipo `.xlsx`.

### GET `/participantes/`
Retorna todos os participantes cadastrados no banco.

Parâmetro opcional:
- `sexo` → Filtra por sexo. Exemplo: `/participantes?sexo=Feminino`

### PUT `/participantes/{id}`
Atualiza a data de nascimento de um participante com base no ID.

Exemplo de corpo JSON:
```json
{
  "nova_data": "2000-01-01"
}
```

### DELETE `/participantes/`
Remove todos os participantes da base de dados.

### POST `/webhook/`
Calcula a idade com base na data de nascimento fornecida.

**Exemplo de entrada:**
```json
{
  "data_nascimento": "1999-05-10"
}
```

### POST `/webhook/`
Calcula a idade com base na data de nascimento fornecida.

**Exemplo de entrada:**
```json
{
  "data_nascimento": "1999-05-10"
}
```

**Exemplo de resposta:**
```json
{
  "idade": 25,
  "status": "Idade calculada com sucesso"
}
```

---

## Observações

- O banco de dados `dados.db` será criado automaticamente na primeira execução da API.
- O campo "Celular" pode estar ausente na planilha, mas é tratado de forma segura no código.
- O projeto está organizado em uma pasta chamada `Teste` dentro do diretório principal.
