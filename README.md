<div align="center">

# 🎬 CineRate

**Sistema de Avaliação de Filmes**

Aplicativo desktop desenvolvido em **Java Swing**, integrado ao **MySQL local do XAMPP**.

**Avalie • Descubra • Compartilhe**

</div>

---

## 📖 Sobre o projeto

O **CineRate** permite explorar um catálogo de filmes, visualizar capas e informações e publicar avaliações com notas e comentários. Cada usuário pode consultar e gerenciar suas próprias avaliações.

Projeto desenvolvido para as **Atividades Práticas Supervisionadas (APS)** do curso de Sistemas de Informação.

A versão atual acompanha um catálogo de **25 filmes** e suas capas. O cadastro de novos filmes pelo aplicativo foi removido.

## ✨ Funcionalidades

- **Login e cadastro:** contas locais, com autenticação no banco de dados e senhas protegidas por hash.
- **Catálogo de filmes:** capas, títulos, gêneros, ano de lançamento e duração em minutos.
- **Busca e filtros:** pesquisa por título e seleção por gênero.
- **Avaliações:** notas de **0 a 5 estrelas**, com intervalos de meia estrela, e comentários de até **1.000 caracteres**.
- **Meu perfil:** alteração do nome e histórico de avaliações, com opções para editar e excluir.
- **Avaliações da comunidade:** consulta às notas e aos comentários publicados para cada filme.

Cada conta pode manter **uma avaliação por filme**. Ao avaliar novamente o mesmo filme, a avaliação existente é atualizada.

## 🛠️ Tecnologias utilizadas

- **Java 17 ou superior**.
- **Java Swing** para a interface gráfica.
- **JDBC** para a comunicação com o banco.
- **MySQL Connector/J 8.4.0**, incluído na pasta `lib/`.
- **MySQL/MariaDB do XAMPP** para armazenamento local.
- **phpMyAdmin** para importar os scripts SQL e consultar o banco.

## 📂 Organização do projeto

O código está organizado em **cinco arquivos Java**, agrupando responsabilidades relacionadas para facilitar a leitura e a manutenção.

```text
CineRate/
├── avaliacao_filmes.java   # Inicialização e navegação
├── TelasUsuario.java       # Login, cadastro e perfil
├── TelasFilmes.java        # Catálogo, detalhes e avaliações
├── Supabase.java           # Autenticação e persistência via JDBC/MySQL
├── Estilo.java             # Cores, componentes, estrelas e imagens
├── database.properties     # Configuração da conexão local
├── inicializar.sql         # Criação do banco, tabelas e gêneros
├── catalogo.sql            # Importação dos 25 filmes
├── iniciar.bat             # Compilação e execução no Windows
├── lib/
│   └── mysql-connector-j-8.4.0.jar
├── capas/
│   └── catalogo/           # Capas dos filmes incluídos
├── CATALOGO.md             # Relação dos filmes e referências
├── VALIDACAO.md            # Registro das verificações realizadas
└── README.md
```

A pasta `build/` é criada automaticamente ao executar `iniciar.bat` e contém os arquivos compilados.

### Responsabilidades dos arquivos

| Arquivo | O que faz |
| :--- | :--- |
| `avaliacao_filmes.java` | Inicia o aplicativo e controla a navegação entre as telas. |
| `TelasUsuario.java` | Reúne as telas de login, criação de conta e perfil do usuário. |
| `TelasFilmes.java` | Exibe o catálogo, os detalhes dos filmes e as avaliações. |
| `Supabase.java` | Autentica usuários e consulta/grava dados no MySQL usando JDBC e consultas parametrizadas. |
| `Estilo.java` | Padroniza cores, botões, campos, estrelas e carregamento das capas; executa tarefas em segundo plano. |

> **Sobre o nome `Supabase.java`:** o arquivo manteve o nome da versão anterior por compatibilidade com as telas. A implementação atual utiliza MySQL local e não depende do Supabase.

## 🗄️ Banco de dados

O banco utilizado pelo projeto se chama **`cinerate`**.

| Tabela | Finalidade |
| :--- | :--- |
| `usuario` | Identificação, nome, e-mail e hash da senha de cada conta. |
| `genero` | Categorias dos filmes, utilizadas no catálogo e nos filtros. |
| `filme` | Título, ano de lançamento, duração, gênero e caminho da capa. |
| `avaliacao_web` | Notas e comentários associados a filmes e usuários, com datas de criação e atualização. |

Os filmes estão relacionados aos gêneros. Cada avaliação está vinculada a um filme e a um usuário, com restrição de uma avaliação por conta e filme.

A autenticação é feita localmente. As senhas são armazenadas com **PBKDF2-HMAC-SHA256**, salt aleatório e **210.000 iterações**.

As capas incluídas ficam na pasta **`capas/catalogo/`**. O campo **`imagem_url`**, da tabela `filme`, armazena o caminho do arquivo, e não a imagem em formato binário. Preserve essa pasta junto do aplicativo ao mover o projeto.

### Configuração da conexão

O arquivo `database.properties` contém a configuração padrão para o XAMPP local:

```properties
db.host=localhost
db.port=3306
db.name=cinerate
db.user=root
db.password=
```

Se o MySQL do computador usar outra porta, usuário ou senha, ajuste esse arquivo. A senha vazia acima é a configuração da conexão local com o banco; cada conta do CineRate possui sua própria senha.

## ▶️ Como executar

### 1. Preparar o ambiente

- Instale o **JDK 17 ou superior** e disponibilize `java` e `javac` no PATH.
- Extraia o projeto completo, incluindo as pastas `lib/` e `capas/`.
- No painel do **XAMPP**, inicie o serviço **MySQL**.

### 2. Inicializar o banco

Na primeira instalação:

1. Inicie também o **Apache** no XAMPP para utilizar o phpMyAdmin.
2. Acesse **http://localhost/phpmyadmin**.
3. Abra a opção **Importar** e execute o arquivo **`inicializar.sql`**. Ele cria e seleciona o banco `cinerate` e prepara as tabelas e os gêneros.
4. Importe o arquivo **`catalogo.sql`** para preencher o catálogo com os 25 filmes.

Se o banco e o catálogo já estiverem configurados neste computador, não é necessário repetir a importação. Não é preciso apagar outros bancos ou tabelas.

### 3. Abrir o aplicativo

Dê dois cliques em **`iniciar.bat`**. O arquivo compila os fontes e inicia o CineRate.

Na tela inicial, entre com uma conta existente ou clique em **Criar uma conta**. O cadastro é local e não exige confirmação por e-mail.

O aplicativo se conecta diretamente ao MySQL. O Apache é necessário apenas para acessar o phpMyAdmin.

### Executar pelo terminal

No Prompt de Comando, dentro da pasta do projeto:

```bat
mkdir build
javac -encoding UTF-8 --release 17 -cp "lib/*" -d build *.java
java -cp "build;.;lib/*" avaliacao_filmes
```

Se a pasta `build/` já existir, pule o primeiro comando.

### Executar em uma IDE

Abra a pasta como projeto Java, selecione um **JDK 17+**, adicione `lib/mysql-connector-j-8.4.0.jar` às bibliotecas e execute a classe **`avaliacao_filmes`**. Defina a pasta do projeto como diretório de trabalho para localizar `database.properties` e as capas.

## 🔧 Solução de problemas

| Problema | O que verificar |
| :--- | :--- |
| Falha de conexão com o banco | Confirme que o MySQL está iniciado no XAMPP e que a porta está correta. |
| Banco ou tabela inexistente | Importe `inicializar.sql` e confira `db.name`. |
| Catálogo vazio | Importe `catalogo.sql` no banco `cinerate`. |
| Acesso negado ao MySQL | Confira `db.user` e `db.password` em `database.properties`. |
| Driver JDBC não encontrado | Verifique a pasta `lib/` e execute pelo `iniciar.bat`, ou adicione o JAR à IDE. |
| `javac` não encontrado | Confira a instalação do JDK e a configuração do PATH. |
| Capas indisponíveis | Preserve `capas/catalogo/` e execute a partir da pasta do projeto. |

## ✅ Validação

O projeto foi compilado com alvo **Java 17** e testado com o **MariaDB 10.4.32 do XAMPP**. As verificações incluíram autenticação, perfil, operações de avaliações e leitura dos 25 filmes e suas capas. A versão sem cadastro de filmes também teve sua compilação validada.

Consulte **`VALIDACAO.md`** para o histórico e as limitações dos testes, e **`CATALOGO.md`** para a relação dos filmes e suas referências.
