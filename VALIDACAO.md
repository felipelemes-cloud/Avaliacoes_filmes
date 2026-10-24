## Versão sem cadastro de filmes

Tela, item do menu, navegação, inclusão de filmes e envio de capas removidos do aplicativo. Catálogo, contas e avaliações preservados. Compilação completa com alvo Java 17 aprovada.

# Histórico de validação

- Compilação integral dos cinco arquivos com JDK 21 usando `--release 17`: aprovada.
- Driver MySQL Connector/J 8.4.0 incluído e carregado via JDBC.
- Integração real com MariaDB 10.4.32 do XAMPP em localhost:3306: aprovada.
- Foi criado um banco temporário exclusivo para testes, removido ao final. Nenhum banco existente foi modificado.
- SQL executado duas vezes: tabelas e gêneros inicializados sem duplicação.
- Cadastro/login, rejeição de senha incorreta e e-mail duplicado: aprovados.
- Contas comuns sem privilégios administrativos; promoção explícita e cadastro administrativo: aprovados.
- Cadastro e leitura de filmes, gêneros e texto com acentos/emoji: aprovados.
- Cópia local da capa: aprovada.
- Criar e editar avaliação sem duplicar, limites de nota/comentário e histórico: aprovados.
- Alteração de nome e consulta de nomes públicos: aprovadas.
- Exclusão própria e bloqueio da exclusão de avaliação de outra conta: aprovados.
- Encerramento de sessão e bloqueio de consulta sem login: aprovados.

Limitações: a interface Swing não recebeu inspeção visual nem um teste manual completo. Não foi feita importação de dados remotos, pois o ZIP original não incluía exportação. A validação real usou MariaDB do XAMPP, não uma instância Oracle MySQL independente.

## Catálogo local de 25 filmes
Importação transacional realizada no cinerate. Todos os 25 registros foram lidos e comparados aos metadados; todas as 25 imagens são legíveis pelo ImageIO. Capas copiadas para a instalação extraída em Downloads e para este pacote. Nenhuma conta ou avaliação foi alterada na importação.

