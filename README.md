# Casa Danielle API - Desafio Tecnico

API Django para gestao de pessoas em casa de apoio, com dashboard web, filtros e exportacao de relatorio em PDF.

## Objetivo
Fornecer uma API REST e uma tela de acompanhamento operacional para cadastro, consulta e monitoramento de pessoas atendidas.

## Tecnologias
- Python
- Django 4.2.29
- Django REST Framework 3.15.1
- drf-yasg (Swagger)
- django-filter
- django-cors-headers
- django-simple-history
- reportlab
- pillow
- python-dotenv
- SQLite

## Como rodar localmente
1. Clone o repositorio
```bash
git clone <URL_DO_REPOSITORIO>
cd <PASTA_DO_PROJETO>
```

2. Crie e ative ambiente virtual
```bash
python -m venv .venv
source .venv/bin/activate
# Windows: .venv\Scripts\activate
```

3. Instale dependencias
```bash
pip install -r requirements.txt
```

4. Crie o arquivo `.env`
```env
SECRET_KEY=sua_chave
DEBUG=True
ALLOWED_HOSTS=127.0.0.1,localhost
```

5. Rode migracoes e servidor
```bash
python manage.py makemigrations
python manage.py migrate
python manage.py runserver
```

## Rotas principais
- Admin: `http://127.0.0.1:8000/admin/`
- Swagger: `http://127.0.0.1:8000/swagger/`
- Dashboard: `http://127.0.0.1:8000/dashboard`
- Exportacao PDF: rota nomeada `exportar_pdf`

## API de Pessoas (PersonViewSet)
Recursos disponiveis:
- Filtros: `cpf`, `gender`
- Busca: `name`
- Ordenacao: `name`

Exemplos:
```http
GET /people/?search=maria
GET /people/?gender=F
GET /people/?ordering=name
GET /people/?cpf=12345678900
```

## Dashboard
Rota publica: `/dashboard`.

Funcionalidades:
- Filtro por nome
- Filtro por genero
- Indicador de total
- Distribuicao por genero
- Link para documentacao da API
- Botao para exportar PDF

## Exportacao PDF
A view `exportar_pacientes_pdf` gera o arquivo `relatorio_casa_danielle.pdf` com:
- titulo do relatorio
- listagem de pessoas
- quebra automatica de pagina

## Melhorias implementadas
### 1) Relatorio PDF
**User Story:** Como gestor da casa de apoio, eu quero exportar um relatorio em PDF, para compartilhar dados de atendimento com rapidez.

**Criterios de aceitacao:**
- Download do PDF funcionando
- Conteudo com cabecalho e lista de pessoas
- Paginacao funcionando

### 2) Filtros no dashboard
**User Story:** Como operador da casa, eu quero filtrar por nome e genero no dashboard, para encontrar informacoes com agilidade.

**Criterios de aceitacao:**
- Filtro por nome com busca parcial
- Filtro por genero correto
- Indicadores respeitam filtros aplicados

### 3) API com busca e ordenacao
**User Story:** Como desenvolvedor consumidor da API, eu quero endpoints pesquisaveis e ordenaveis com Swagger, para integrar o front-end com menos erro.

**Criterios de aceitacao:**
- Endpoint visivel no Swagger
- Busca por nome funcionando
- Filtros por cpf e gender funcionando
- Ordenacao por name funcionando

## Observacoes
- Em producao, usar `DEBUG=False`.
- Restringir `ALLOWED_HOSTS` e CORS em ambiente produtivo.
- Nao versionar `__pycache__` e `*.pyc`.
- Se necessario, migrar de `drf-yasg` para `drf-spectacular`.
