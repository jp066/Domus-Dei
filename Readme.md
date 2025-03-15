# Domus Dei

**Domus Dei** é um aplicativo mobile desenvolvido para fortalecer e organizar a vida paroquial. Ele reúne funcionalidades para párocos, catequistas, coordenadores e fiéis em um único espaço digital, promovendo comunicação eficiente, organização litúrgica e espiritualidade acessível.

## Índice

- [Visão Geral](#visão-geral)
- [Funcionalidades](#funcionalidades)
- [Tecnologias](#tecnologias)
- [Instalação](#instalação)
- [Uso](#uso)
- [Protótipo](#protótipo)
- [Estrutura do Projeto (Django)](#estrutura-do-projeto-django)
- [Endpoints da API](#endpoints-da-api)
- [Contribuições](#contribuições)
- [Licença](#licença)

## Visão Geral

O Domus Dei organiza a vida da paróquia em duas áreas principais:

- **Área de Gestão**: exclusiva para pároco e equipes da paróquia.      
- **Área Livre**: acessível a todos os fiéis cadastrados.

Ele permite desde o agendamento de sacramentos e a escala de ministérios até a visualização de leituras diárias e envio de pedidos de oração.

## Funcionalidades

### Área de Gestão (restrita)

- **Acesso exclusivo para pároco com verificação única(id próprio) ou diacono (com permissão do pároco):**
  - Gerenciamento de Missas: horários e locais
  - Agendamento de Sacramentos: confissão, batismo, matrimônio, missas particulares.
  - Enquetes com a comunidade
- **Padre e coordenadores (outro acesso único, diferente do padre) tem acesso:**
  - Planejamento semanal (calendário)
  - Notificações automáticas para envolvidos.
  - Catequese Online (materiais, frequência, alunos)
  - Escala de Ministérios (leitores, músicos, coroinhas)
  - Galeria PASCOM (upload de fotos e vídeos)
  - Área de Finanças (somente padre e coordenadores do ministério financeiro).
  - Organização de eventos, encontros e retiros.

### Área Livre (todos os fiéis)

- Pedidos de Oração (com opção anônima)
- Leituras do dia via API externa
- Homilia diária (áudio do pároco)
- Galeria de fotos (visualização e download)
- Localização de missas próximas
- Inscrição em eventos religiosos

## Tecnologias

### Backend

- Django + Django REST Framework (DRF)
- Banco: PostgreSQL (ou SQLite para testes)
- Autenticação: JWT (JSON Web Tokens)
- Django Admin para painel administrativo
- APIs públicas integradas (Liturgia Diária etc.)

### Frontend

- React Native com JavaScript/TypeScript
- Compatível com Android e iOS
- Integração com API RESTful
- Notificações push

### Infraestrutura

- Hospedagem: Railway, Render, DigitalOcean, AWS
- Publicação: Google Play & App Store

## Instalação

### Backend

```bash
git clone https://github.com/seu-usuario/domus-dei-backend.git
cd domus-dei-backend
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
python manage.py migrate
python manage.py runserver
```

### Frontend

```bash
git clone https://github.com/seu-usuario/domus-dei-frontend.git
cd domus-dei-frontend
npm install
npx react-native run-android
```

## Uso

1. Crie superusuário para acesso no admin do Django.
2. Cadastre os perfis: pároco, catequista, coordenadores e fiéis.
3. Acesse o app com login JWT.
4. Utilize os recursos conforme permissões.

## Protótipo

[Figma – Design das telas do app](https://www.figma.com/file/MYLSnPpIAfFonwKLZKE2RZ)

## Estrutura do Projeto (Django)

```
domus_dei_backend/
├── manage.py
├── requirements.txt
├── config/
│   ├── settings.py
│   └── urls.py
├── apps/
│   ├── users/
│   ├── masses/
│   ├── sacraments/
│   ├── catechesis/
│   ├── prayer_requests/
│   ├── readings/
│   ├── ministries/
│   ├── gallery/
│   ├── finances/
│   ├── events/
│   └── notifications/
├── media/
├── static/
└── db.sqlite3
```

## Endpoints da API

### `/api/users/`
- `POST /register/` – Registro de usuário
- `POST /login/` – Login com JWT
- `GET /profile/` – Ver perfil
- `PUT /profile/update/` – Atualizar perfil

### `/api/masses/`
- `GET /nearest/` – Missas próximas
- `GET /` – Lista de missas
- `POST /create/` – Criar missa
- `PUT /update/<id>/` – Atualizar missa
- `DELETE /delete/<id>/` – Remover missa

### `/api/sacraments/`
- `GET /` – Listar agendamentos
- `POST /schedule/confession/` – Agendar confissão
- `POST /schedule/baptism/` – Agendar batismo
- `POST /schedule/marriage/` – Agendar matrimônio
- `POST /schedule/private-mass/` – Agendar missa particular
- `PUT /update/<id>/` – Atualizar agendamento
- `DELETE /delete/<id>/` – Cancelar agendamento

### `/api/catechesis/`
- `GET /students/` – Listar catequizandos
- `POST /students/create/` – Adicionar catequizando
- `POST /materials/upload/` – Upload de material
- `GET /materials/` – Listar materiais
- `POST /attendance/` – Registrar frequência

### `/api/prayer_requests/`
- `GET /` – Listar pedidos
- `POST /create/` – Criar pedido
- `PUT /mark-as-answered/<id>/` – Marcar como atendido

### `/api/readings/`
- `GET /daily/` – Leituras do dia (API externa)
- `POST /homily/upload/` – Enviar homilia
- `GET /homily/` – Listar homilias

### `/api/ministries/`
- `GET /schedule/` – Ver escalas
- `POST /schedule/create/` – Criar escala
- `PUT /schedule/update/<id>/` – Atualizar escala

### `/api/gallery/`
- `GET /albums/` – Ver álbuns
- `POST /albums/create/` – Criar álbum
- `POST /upload/` – Upload de mídia
- `GET /download/<id>/` – Baixar mídia

### `/api/finances/`
- `GET /` – Ver resumo financeiro
- `POST /entry/` – Nova entrada
- `POST /expense/` – Novo gasto
- `DELETE /delete/<id>/` – Remover registro

### `/api/events/`
- `GET /` – Listar eventos
- `POST /create/` – Criar evento
- `POST /subscribe/` – Inscrição
- `GET /participants/<id>/` – Ver inscritos

### `/api/notifications/`
- `GET /` – Ver notificações
- `POST /send/` – Enviar notificação

## Contribuições

Você pode contribuir com novas ideias, melhorias ou correções. Basta abrir uma issue ou enviar um pull request.

## Licença

Projeto licenciado sob a [MIT License](LICENSE).
