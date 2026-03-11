<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ji Serviços Pro - GIF Edition</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>
    
    <style>
        :root { --primary: #004AAD; --bg: #F2F2F7; }
        * { box-sizing: border-box; margin: 0; padding: 0; font-family: sans-serif; }
        body { background: var(--bg); padding: 20px; display: flex; justify-content: center; }

        .app-container { width: 100%; max-width: 480px; background: white; border-radius: 30px; padding: 25px; box-shadow: 0 10px 30px rgba(0,0,0,0.1); text-align: center; }
        
        /* Espaço para o GIF de Logo */
        .logo-gif {
            width: 120px;
            height: 120px;
            margin: 0 auto 15px;
            background: #eee; /* Cor de fundo enquanto o gif não carrega */
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            overflow: hidden;
            border: 3px solid var(--primary);
        }
        .logo-gif img { width: 100%; height: 100%; object-fit: cover; }

        .form-group { margin-bottom: 15px; text-align: left; }
        .form-group label { display: block; font-size: 11px; font-weight: bold; color: #666; margin-bottom: 5px; text-transform: uppercase; }
        .form-group input, .form-group select, .form-group textarea {
            width: 100%; padding: 14px; border-radius: 12px; border: 1.5px solid #E5E5EA; font-size: 16px; outline: none;
        }

        /* Botões Estilizados */
        .btn { width: 100%; padding: 18px; border-radius: 18px; border: none; font-weight: bold; font-size: 16px; cursor: pointer; margin-top: 12px; display: flex; align-items: center; justify-content: center; gap: 10px; color: white; transition: 0.2s; }
        .btn-blue { background: var(--primary); box-shadow: 0 5px 15px rgba(0,74,173,0.3); }
        .btn-red { background: #FF3B30; display: none; box-shadow: 0 5px 15px rgba(255,59,48,0.3); }
        .btn-green { background: #25D366; display: none; text-decoration: none; box-shadow: 0 5px 15px rgba(37,211,102,0.3); }
        .btn-gray { background: #8E8E93; font-size: 13px; margin-top: 25px; }
        .btn:active { transform: scale(0.97); }

        /* PDF Oculto */
        #conteudo-pdf { width: 700px; background: white; position: absolute; left: -9999px; top: 0; }
        .pdf-wrapper { padding: 50px; min-height: 1050px; }
        .valor-box { background: var(--primary); color: white; padding: 30px; border-radius: 15px; text-align: right; margin-top: 40px; }
    </style>
</head>
<body>

<div class="app-container">
    <div class="logo-gif">
        <img src="https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExNHJid2p6bmZ6bmZ6bmZ6bmZ6bmZ6bmZ6bmZ6bmZ6bmZ6bmZ6bmZ6JmVwPXYxX2ludGVybmFsX2dpZl9ieV9pZCZjdD1n/3o7TKVUn7iM8FMEU24/giphy.gif" alt="Ji Serviços">
    </div>
    
    <header style="margin-bottom: 25px;">
        <h1 style="color: var(--primary); letter-spacing: -1px;">Ji Serviços</h1>
        <p style="color: #888; font-size: 12px;">Manaus - Elétrica e Refrigeração</p>
    </header>

    <div class="form-group">
        <label>Nome do Cliente</label>
        <input type="text" id="nome" placeholder="Nome Completo">
    </div>
    
    <div class="form-group">
        <label>WhatsApp</label>
        <input type="number" id="telefone" placeholder="92985821876">
    </div>

    <div class="form-group">
        <label>Diagnóstico Técnico</label>
        <textarea id="diag" rows="3" placeholder="O que foi encontrado?"></textarea>
    </div>

    <div class="form-group">
        <label>Valor Total (R$)</label>
        <input type="number" id="valor" placeholder="0.00">
    </div>

    <button class="btn btn-blue" onclick="gerar()">
        <i class="fa-solid fa-bolt"></i> GERAR ORÇAMENTO
    </button>

    <div id="acoes" style="display: none;">
        <button id="btnPdf" class="btn btn-red" onclick="baixarPDF()">
            <i class="fa-solid fa-file-pdf"></i> BAIXAR PDF
        </button>
        <a id="linkWpp" href="#" target="_blank" class="btn btn-green">
            <i class="fa-brands fa-whatsapp"></i> ENVIAR WHATSAPP
        </a>
        <button class="btn btn-gray" onclick="location.reload()">
            <i class="fa-solid fa-rotate"></i> NOVO ATENDIMENTO
        </button>
    </div>
</div>

<div id="conteudo-pdf">
    <div class="pdf-wrapper">
        <div style="border-bottom: 5px solid #004AAD; padding-bottom: 20px; margin-bottom: 30px;">
            <h1 style="font-size: 38px; color: #004AAD; margin: 0;">JI SERVIÇOS</h1>
            <p style="font-size: 16px; margin-top: 5px;">Manaus - AM | (92) 98582-1876</p>
        </div>

        <h2 style="background: #F2F2F7; padding: 15px; text-align: center; border-radius: 10px;">RELATÓRIO DE SERVIÇO</h2>

        <div style="margin: 40px 0; font-size: 18px;">
            <p><strong>CLIENTE:</strong> <span id="pdf-nome"></span></p>
            <p style="margin-top: 10px;"><strong>DATA:</strong> <span id="pdf-data"></span></p>
        </div>

        <div style="border: 2px solid #EEE; padding: 25px; border-radius: 15px; margin-bottom: 30px;">
            <h3 style="color: #004AAD; margin-bottom: 15px;">DIAGNÓSTICO TÉCNICO:</h3>
            <p id="pdf-diag" style="font-size: 17px; line-height: 1.6; color: #333;"></p>
        </div>

        <div class="valor-box">
            <p style="font-size: 16px; opacity: 0.9;">VALOR DO INVESTIMENTO:</p>
            <h1 id="pdf-total" style="font-size: 48px; margin-top: 5px;"></h1>
        </div>

        <div style="margin-top: auto; text-align: center; padding-top: 40px; border-top: 1px solid #EEE;">
            <p style="font-size: 14px; color: #666;">Garantia de 90 dias nos serviços prestados.</p>
            <p style="font-size: 14px; font-weight: bold; color: #004AAD; margin-top: 5px;">Ji Serviços - Qualidade e Confiança</p>
        </div>
    </div>
</div>

<script>
    function gerar() {
        const nome = document.getElementById('nome').value;
        const valor = parseFloat(document.getElementById('valor').value) || 0;
        const diag = document.getElementById('diag').value;
        const tel = document.getElementById('telefone').value;

        if(!nome || valor === 0) return alert("Por favor, preencha Nome e Valor!");

        document.getElementById('pdf-nome').innerText = nome.toUpperCase();
        document.getElementById('pdf-diag').innerText = diag || "Inspeção técnica concluída.";
        document.getElementById('pdf-total').innerText = "R$ " + valor.toLocaleString('pt-BR', {minimumFractionDigits: 2});
        document.getElementById('pdf-data').innerText = new Date().toLocaleDateString('pt-BR');

        document.getElementById('acoes').style.display = 'block';
        document.getElementById('btnPdf').style.display = 'flex';
        document.getElementById('linkWpp').style.display = 'flex';
        
        const msg = `*📋 JI SERVIÇOS - ORÇAMENTO*%0A*Cliente:* ${nome}%0A*Valor:* R$ ${valor.toFixed(2)}%0A%0A_O PDF oficial segue em anexo._`;
        document.getElementById('linkWpp').href = `https://wa.me/55${tel}?text=${msg}`;
        
        window.scrollTo({ top: document.body.scrollHeight, behavior: 'smooth' });
    }

    function baixarPDF() {
        const element = document.getElementById('conteudo-pdf');
        const opt = {
            margin: 0,
            filename: `Orcamento_Ji_${document.getElementById('nome').value}.pdf`,
            image: { type: 'jpeg', quality: 0.98 },
            html2canvas: { scale: 2, useCORS: true, windowWidth: 700 },
            jsPDF: { unit: 'mm', format: 'a4', orientation: 'portrait' }
        };
        html2pdf().set(opt).from(element).save();
    }
</script>

</body>
</html>

App-J-I-servi-o-
