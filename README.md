
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Calculadora de Desconto - Camisetas</title>
  
</head>
<body>
  <main class="card" role="main">
    <h1>Calculadora de desconto — Camisetas</h1>
    <p class="subtitle">Preço unitário: <strong>R$ 35,00</strong>. Compras de <strong>3 ou mais</strong> ganham <strong>20% de desconto</strong> no total.</p>
    <form id="form" onsubmit="return false;" aria-label="Calculadora de desconto de camisetas">
      <label for="qty">Quantidade de camisetas</label>
      <input id="qty" name="qty" type="number" min="0" step="1" value="1" required aria-required="true" />
      <button id="calc">Calcular valor final</button>
    </form>
    <div id="output" class="result" aria-live="polite">
      <div class="small">Preencha a quantidade e pressione <strong>Calcular valor final</strong>.</div>
    </div>
   
  <script>
    // Configurações do problema
    const PRECO_UNIT = 35.0; // em reais
    const QTD_DESC_MIN = 3;  // quantidade mínima para desconto
    const TAXA_DESC = 0.20;  // 20% de desconto
    // Elementos
    const form = document.getElementById('form');
    const qtyInput = document.getElementById('qty');
    const output = document.getElementById('output');
    const btn = document.getElementById('calc');
    // Formatação para reais (pt-BR)
    function formatBRL(value) {
      return value.toLocaleString('pt-BR', { style: 'currency', currency: 'BRL' });
    }

    function calcular() {
      const qtd = Number(qtyInput.value);

      if (!Number.isFinite(qtd) || qtd < 0) {
        output.innerHTML = '<div class="small">Quantidade inválida. Insira 0 ou mais.</div>';
        return;
      }
      const totalSemDesc = qtd * PRECO_UNIT;

      if (qtd >= QTD_DESC_MIN) {
        const desconto = totalSemDesc * TAXA_DESC;
        const totalFinal = totalSemDesc - desconto;
        output.innerHTML = `
          <div><strong>Quantidade:</strong> ${qtd}</div>
          <div><strong>Valor sem desconto:</strong> ${formatBRL(totalSemDesc)}</div>
          <div><strong>Desconto (20%):</strong> ${formatBRL(desconto)}</div>
          <div style="margin-top:8px;font-size:16px"><strong>Valor final:</strong> ${formatBRL(totalFinal)}</div>
        `;
      } else {
        output.innerHTML = `
          <div><strong>Quantidade:</strong> ${qtd}</div>
          <div style="margin-top:8px;font-size:16px"><strong>Valor final:</strong> ${formatBRL(totalSemDesc)}</div>
          <div class="muted" style="margin-top:6px">Compre ${QTD_DESC_MIN} ou mais para receber 20% de desconto.</div>
        `;
      }
    }
    // Eventos
    btn.addEventListener('click', calcular);
    // Permite calcular também ao pressionar Enter no campo
    qtyInput.addEventListener('keydown', function(e){ if (e.key === 'Enter') { e.preventDefault(); calcular(); } });
    // Calcula valor inicial
    calcular();
  </script>
</body>
</html>
