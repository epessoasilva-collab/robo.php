<?php
// robo.php — busca a programação e gera o dados.txt
// Fonte: AdoroCinema (exemplo simplificado; pode precisar de ajustes se o site mudar)

$html = file_get_contents('https://www.adorocinema.com/filmes/numero-cinemas/');
if (!$html) { exit("Erro ao acessar o AdoroCinema\n"); }

// Extrai os títulos dos filmes (exemplo com regex; o ideal é usar DOMDocument)
preg_match_all('/<h2 class="meta-title">.*?<a[^>]*>(.*?)<\/a>/s', $html, $matches);
$titulos = array_unique($matches[1]);

$linhas = ["# titulo|faixa|genero|sinopse|trailer|cinema|endereco|bairro|regiao|preco|horarios"];

// Para cada filme, você precisaria buscar os detalhes (cinema, horário, etc.)
// Este é um exemplo mínimo; a implementação real varia conforme a fonte.
foreach ($titulos as $titulo) {
    // Dados fictícios para exemplo — substitua pela lógica real de extração
    $linhas[] = "$titulo|14|Ação|Sinopse de exemplo.|-|Cinema Exemplo|Rua Exemplo, 123|Centro|Centro|Inteira R$ 30|14:00;16:30;19:00";
}

file_put_contents('dados.txt', implode(PHP_EOL, $linhas) . PHP_EOL);
echo "dados.txt gerado com " . count($titulos) . " filmes.\n";
