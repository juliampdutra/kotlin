1. Passagem de parâmetros obrigatórios na tela de Perfil
   
O que foi implemtado?
-> composable(route = "perfil/{nome}") {
   val nome: String? = it.arguments?.getString("nome", "Convidado")
   PerfilScreen(modifier = Modifier.padding(innerPadding), navController, nome!!)
Representa a transição de uma navegação estática para uma navegação dinâmica e baseada em dados.
A principal evolução foi em permitir que as telas do aplicativo (como "Perfil" e "Pedidos") deixassem de ser genéricas e passassem a exibir informações específicas fornecidas pelo usuário em telas anteriores.

Como a navegação foi configurada?
Rotas Obrigatórias: Utilizam barras (/) e chaves {} para definir o argumento. Exemplo: "perfil/{nome}". 
A rota foi alterada de uma String estática para uma dinâmica: composable(route = "perfil/{nome}").

Como os parâmetros são enviados e recebidos?
Enviando Parâmetros
O envio utiliza Template Strings (interpolação) do Kotlin para inserir as variáveis diretamente na URL da rota.
Exemplo Obrigatório: navController.navigate("perfil/$nomeDigitado"). - / para obrigatório
Exemplo Opcional: navController.navigate("pedidos?usuario=$nomeDigitado"). - ? para opcional
Recebendo Parâmetros
- Extração: O código utiliza it.arguments?.getString("nome") para extrair o valor enviado.
- Tratamento de Nulos: Para parâmetros opcionais, define-se um valor padrão caso o dado esteja ausente.
  
O que foi implementado?
onClick = { navController.navigate("perfil/Julia Dutra") },
Foi implementada a refatoração da rota de Perfil para suportar a passagem de parâmetros obrigatórios.
A interface deixa de ser genérica e passa a ser reativa ao estado, construindo a tela de perfil especificamente com as informações fornecidas pelo usuário.

Como a navegação foi configurada?
- Evolução da Rota: A rota, que antes era apenas "perfil", foi alterada para "perfil/{nome}".
- Obrigatoriedade: O uso das chaves {} indica que a informação do nome é indispensável para que a navegação ocorra com sucesso.
- Identificação de Argumentos: O sistema agora reconhece que qualquer valor inserido após a barra na URL da navegação deve ser tratado como a variável nome.

Como os parâmetros são enviados e recebidos?
Enviando: Na tela de origem, a navegação é chamada utilizando a interpolação de strings do Kotlin (Template Strings), montando a rota como navController.navigate("perfil/$nomeDigitado")
Recebendo: Dentro do bloco composable, o parâmetro é recuperado através do objeto it.arguments.

2. Passagem de parâmetros opcionais na tela de Pedidos.
   
O que foi implementado?
composable(
    route = "pedidos?cliente={cliente}",
    arguments = listOf(navArgument("cliente") {
    defaultValue = "Cliente Genérico"
        })
   ) {
 PedidosScreen(modifier = Modifier.padding(innerPadding), navController, it.arguments?.getString("cliente"))
 A alteração substitui uma navegação estática por uma lógica onde a interface se torna reativa aos dados fornecidos.

 Como a navegação foi configurada?
A configuração foi ajustada para suportar parâmetros opcionais, garantindo que a rota seja encontrada mesmo sem o envio de dados.

Como os parâmetros são enviados e recebidos?
Enviando: A tela pode ser chamada de duas formas: com dado ("pedidos?cliente=Julia") ou sem dado ("pedidos").
Recebendo: O código utiliza o it.arguments?.getString("cliente") para extrair o valor de dentro.

O que foi implementado?
 PerfilScreen(
     modifier = Modifier.padding(innerPadding),
     navController,
     nome!!
 )
A alteração substitui uma navegação estática por uma lógica onde a interface se torna reativa aos dados fornecidos.

Como a navegação foi configurada?
O código foi organizado para que os parâmetros sejam passados de forma explícita para o construtor da tela.
O sistema utiliza o identificador "nome" para garantir que a informação correta seja vinculada à variável correspondente
A configuração assegura que a tela de perfil só seja renderizada após a definição dos parâmetros necessários pela rota anterior.

Como os parâmetros são enviados e recebidos?
Enviados: A variável nome!! é o parâmetro que está sendo passado para a função PerfilScreen.
Recebido: O código utiliza a instrução val nome: String? = it.arguments?.getString("nome", "Convidado") para recuperar ou extrair o valor que foi transportado pela rota de navegação.

O que foi implementado?
fun PedidosScreen(modifier: Modifier = Modifier, navController: NavController, cliente: String?) {
text = "PEDIDOS - $cliente",
A tela deixa de mostrar apenas "PEDIDOS" para exibir informações personalizadas de acordo com o parâmetro fornecido.

Como a navegação foi configurada?
A função PedidosScreen foi modificada para aceitar um novo parâmetro chamado cliente, do tipo String?
Ao definir o parâmetro como opcional (String?), a tela mantém a compatibilidade com rotas que podem ou não enviar essa informação.

3. Inserindo valor ao parâmetro opcional na tela de Pedidos

O que foi implementado?
onClick = { navController.navigate("pedidos?cliente=Cliente ABCD") },
Substitui uma navegação estática por uma lógica onde a interface se torna reativa aos dados fornecidos

Como a navegação foi configurada?
A configuração no botão de navegação foi ajustada para utilizar a estrutura de parâmetros opcionais.

Como os parâmetros são enviados e recebidos?
Enviando: Na ação de clique (onClick), o comando navController.navigate("pedidos?cliente=Cliente XPTO") é executado. 
Este comando "empacota" a String "Cliente ABCD" e a envia através da URL de navegação.

4. Passagem de múltiplos parâmetros

O que foi implementado?
  PedidosScreen(
        modifier = Modifier.padding(innerPadding),
         navController,
         it.arguments?.getString("cliente")
   )
   Foi realizada a transição de uma navegação estática para uma dinâmica e baseada em dados.

Como a navegação foi configurada?
O código utiliza o bloco composable para definir como a tela de Pedidos deve ser instanciada.
A configuração garante que a tela de destino (PedidosScreen) receba apenas os dados necessários.

Como os parâmetros são enviados e recebidos?
Recebendo: O código utiliza it.arguments?.getString("cliente") para extrair o valor que foi transportado pela rota.
Enviando: O valor extraído é enviado (passado como argumento) diretamente para a função PedidosScreen(...)

O que foi implementado?
composable(
  route = "perfil/{nome}/{idade}",
  arguments = listOf(
    navArgument("nome") { type = NavType.StringType },
    navArgument("idade") { type = NavType.IntType }
    )
 ) {
 A alteração representa a transição de uma navegação estática para uma navegação dinâmica e baseada em dados.

Como a navegação foi configurada?
A rota foi definida como "perfil/{nome}/{idade}", estabelecendo uma estrutura onde a ordem dos valores é fundamental.
Foi incluída uma lista de argumentos para definir o tipo de cada dado, como NavType.StringType para o nome e NavType.IntType para a idade. Isso garante que o sistema saiba como tratar cada informação individualmente.

Como os parâmetros são enviados e recebidos?
Enviando: O código encaminha os valores armazenados nas variáveis para o componente visual através da chamada PerfilScreen(navController, nome!!, idade!!).
Recebendo: As funções incluem valores padrão para garantir que o app não quebre caso os dados estejam ausentes. (Funções: it.arguments?.getInt("idade", 0) e it.arguments?.getString("nome", "Convidado")

O que foi implementado?
onClick = { navController.navigate("perfil/Julia Dutra/20") },
nome: String,
idade: Int
text = "PERFIL - $nome tem $idade anos",
O botão para o perfil ficar mais específico
Adicionou 2 variaveis de nome e idade
Adicionou no texto de Perfil para que mostre para o usuario algo como "Julia tem 20 anos"

Como a navegação foi configurada?
A rota é definida como "perfil/{nome}/{idade}", onde cada par de chaves indica um argumento obrigatório.
Os argumentos são listados para garantir que o sistema saiba tratar o "nome" como StringType e a "idade" como IntType.
Como a rota utiliza barras (/), a ordem é fundamental. O primeiro valor após a barra de perfil será sempre lido como nome, e o segundo como idade.

Como os parâmetros são enviados e recebidos
Enviando: Na tela de origem, a passagem é feita através do comando navController.navigate("perfil/Julia Dutra/20"). Aqui, os dados reais são inseridos diretamente na String da rota.
Recebendo: it.arguments?.getString("nome") para o nome e it.arguments?.getInt("idade") para a idade.






