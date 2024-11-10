Projeto de Consulta de Seguro - Validação de Elegibilidade

Este projeto é uma aplicação web interativa desenvolvida em HTML, CSS, JavaScript e jQuery para realizar uma consulta de elegibilidade de seguro, integrando-se com APIs externas. O sistema realiza uma verificação com base no valor de um veículo e no estado de residência do usuário.

Funcionalidades principais:
Integração com a API FIPE: O sistema consulta o valor do veículo pelo código FIPE informado pelo usuário, verificando se o valor é igual ou superior a R$30.000 para ser aprovado.

javascript
Copiar código
let urlFipe = 'https://brasilapi.com.br/api/fipe/preco/v1/' + fipe;
$.get(urlFipe, function(data){
    data.forEach(veiculo => {
        let valor = parseFloat(veiculo['valor'].replace("R$", "").replace(".", "").replace(",", "."));
        if (valor >= 30000) { veiculoAprovado = true; }
    });
});
Verificação de Estado via API de CEP: O sistema também consulta a API de CEP, verificando se o estado é "RJ" (condição para aprovação).

javascript
Copiar código
let urlCep = 'https://brasilapi.com.br/api/cep/v2/' + cep;
$.get(urlCep, function(data){
    if (data['state'] === "RJ") { estadoAprovado = true; }
});
Feedback ao usuário: Caso ambas as condições sejam atendidas, o sistema exibe uma mensagem de elegibilidade ao seguro. Caso contrário, retorna uma mensagem de não aprovação.

javascript
Copiar código
if (veiculoAprovado && estadoAprovado) {
    $("#resultadoSeguro").html("<p class='mb-0'><strong>Parabéns! Você está elegível para o seguro.</strong></p>")
                         .removeClass("d-none alert-danger").addClass("alert-success");
} else {
    $("#resultadoSeguro").html("<p class='mb-0'><strong>Desculpe, você não atende aos critérios para o seguro.</strong></p>")
                         .removeClass("d-none alert-success").addClass("alert-danger");
}
Tecnologias Utilizadas
HTML5 e CSS3 para a estrutura e estilo da página
Bootstrap 4 para responsividade e design moderno
jQuery para manipulação dinâmica do DOM e integração com APIs externas
APIs para consulta de informações FIPE e CEP, simulando um ambiente real de validação de dados.
