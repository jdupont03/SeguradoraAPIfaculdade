**Insurance Eligibility Check Project**
This project is an interactive web application developed using HTML, CSS, JavaScript, and jQuery to check insurance eligibility by integrating with external APIs. The system validates eligibility based on a vehicle's value and the user's state of residence.

**Main Features**
1. Integration with the FIPE API
   
The system retrieves the vehicle’s value using the FIPE code provided by the user, verifying if the value is equal to or greater than R$30,000 to be eligible.

        let urlFipe = 'https://brasilapi.com.br/api/fipe/preco/v1/' + fipe;
        $.get(urlFipe, function(data){
            data.forEach(veiculo => {
                let valor = parseFloat(veiculo['valor'].replace("R$", "").replace(".", "").replace(",", "."));
                if (valor >= 30000) { veiculoAprovado = true; }
            });
        });

**2. State Verification via CEP API**

The system also queries the CEP API, checking if the user’s state is "RJ" (required for eligibility).

        let urlCep = 'https://brasilapi.com.br/api/cep/v2/' + cep;
        $.get(urlCep, function(data){
            if (data['state'] === "RJ") { estadoAprovado = true; }
        });

**3. User Feedback**

If both conditions are met, the system displays a message of insurance eligibility. Otherwise, a message indicating ineligibility is shown.

        if (veiculoAprovado && estadoAprovado) {
            $("#resultadoSeguro").html("<p class='mb-0'><strong>Congratulations! You are eligible for insurance.</strong></p>")
                                 .removeClass("d-none alert-danger").addClass("alert-success");
        } else {
            $("#resultadoSeguro").html("<p class='mb-0'><strong>Sorry, you do not meet the eligibility criteria for insurance.</strong></p>")
                                 .removeClass("d-none alert-success").addClass("alert-danger");
        }

**Technologies Used**

-HTML5 and CSS3 for page structure and styling

-Bootstrap 4 for responsiveness and modern design

-jQuery for dynamic DOM manipulation and API integration

-APIs to retrieve FIPE and CEP data, simulating a real-world data validation environment.
