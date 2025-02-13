<<<<<<< HEAD
# got-database-project
=======
# Game of Thrones - Database Project

## Sobre o Projeto
Este projeto foi desenvolvido para a disciplina de **Banco de Dados** da **Universidade do Porto** e realizado em grupo.
Este projeto tem como objetivo a modelagem e análise de dados do universo de **Game of Thrones**, incluindo batalhas, casas, personagens e regiões do continente fictício de Westeros.

Utilizamos uma **base de dados relacional** para armazenar informações detalhadas sobre os eventos da série, possibilitando consultas SQL e a visualização dos dados através de uma aplicação Flask.

## Modelagem do Banco de Dados
A modelagem da base de dados foi feita para capturar as principais relações entre os elementos do universo de Game of Thrones:

- **Regions**: O continente de Westeros é dividido em 10 regiões.
- **Houses**: Cada região tem diversas casas, algumas das quais governam territórios.
- **Characters**: Personagens fazem parte das casas e participam das batalhas.
- **Battles**: Eventos onde casas lutam entre si, podendo ter comandantes e estatísticas de tropas.
- **Defenses & Attacks**: Relações entre casas e batalhas, detalhando os lados do conflito.

### Modelo Relacional
Cada entidade do projeto está representada de forma estruturada para facilitar consultas e análises.

- **Regions** (Region_ID, Name, Rulled_by_House_ID)
- **Cities** (City_ID, Name, Region_ID)
- **Houses** (House_ID, Name, Words, Region_ID, City_ID)
- **Characters** (Character_ID, Name, House_ID, is_King)
- **Battles** (Battle_ID, Name, Year, AttackerKing_ID, DefenderKing_ID, Region_ID)
- **Attacks** (Battle_ID, House_ID)
- **Defenses** (Battle_ID, House_ID)

## Tecnologias Utilizadas
- **Python** (Flask, Pandas)
- **SQLite** para armazenamento dos dados
- **HTML + CSS** para a interface
- **Jinja2** para renderização de templates

## Como Rodar o Projeto Localmente
### 1. Clone o repositório
```bash
git clone https://github.com/yanoccoelho/got-database-project.git
cd got-database-project
```

### 2. Crie um ambiente virtual e instale as dependências
```bash
python -m venv venv
source venv/bin/activate  # No Windows: venv\Scripts\activate
pip install -r requirements.txt
```

### 3. Execute a aplicação
```bash
python src/app.py
```

### 4. Acesse no navegador
```
http://localhost:9001/
```

## Consultas SQL Principais
Exemplos de queries utilizadas na aplicação:

1. **Casas mais atacadas**:
```sql
SELECT h.House, COUNT(d.Battle_ID) AS Attacks
FROM Houses h JOIN Defenses d ON h.House_ID = d.DefenderHouse_ID
GROUP BY h.House ORDER BY Attacks DESC;
```

2. **Batalhas mais equilibradas**:
```sql
SELECT Battle_Name, ABS(Attacker_size - Defender_size) AS Size_Diff
FROM Battles WHERE Attacker_size IS NOT NULL AND Defender_size IS NOT NULL
ORDER BY Size_Diff ASC;
```

3. **Taxa de vitória de cada rei**:
```sql
SELECT c.Character_ID, c.Name AS King, COUNT(b.Battle_ID) AS Total_Battles,
       SUM(b.is_attacker_winner) AS Wins,
       ROUND((SUM(b.is_attacker_winner) * 100.0) / COUNT(b.Battle_ID), 2) AS WinRate
FROM Characters c JOIN Battles b ON c.Character_ID = b.AttackerKing_ID
GROUP BY c.Character ORDER BY WinRate DESC;
```

## Estrutura do Repositório
```
got-database-project/
│── data/                  # Dados utilizados no projeto      
│── static/                # Arquivos estáticos (imagens, CSS, JS)
│── templates/             # Templates HTML para a aplicação Flask
│── docs/                  # Relatório do projeto
│── src/                   # Código-fonte
│   ├── app.py             # Script principal da aplicação
│   ├── db.py              # Configuração do banco de dados
│   ├── csvHandler.py      # Manipulação de CSVs
│   ├── server.py          # Inicialização do servidor
│   ├── test_db_connection.py # Testes de conexão
│── got.db                 # Banco de dados SQLite
│── README.md              # Documentação do projeto
│── requirements.txt       # Dependências
│── .gitignore             # Arquivos ignorados
```

## Curiosidades e Insights
- Westeros é um mundo fictício dividido em 10 regiões, cada uma governada por uma casa nobre.
- Algumas casas participaram de diversas batalhas e tiveram diferentes taxas de sucesso.
- Foram utilizadas técnicas de normalização e otimização para melhorar a estrutura do banco de dados.

## Referências
- [Game of Thrones Characters Dataset](https://www.kaggle.com/datasets/ankytastic/game-of-thrones-characters)
- [Game of Thrones Battles Dataset](https://www.kaggle.com/datasets/satyampandey4229/games-of-thrones)
- [Game of Thrones Houses Dataset](https://www.kaggle.com/datasets/neelgajare/463-game-of-thrones-houses-dataset)
- [Game of Thrones Wiki](https://gameofthrones.fandom.com/wiki/Wiki)

>>>>>>> 6ac1573 (Commit completo - Projeto Game of Thrones Database)
