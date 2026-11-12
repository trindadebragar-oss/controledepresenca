# controledepresenca<!DOCTYPE html>
<html lang="pt-br">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Sistema de Presença Escolar</title>


    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f2f5;
            text-align: center;
            padding: 40px;
        }

        h1 {
            color: #1d3557;
        }

        button {
            background-color: #2563eb;
            color: white;
            padding: 12px 20px;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            margin: 10px;
        }
    </style>
</head>


<body>

    <h1>Sistema de Presença Escolar</h1>

    <p>Bem-vindo ao sistema de controle de presença.</p>

    <button onclick="mostrarCadastro()">
        Cadastrar Aluno
    </button>
<button onclick="mostrarAlunos()">
    Alunos Cadastrados
</button>
<div id="listaAlunos" style="display: none;">

    <h2>Alunos Cadastrados</h2>

    <ul id="alunos"></ul>

</div>
    <button onclick="alert('Em desenvolvimento!')">
        Registrar Presença
    </button>

    <button onclick="alert('Em desenvolvimento!')">
        Consultar Presenças
    </button>

    <div id="cadastro" style="display: none; margin-top: 30px;">

        <h2>Cadastro de Aluno</h2>

        <form onsubmit="salvarAluno(event)">

            <p>Nome completo:</p>
            <input type="text" id="nome" required>

            <p>Matrícula:</p>
            <input type="text" id="matricula" required>

            
<p>Turma:</p>

<select id="turma" required>
    <option value="">Selecione a turma</option>
    <option value="1º Ano A">1º Ano A</option>
    <option value="1º Ano B">1º Ano B</option>
    <option value="2º Ano A">2º Ano A</option>
    <option value="2º Ano B">2º Ano B</option>
    <option value="3º Ano A">3º Ano A</option>
    <option value="3º Ano B">3º Ano B</option>
</select>


            <br><br>

            <button type="submit">Salvar Aluno</button>

        </form>

        <p id="mensagem"></p>

    </div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
<script>


        

function mostrarCadastro() {
    
}

function salvarAluno(event) {
    // código existente
}



function mostrarCadastro() {
    // código existente
}

function salvarAluno(event) {
    // código existente
}





        function mostrarCadastro() {
            document.getElementById("cadastro").style.display = "block";
        }

       
function salvarAluno(event) {
    event.preventDefault();

    let nome = document.getElementById("nome").value;
    let matricula = document.getElementById("matricula").value;
    let turma = document.getElementById("turma").value;

    let alunos = JSON.parse(localStorage.getItem("alunos")) || [];

    let existe = alunos.some(aluno => aluno.matricula === matricula);

    if (existe) {
        document.getElementById("mensagem").innerText =
            "Essa matrícula já está cadastrada!";
        return;
    }

    alunos.push({
        nome: nome,
        matricula: matricula,
        turma: turma
    });

    localStorage.setItem("alunos", JSON.stringify(alunos));

    document.getElementById("mensagem").innerText =
        "Aluno " + nome + " salvo com sucesso!";

    event.target.reset();
}



function mostrarAlunos() {
    let alunos = JSON.parse(localStorage.getItem("alunos")) || [];

    let lista = document.getElementById("listaAlunos");
    let conteudo = document.getElementById("alunos");

    lista.style.display = "block";
    conteudo.innerHTML = "";

    if (alunos.length === 0) {
        conteudo.innerHTML = "<li>Nenhum aluno cadastrado.</li>";
        return;
    }

    alunos.forEach(function(aluno) {
        let item = document.createElement("li");

        let informacoes = document.createElement("p");
        informacoes.textContent =
            "Nome: " + aluno.nome +
            " | Matrícula: " + aluno.matricula +
            " | Turma: " + aluno.turma;

        let botao = document.createElement("button");
        botao.textContent = "Gerar QR Code";

        let areaQR = document.createElement("div");

        botao.onclick = function() {
            areaQR.innerHTML = "";

            if (typeof QRCode === "undefined") {
                areaQR.textContent = "Biblioteca QR Code não carregada.";
                return;
            }

            new QRCode(areaQR, {
                text: "PRESENCA:" + aluno.matricula,
                width: 150,
                height: 150
            });
        };

        item.appendChild(informacoes);
        item.appendChild(botao);
        item.appendChild(areaQR);

        conteudo.appendChild(item);
    });
}


    </script>

</body>


</html>

