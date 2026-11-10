# Java

* { box-sizing: border-box; }
body {
  font-family: Arial, sans-serif;
  background: #f4f1f6;
  margin: 0;
  padding: 30px;
}
.container {
  max-width: 500px;
  margin: 40px auto;
  padding: 30px;
  background: white;
  border-radius: 12px;
  box-shadow: 0 4px 12px rgba(0,0,0,.10);
}
h1 { color: #43054e; text-align: center; }
label { display: block; margin-top: 15px; }
input {
  width: 100%; padding: 12px; margin-top: 8px;
  border: 1px solid #ccc; border-radius: 6px;
}
button {
  width: 100%; margin-top: 20px; padding: 12px;
  background: #662c92; color: white;
  border: 0; border-radius: 6px; cursor: pointer;
}
button:hover { background: #43054e; }
#resultado, #resultadoMedia {
  margin-top: 20px; padding: 15px;
  background: #f3f4f6; border-radius: 6px;
}
#resultadoMedia.erro { background: #fdecea; color: #b3261e; }
#resultadoMedia.sucesso { background: #e8f5e9; color: #1b5e20; font-weight: bold; }

Aula01-JavaScript/
├── index.html
├── style.css
├── script.js
└── evidencias/
    ├── calculadora.png
    └── media-estudante.png
    /* ===== LABORATÓRIO 1 — Cadastro simples de usuário (ver no Console) ===== */
const nome = "Lucas Ferreira";
const email = "lucas@email.com";
let idade = 24;
let usuarioAtivo = true;

console.log("DADOS DO USUÁRIO");
console.log("Nome:", nome);
console.log("E-mail:", email);
console.log("Idade:", idade);
console.log("Usuário ativo:", usuarioAtivo);

// Tarefa 4: estimar a idade a partir do ano de nascimento (referência 2026)
const anoNascimento = 2002;
const idadeEstimada = 2026 - anoNascimento;
console.log("Ano de nascimento:", anoNascimento);
console.log("Idade estimada (pode variar conforme o aniversário):", idadeEstimada);

/* ===== LABORATÓRIO 2 — Calculadora de operações ===== */
const botao = document.getElementById("btnCalcular");

botao.addEventListener("click", function () {
  const campo1 = document.getElementById("numero1");
  const campo2 = document.getElementById("numero2");
  const resultado = document.getElementById("resultado");

  if (campo1.value === "" || campo2.value === "") {
    resultado.textContent = "Preencha os dois números.";
    return;
  }

  const numero1 = Number(campo1.value);
  const numero2 = Number(campo2.value);

  const soma = numero1 + numero2;
  const subtracao = numero1 - numero2;
  const multiplicacao = numero1 * numero2;
  const divisao = numero2 === 0
    ? "Não é possível dividir por zero."
    : numero1 / numero2;

  resultado.innerHTML = `
    <p>Soma: ${soma}</p>
    <p>Subtração: ${subtracao}</p>
    <p>Multiplicação: ${multiplicacao}</p>
    <p>Divisão: ${divisao}</p>
  `;
});

/* ===== LABORATÓRIO 3 — Calculadora de média ===== */
const botaoMedia = document.getElementById("calcular");

botaoMedia.addEventListener("click", function () {
  const campos = [
    document.getElementById("nota1"),
    document.getElementById("nota2"),
    document.getElementById("nota3")
  ];
  const saida = document.getElementById("resultadoMedia");

  saida.className = "";

  // Rejeita campos vazios
  if (campos.some(function (c) { return c.value === ""; })) {
    saida.textContent = "Erro: preencha as três notas.";
    saida.className = "erro";
    return;
  }

  const notas = campos.map(function (c) { return Number(c.value); });

  // Aceita somente notas entre 0 e 10
  if (notas.some(function (n) { return isNaN(n) || n < 0 || n > 10; })) {
    saida.textContent = "Erro: as notas devem estar entre 0 e 10.";
    saida.className = "erro";
    return;
  }

  const media = (notas[0] + notas[1] + notas[2]) / 3;
  saida.textContent = "Média: " + Number(media.toFixed(2));
  saida.className = "sucesso";
});
