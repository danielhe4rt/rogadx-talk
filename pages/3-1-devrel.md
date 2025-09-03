---
layout: statement
layoutClass: gap-16
---

# Você já ouviu o termo aplicação "Legada"

<v-click>
  
## Provavelmente sim! Mas vamo quebrar isso um pouco.

</v-click>

---
layout: two-cols
layoutClass: gap-16
---

## Provavelmente você já viu algum meme do tipo

<h3 class="my-3 text-gray-100"> Tipos de Cagadas "Legadão" </h3>

<v-clicks class="text-gray-200" depth="2">


- *Hadouken*
- *Bug Buy*
- *SQL Injection 4Noobs*
- *Comentários*
- *Integrações Duvidosas*
- **Entre vários outros**

</v-clicks>

::right:: 

## Snippet

<br>

<div v-if="$clicks == 1">

```php
$tempo = rand(1, 20); // Tempo aleatório de carregamento
echo "Carregando Hadouken por {$tempo} segundos...\n";

if ($tempo > 0) {
    if ($tempo < 5) {
        echo "Energia baixinha... 🤏\n";
        if ($tempo == 1) {
            echo "Só um espirro de energia. 😅\n";
        } else {
            if ($tempo == 2) {
                echo "Quase nada ainda...\n";
            } else {
                if ($tempo == 3) {
                    echo "Tá crescendo... um pouco. 💪\n";
                } else {
                    echo "Quase lá...\n";
                }
            }
        }
    }
}

```
</div>

<div v-if="$clicks == 2">

```php
// Sistema de compra FODA 100% aprovado
// Por: juninhogameplays-senior-dev-confia

try {
    processarPagamento();
    atualizarEstoque();
    enviarNotaFiscal();
} catch (Exception $e) {
    // Nada, absolutamente nada. 
    // O cliente vai ver "Processando..." pra sempre.
    // Talvez receber um tijolo numa caixa de sapato?
}
```

</div>
<div v-if="$clicks == 3">
  
```php
public function criarTreta()
{
    // Recebendo dados direto da request sem validação
    $titulo = $_POST['titulo'];
    $descricao = $_POST['descricao'];

    // confiando cegamente no cliente
    $usuario = $_POST['usuario']; 

    // Concatenando SQL na mão, vulnerável a SQL Injection
    $db = new PDO('mysql:host=localhost;dbname=treta_db', 'root', '');
    $db->query("
      INSERT INTO tretas (titulo, descricao, usuario) 
        VALUES 
      ('$titulo', '$descricao', '$usuario')
    ");

    echo "Treta criada!"; // sem status code, sem JSON, só na fé
}
```
</div>

<div v-if="$clicks == 4">
  
```php
// // Antigo sistema de login ultra-secreto 🤐
// // $usuario = $_POST['usuario'];
// // $senha = $_POST['senha'];
// // if ($usuario == "admin" && $senha == "1234") {
// //     // echo "Bem-vindo, admin!";
// //     // // Redireciona para a dashboard (hoje nem tem mais dashboard...)
// //     // header("Location: /painel");
// // } else {
// //     // echo "Acesso negado.";
// // }

// // Backup da função de cálculo do imposto, mas ninguém usa isso faz 2 anos 😴
// // function calculaImposto($valor) {
// //     $aliquota = 0.27;
// //     $imposto = $valor * $aliquota;
// //     return $imposto;
// // }

// // // Sistema antigo de envio de email com mail()
// // // $to = "cliente@example.com";
// // // $subject = "Confirmação do pedido";
// // // $message = "Seu pedido foi confirmado!";
// // // $headers = "From: noreply@example.com";
// // // mail($to, $subject, $message, $headers);
```

</div>

<div v-if="$clicks == 5">

```php
$url = "https://api.exemplo.com/v1/dados";
$apiKey = "SUA_API_KEY_AQUI_VERSIONADA_PQ_SIM";

$ch = curl_init();

curl_setopt($ch, CURLOPT_URL, $url);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_HTTPHEADER, [
    "Authorization: Bearer {$apiKey}",
    "Accept: application/json"
]);

$response = curl_exec($ch);
curl_close($ch);

// Sem validação, sem ver se veio ok
echo $response;
```

</div>

<!-- - Communities are everywhere, and we often participate without even realizing it. -->
<!-- - These communities shape our experiences and skills. -->

---
layout: quote
layoutClass: gap-16
---

# Mas como isso chega nesse ponto?

Aquele pensamento quando você chega e ve a casa que tu vai morar desarrumadassa?

<v-click>

> QUEM FOI O CORNO QUE FEZ ESSA BAGUNÇA?? - Chegando em Casa, Você. 

</v-click>
---
layout: center
layoutClass: gap-16
---

# Decisões mal pensadas viram padrão

“Vamos fazer rapidinho aqui e depois refatorar...”

<v-click>

> E nunca mais refatorou 😅

</v-click>

---
layout: center
layoutClass: gap-16
---

# Decisões mal pensadas viram padrão

Deixa só essa senha hardcoded... é só um teste

<v-click>

> E foi pra produção 🤡

</v-click>

---
layout: center
layoutClass: gap-16
---

# Crescimento desorganizado

A aplicação começou pequena e agora não escala mais

<v-click>

> O caos chegou antes da refatoração 🚀

</v-click>

---
layout: center
layoutClass: gap-16
---

# Falta de disciplina e boas práticas

Sem versionamento correto, sem testes, sem documentação

<v-click>

> O famoso: “Confia que tá funcionando, mas se eu sair do time problema é de vocês” 🤷‍♂️

</v-click>

---
layout: center
layoutClass: gap-16
---

# Falta de disciplina e boas práticas

Cada um codando do jeito que quiser

<v-click>

> Até os bugs são personalizados 🤣

</v-click>

---
layout: center
layoutClass: gap-16
---

# O “herói” da equipe

Resolve tudo na base da gambiarra ("funciona na minha máquina")

<v-click>

> Até a bomba explodir 🎇

</v-click>

---
layout: center
layoutClass: gap-16
---

# O “herói” da equipe

Soluções temporárias viram definitivas

<v-click>

> E ninguém mais quer mexer depois 🏃‍♂️💨

</v-click>

---
layout: center
layoutClass: gap-16
---


## E o MAIOR VILÃO DE TODOS

<v-click>

# LGTM? APROVA AI QUE AQUI DEU BOM

</v-click>

<v-click>

> LGTM!! APROVADO PODE MERGEAR!!! - Que Não Revisou, Revisor

</v-click>



---
layout: quote
layoutClass: gap-16
---

# Sabe quem passou por todas essas etapas?

## Eu, provavelmente você, e muitos outros vão passar também!

<br>

> E tá tudo bem! Ninguém nasce sabendo, mas a parada é: vamo continuar repetindo isso até quando?


---
layout: quote
layoutClass: gap-16
---

# O problema é quando:

<v-click>

## 1. Você vê acontecendo e não opina por motivos

<br>
</v-click>

<v-click>

### 2. Você tá revisando e tem medo de apontar por insegurança

<br>
</v-click>

<v-click>

#### 3. Você tá vendo a MERDA acontecer mas tem medo de ser demitido

<br>
</v-click>

<v-click>

> Você realmente deveria começar a se impor. Isso é mais que sênioridade, mas criar maturidade num ambiente profissional.

</v-click>