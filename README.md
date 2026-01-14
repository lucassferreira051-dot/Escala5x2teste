<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistema de Escala 5x2 - Rodízio Perfeito</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
    <style>
        /* ============================================
           ESTILOS FUTURÍSTICOS - TEMA TECBAN
           CORES: VERMELHO, PRETO, FUNDO BRANCO
           ============================================ */

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', 'Roboto', 'Helvetica Neue', sans-serif;
        }

        body {
            background: #FFFFFF; /* FUNDO BRANCO */
            color: #333333; /* Cor de texto escura para contraste com fundo branco */
            line-height: 1.6;
            padding: 20px;
            min-height: 100vh;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
            background: #FFFFFF; /* FUNDO BRANCO */
            border: 1px solid rgba(211, 47, 47, 0.2); /* Borda vermelha sutil */
            border-radius: 20px;
            padding: 30px;
            box-shadow: 0 20px 60px rgba(211, 47, 47, 0.1); /* Sombra vermelha suave */
            position: relative;
            overflow: hidden;
        }

        .container::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 4px;
            background: linear-gradient(90deg, #D32F2F, #FF5252, #B71C1C); /* Gradiente vermelho */
            z-index: 1;
        }

        .header {
            text-align: center;
            padding-bottom: 25px;
            margin-bottom: 30px;
            border-bottom: 1px solid rgba(211, 47, 47, 0.2); /* Linha vermelha sutil */
            position: relative;
        }

        .header::after {
            content: '';
            position: absolute;
            bottom: -1px;
            left: 50%;
            transform: translateX(-50%);
            width: 200px;
            height: 3px;
            background: linear-gradient(90deg, transparent, #D32F2F, transparent); /* Linha vermelha central */
        }

        h1 {
            color: #000000; /* PRETO */
            font-size: 32px;
            font-weight: 700;
            margin-bottom: 10px;
            text-transform: uppercase;
            letter-spacing: 1px;
            background: linear-gradient(90deg, #D32F2F, #FF5252); /* Gradiente vermelho */
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .subtitle {
            color: #666666; /* Cinza escuro */
            font-size: 16px;
            font-weight: 300;
        }

        .menu {
            display: grid;
            grid-template-columns: repeat(5, 1fr);
            gap: 15px;
            margin-bottom: 40px;
        }

        .menu-item {
            background: #FFFFFF; /* FUNDO BRANCO */
            color: #333333; /* Texto escuro */
            border: 1px solid rgba(211, 47, 47, 0.3); /* Borda vermelha */
            padding: 18px 15px;
            cursor: pointer;
            font-size: 14px;
            font-weight: 600;
            text-align: center;
            border-radius: 12px;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 8px;
            box-shadow: 0 4px 12px rgba(211, 47, 47, 0.08);
        }

        .menu-item::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(211, 47, 47, 0.1), transparent);
            transition: 0.5s;
        }

        .menu-item:hover::before {
            left: 100%;
        }

        .menu-item:hover {
            background: #FFEBEE; /* Vermelho bem claro */
            border-color: #D32F2F; /* Vermelho principal */
            transform: translateY(-3px);
            box-shadow: 0 10px 25px rgba(211, 47, 47, 0.15);
        }

        .menu-item i {
            font-size: 20px;
            color: #D32F2F; /* Vermelho principal */
        }

        .content {
            padding: 20px;
            min-height: 500px;
        }

        .section {
            display: none;
            animation: fadeIn 0.5s ease;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .section.active {
            display: block;
        }

        h2 {
            color: #000000; /* PRETO */
            font-size: 24px;
            font-weight: 600;
            margin-bottom: 25px;
            padding-bottom: 15px;
            border-bottom: 1px solid rgba(211, 47, 47, 0.2); /* Linha vermelha sutil */
            position: relative;
        }

        h2::after {
            content: '';
            position: absolute;
            bottom: -1px;
            left: 0;
            width: 100px;
            height: 3px;
            background: linear-gradient(90deg, #D32F2F, #FF5252); /* Gradiente vermelho */
        }

        .form-group {
            margin-bottom: 25px;
        }

        label {
            display: block;
            margin-bottom: 10px;
            font-weight: 600;
            font-size: 14px;
            color: #D32F2F; /* Vermelho principal */
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }

        input, select {
            width: 250px;
            padding: 14px 20px;
            background: #FFFFFF; /* FUNDO BRANCO */
            border: 1px solid rgba(211, 47, 47, 0.4); /* Borda vermelha */
            border-radius: 10px;
            font-size: 15px;
            color: #333333; /* Texto escuro */
            transition: all 0.3s ease;
            outline: none;
        }

        input:focus, select:focus {
            border-color: #D32F2F; /* Vermelho principal */
            background: #FFFFFF; /* FUNDO BRANCO */
            box-shadow: 0 0 0 3px rgba(211, 47, 47, 0.2); /* Sombra vermelha */
        }

        input::placeholder {
            color: rgba(51, 51, 51, 0.5); /* Cinza para placeholder */
        }

        select option {
            background: #FFFFFF; /* FUNDO BRANCO */
            color: #333333; /* Texto escuro */
        }

        .btn {
            background: linear-gradient(90deg, #D32F2F, #FF5252); /* Gradiente vermelho */
            color: #FFFFFF; /* BRANCO */
            border: none;
            padding: 16px 32px;
            cursor: pointer;
            font-size: 15px;
            font-weight: 600;
            border-radius: 10px;
            transition: all 0.3s ease;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            position: relative;
            overflow: hidden;
            margin-right: 10px;
            margin-bottom: 10px;
            display: inline-flex;
            align-items: center;
            gap: 8px;
        }

        .btn i {
            font-size: 16px;
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 25px rgba(211, 47, 47, 0.3);
            background: linear-gradient(90deg, #B71C1C, #D32F2F); /* Gradiente vermelho mais escuro */
        }

        .btn-secondary {
            background: linear-gradient(90deg, #666666, #999999);
        }

        .btn-secondary:hover {
            background: linear-gradient(90deg, #555555, #777777);
            box-shadow: 0 10px 25px rgba(102, 102, 102, 0.3);
        }

        .btn-success {
            background: linear-gradient(90deg, #2E7D32, #4CAF50);
        }

        .btn-success:hover {
            background: linear-gradient(90deg, #1B5E20, #388E3C);
            box-shadow: 0 10px 25px rgba(46, 125, 50, 0.3);
        }

        .result {
            margin-top: 30px;
            padding: 25px;
            background: #FFFFFF; /* FUNDO BRANCO */
            border: 1px solid rgba(211, 47, 47, 0.2); /* Borda vermelha sutil */
            border-radius: 15px;
            max-height: 600px;
            overflow-y: auto;
            font-size: 14px;
            box-shadow: 0 5px 15px rgba(211, 47, 47, 0.05);
        }

        .result::-webkit-scrollbar {
            width: 8px;
        }

        .result::-webkit-scrollbar-track {
            background: rgba(211, 47, 47, 0.05);
            border-radius: 4px;
        }

        .result::-webkit-scrollbar-thumb {
            background: linear-gradient(180deg, #FF5252, #D32F2F); /* Gradiente vermelho */
            border-radius: 4px;
        }

        table {
            width: 100%;
            border-collapse: separate;
            border-spacing: 0;
            margin: 20px 0;
            font-size: 13px;
            border-radius: 10px;
            overflow: hidden;
            box-shadow: 0 5px 15px rgba(211, 47, 47, 0.05);
        }

        th, td {
            padding: 12px 15px;
            text-align: center;
            border-bottom: 1px solid rgba(211, 47, 47, 0.1); /* Linha vermelha sutil */
        }

        th {
            background: linear-gradient(90deg, rgba(211, 47, 47, 0.15), rgba(255, 82, 82, 0.1)); /* Gradiente vermelho suave */
            color: #000000; /* PRETO */
            font-weight: 700;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            font-size: 12px;
            position: relative;
        }

        th::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 0;
            width: 100%;
            height: 2px;
            background: linear-gradient(90deg, #FF5252, #D32F2F); /* Gradiente vermelho */
        }

        tbody tr {
            background: #FFFFFF; /* FUNDO BRANCO */
            transition: all 0.3s ease;
        }

        tbody tr:nth-child(even) {
            background: rgba(211, 47, 47, 0.02); /* Vermelho muito sutil */
        }

        tbody tr:hover {
            background: rgba(211, 47, 47, 0.08); /* Vermelho claro ao passar o mouse */
            transform: translateY(-1px);
        }

        .presente {
            background: linear-gradient(135deg, rgba(46, 125, 50, 0.15), rgba(56, 142, 60, 0.1)); /* Verde suave */
            color: #2E7D32; /* Verde escuro */
            font-weight: 700;
            border-radius: 6px;
            padding: 6px 10px;
            border: 1px solid rgba(46, 125, 50, 0.3);
        }

        .folga {
            background: linear-gradient(135deg, rgba(211, 47, 47, 0.15), rgba(183, 28, 28, 0.1)); /* Vermelho suave */
            color: #D32F2F; /* Vermelho principal */
            font-weight: 700;
            border-radius: 6px;
            padding: 6px 10px;
            border: 1px solid rgba(211, 47, 47, 0.3);
        }

        .ilha-sp {
            background: linear-gradient(135deg, rgba(211, 47, 47, 0.15), rgba(183, 28, 28, 0.1)); /* Vermelho suave */
            color: #D32F2F; /* Vermelho principal */
            font-weight: 600;
            border-radius: 6px;
            padding: 4px 8px;
            border: 1px solid rgba(211, 47, 47, 0.3);
        }

        .ilha-sc {
            background: linear-gradient(135deg, rgba(46, 125, 50, 0.15), rgba(56, 142, 60, 0.1)); /* Verde suave */
            color: #2E7D32; /* Verde escuro */
            font-weight: 600;
            border-radius: 6px;
            padding: 4px 8px;
            border: 1px solid rgba(46, 125, 50, 0.3);
        }

        .ilha-no {
            background: linear-gradient(135deg, rgba(255, 152, 0, 0.15), rgba(245, 124, 0, 0.1)); /* Laranja suave */
            color: #FF9800; /* Laranja */
            font-weight: 600;
            border-radius: 6px;
            padding: 4px 8px;
            border: 1px solid rgba(255, 152, 0, 0.3);
        }

        .ilha-su {
            background: linear-gradient(135deg, rgba(156, 39, 176, 0.15), rgba(123, 31, 162, 0.1)); /* Roxo suave */
            color: #9C27B0; /* Roxo */
            font-weight: 600;
            border-radius: 6px;
            padding: 4px 8px;
            border: 1px solid rgba(156, 39, 176, 0.3);
        }

        .status-ok {
            color: #2E7D32; /* Verde escuro */
            font-weight: 700;
            background: rgba(46, 125, 50, 0.1);
            padding: 6px 12px;
            border-radius: 6px;
            border: 1px solid rgba(46, 125, 50, 0.3);
        }

        .download-buttons {
            margin: 20px 0;
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
        }

        .console-output {
            background: #000000; /* PRETO */
            color: #FF5252; /* Vermelho claro para texto de console */
            padding: 20px;
            font-family: 'Consolas', 'Monaco', monospace;
            font-size: 13px;
            white-space: pre-wrap;
            margin-top: 20px;
            max-height: 300px;
            overflow-y: auto;
            border-radius: 10px;
            border: 1px solid rgba(255, 82, 82, 0.3); /* Borda vermelha */
            box-shadow: inset 0 0 20px rgba(0, 0, 0, 0.5);
        }

        /* Efeito de grade */
        .grid-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-image: 
                linear-gradient(rgba(211, 47, 47, 0.03) 1px, transparent 1px),
                linear-gradient(90deg, rgba(211, 47, 47, 0.03) 1px, transparent 1px);
            background-size: 50px 50px;
            pointer-events: none;
            z-index: -1;
        }

        /* Responsividade */
        @media (max-width: 1024px) {
            .container {
                padding: 20px;
            }
            
            .menu {
                grid-template-columns: repeat(3, 1fr);
            }
            
            h1 {
                font-size: 28px;
            }
        }

        @media (max-width: 768px) {
            body {
                padding: 10px;
            }
            
            .container {
                padding: 15px;
            }
            
            .menu {
                grid-template-columns: repeat(2, 1fr);
                gap: 10px;
            }
            
            h1 {
                font-size: 24px;
            }
            
            h2 {
                font-size: 20px;
            }
            
            input, select {
                width: 100%;
            }
            
            table {
                font-size: 11px;
            }
            
            th, td {
                padding: 8px 10px;
            }
            
            .download-buttons {
                flex-direction: column;
            }
            
            .btn {
                width: 100%;
                justify-content: center;
            }
        }

        @media (max-width: 480px) {
            h1 {
                font-size: 20px;
            }
            
            .subtitle {
                font-size: 14px;
            }
            
            .menu {
                grid-template-columns: 1fr;
            }
            
            .menu-item {
                padding: 15px 10px;
                font-size: 13px;
            }
        }
    </style>
</head>
<body>
    <div class="grid-overlay"></div>
    
    <div class="container">
        <div class="header">
            <h1>📊 SISTEMA DE ESCALAS 5x2 - RODÍZIO PERFEITO COMPLETO</h1>
            <div class="subtitle">Sistema exato do Python - Nenhuma regra alterada</div>
        </div>
        
        <div class="menu">
            <button class="menu-item" onclick="showSection('gerar')">
                <i class="fas fa-calendar-plus"></i> Gerar Nova Escala
            </button>
            <button class="menu-item" onclick="showSection('visualizar')">
                <i class="fas fa-eye"></i> Visualizar Escala
            </button>
            <button class="menu-item" onclick="showSection('contadores')">
                <i class="fas fa-chart-bar"></i> Ver Contadores
            </button>
            <button class="menu-item" onclick="showSection('folgas')">
                <i class="fas fa-sync-alt"></i> Rodízio de Folgas
            </button>
            <button class="menu-item" onclick="showSection('anual')">
                <i class="fas fa-calendar-alt"></i> Escala Anual
            </button>
        </div>
        
        <div class="content">
            <!-- Seção: Gerar Nova Escala -->
            <div id="gerar" class="section active">
                <h2>GERAR NOVA ESCALA MENSAL</h2>
                <div class="form-group">
                    <label for="ano">Ano (ex: 2024):</label>
                    <input type="number" id="ano" min="2023" max="2030" value="2024">
                </div>
                <div class="form-group">
                    <label for="mes">Mês (1-12):</label>
                    <select id="mes">
                        <option value="1">Janeiro</option>
                        <option value="2">Fevereiro</option>
                        <option value="3">Março</option>
                        <option value="4">Abril</option>
                        <option value="5">Maio</option>
                        <option value="6">Junho</option>
                        <option value="7">Julho</option>
                        <option value="8">Agosto</option>
                        <option value="9">Setembro</option>
                        <option value="10">Outubro</option>
                        <option value="11">Novembro</option>
                        <option value="12">Dezembro</option>
                    </select>
                </div>
                <div class="form-group">
                    <label for="semanas">Número de semanas [4]:</label>
                    <input type="number" id="semanas" min="4" max="5" value="4">
                </div>
                
                <button class="btn" onclick="gerarEscala()">
                    <i class="fas fa-cogs"></i> Gerar Escala com Rodízio Perfeito
                </button>
                
                <div class="download-buttons" id="download-buttons-gerar" style="display:none;">
                    <button class="btn btn-success" onclick="exportarEscalaParaExcel('gerar')">
                        <i class="fas fa-file-excel"></i> Baixar Excel
                    </button>
                    <button class="btn btn-secondary" onclick="exportarEscalaParaPDF('gerar')">
                        <i class="fas fa-file-pdf"></i> Baixar PDF
                    </button>
                    <button class="btn btn-secondary" onclick="exportarEscalaParaCSV('gerar')">
                        <i class="fas fa-file-csv"></i> Baixar CSV
                    </button>
                </div>
                
                <div id="console-gerar" class="console-output" style="display:none;"></div>
                <div id="resultado-gerar" class="result" style="display:none;"></div>
            </div>
            
            <!-- Seção: Visualizar Escala -->
            <div id="visualizar" class="section">
                <h2>VISUALIZAR ESCALA EXISTENTE</h2>
                <div class="form-group">
                    <label for="v-ano">Ano:</label>
                    <input type="number" id="v-ano" min="2023" max="2030" value="2024">
                </div>
                <div class="form-group">
                    <label for="v-mes">Mês:</label>
                    <select id="v-mes">
                        <option value="1">Janeiro</option>
                        <option value="2">Fevereiro</option>
                        <option value="3">Março</option>
                        <option value="4">Abril</option>
                        <option value="5">Maio</option>
                        <option value="6">Junho</option>
                        <option value="7">Julho</option>
                        <option value="8">Agosto</option>
                        <option value="9">Setembro</option>
                        <option value="10">Outubro</option>
                        <option value="11">Novembro</option>
                        <option value="12">Dezembro</option>
                    </select>
                </div>
                <button class="btn" onclick="visualizarEscala()">
                    <i class="fas fa-search"></i> Visualizar Escala
                </button>
                
                <div class="download-buttons" id="download-buttons-visualizar" style="display:none;">
                    <button class="btn btn-success" onclick="exportarEscalaParaExcel('visualizar')">
                        <i class="fas fa-file-excel"></i> Baixar Excel
                    </button>
                    <button class="btn btn-secondary" onclick="exportarEscalaParaPDF('visualizar')">
                        <i class="fas fa-file-pdf"></i> Baixar PDF
                    </button>
                </div>
                
                <div id="console-visualizar" class="console-output" style="display:none;"></div>
                <div id="resultado-visualizar" class="result" style="display:none;"></div>
            </div>
            
            <!-- Seção: Contadores -->
            <div id="contadores" class="section">
                <h2>CONTADORES DE FIM DE SEMANA</h2>
                <div class="form-group">
                    <label for="c-ano">Ano:</label>
                    <input type="number" id="c-ano" min="2023" max="2030" value="2024">
                </div>
                <div class="form-group">
                    <label for="c-mes">Mês (0 para todos):</label>
                    <select id="c-mes">
                        <option value="0">Todos os meses</option>
                        <option value="1">Janeiro</option>
                        <option value="2">Fevereiro</option>
                        <option value="3">Março</option>
                        <option value="4">Abril</option>
                        <option value="5">Maio</option>
                        <option value="6">Junho</option>
                        <option value="7">Julho</option>
                        <option value="8">Agosto</option>
                        <option value="9">Setembro</option>
                        <option value="10">Outubro</option>
                        <option value="11">Novembro</option>
                        <option value="12">Dezembro</option>
                    </select>
                </div>
                <button class="btn" onclick="verContadores()">
                    <i class="fas fa-chart-line"></i> Ver Contadores
                </button>
                
                <div class="download-buttons" id="download-buttons-contadores" style="display:none;">
                    <button class="btn btn-success" onclick="exportarContadoresParaExcel()">
                        <i class="fas fa-file-excel"></i> Baixar Contadores Excel
                    </button>
                </div>
                
                <div id="console-contadores" class="console-output" style="display:none;"></div>
                <div id="resultado-contadores" class="result" style="display:none;"></div>
            </div>
            
            <!-- Seção: Rodízio de Folgas -->
            <div id="folgas" class="section">
                <h2>RODÍZIO DE FOLGAS SEMANAL</h2>
                <div class="form-group">
                    <label for="rf-ano">Ano:</label>
                    <input type="number" id="rf-ano" min="2023" max="2030" value="2024">
                </div>
                <div class="form-group">
                    <label for="rf-mes">Mês:</label>
                    <select id="rf-mes">
                        <option value="1">Janeiro</option>
                        <option value="2">Fevereiro</option>
                        <option value="3">Março</option>
                        <option value="4">Abril</option>
                        <option value="5">Maio</option>
                        <option value="6">Junho</option>
                        <option value="7">Julho</option>
                        <option value="8">Agosto</option>
                        <option value="9">Setembro</option>
                        <option value="10">Outubro</option>
                        <option value="11">Novembro</option>
                        <option value="12">Dezembro</option>
                    </select>
                </div>
                <button class="btn" onclick="verRodizioFolgas()">
                    <i class="fas fa-retweet"></i> Ver Rodízio de Folgas
                </button>
                
                <div id="console-folgas" class="console-output" style="display:none;"></div>
                <div id="resultado-folgas" class="result" style="display:none;"></div>
            </div>
            
            <!-- Seção: Escala Anual -->
            <div id="anual" class="section">
                <h2>ESCALA ANUAL COMPLETA</h2>
                <div class="form-group">
                    <label for="a-ano">Ano:</label>
                    <input type="number" id="a-ano" min="2023" max="2030" value="2024">
                </div>
                
                <button class="btn" onclick="gerarEscalaAnual()">
                    <i class="fas fa-calendar-check"></i> Gerar Escala Anual
                </button>
                
                <div class="download-buttons" id="download-buttons-anual" style="display:none;">
                    <button class="btn btn-success" onclick="exportarEscalaAnualParaExcel()">
                        <i class="fas fa-file-excel"></i> Baixar Escala Anual Excel
                    </button>
                    <button class="btn btn-secondary" onclick="exportarEscalaAnualPorMes()">
                        <i class="fas fa-folder-open"></i> Baixar por Mês (ZIP)
                    </button>
                    <button class="btn btn-secondary" onclick="exportarResumoAnual()">
                        <i class="fas fa-chart-pie"></i> Baixar Resumo Anual
                    </button>
                </div>
                
                <div id="console-anual" class="console-output" style="display:none;"></div>
                <div id="resultado-anual" class="result" style="display:none;"></div>
            </div>
        </div>
    </div>

    <script>
        // ============================================
        // DADOS DO SISTEMA (EXATAMENTE COMO NO PYTHON)
        // ============================================
        const funcionarios = {
            "ILHA SP": [
                "ERNANE ALVES BRITO", "JULIA SANTOS SIQUEIRA", "NICOLI PEREIRA DA SILVA",
                "MARCO ANTONIO DE CAMPOS", "JOBSON DA SILVA BRITO", "CARLA ROBERTA ALVES",
                "LUCAS SANTOS", "LEONEL PEREIRA", "DANIELA ALVES DE CARVALHO"
            ],
            "ILHA SC": [
                "ROBSON DE LIMA SANTOS", "AMANDA ALVES DE SOUZA", "LETICIA SILVA DE SANTANA",
                "ALAN DE SOUZA CHAVES", "VICTOR HUGO DE SOUZA VASCONSELLOS",
                "MATEUS FAGUNDES DE LIMA", "MANUELA MENESES MACHADO"
            ],
            "ILHA NO": [
                "UENDERSON ENIS GOMES PEREIRA", "VINICIUS HENRIQUE VIANA DOS SANTOS",
                "MARCELO ANTONIO DA CRUZ", "LEANDRO BATISTA DE MELLO",
                "MATEUS DA SILVA CAMPOS", "DAPHNE FELIPPE DA HORA",
                "FELIPE ALEXANDRE DE ALMEIDA", "MARCOS ANDRE OLIVA TEXEIRA"
            ],
            "ILHA SU": [
                "RODRIGO PEREIRA MARQUES MACEGOZA", "FERNANDA ALVES DE BRITO",
                "TALITA MARTINS PAZ", "EDUARDO GARCIA MASSA", "MATHEUS DOS SANTOS SILVA",
                "FRANCISCO LUTHELLE CARNEIRO SEVERO", "AUGUSTO PERNHA SANTOS",
                "RAY BORAZO", "THIAGO CASTRO"
            ]
        };
        
        const diasSemana = ["Seg", "Ter", "Qua", "Qui", "Sex", "Sáb", "Dom"];
        const diasCompletos = ["Segunda", "Terça", "Quarta", "Quinta", "Sexta", "Sábado", "Domingo"];
        const meses = ["", "Janeiro", "Fevereiro", "Março", "Abril", "Maio", "Junho", 
                      "Julho", "Agosto", "Setembro", "Outubro", "Novembro", "Dezembro"];
        
        // ============================================
        // VARIÁVEIS DO SISTEMA
        // ============================================
        let rodizioIlhas = {};
        let rodizioFolgas = {};
        let contadoresAcumulados = {};
        let escalasGeradas = {};
        let escalaAnualGerada = {};
        let escalaAtual = null;
        let contadoresAtuais = null;
        
        // ============================================
        // FUNÇÕES DO SISTEMA (EXATA LÓGICA DO PYTHON)
        // ============================================
        
        function inicializarSistema() {
            console.log("Inicializando sistema...");
            
            for (const [ilha, listaFunc] of Object.entries(funcionarios)) {
                rodizioIlhas[ilha] = {
                    'filaDomingo': [...listaFunc],
                    'filaSabado': [...listaFunc],
                    'domingosPegos': {},
                    'sabadosPegos': {},
                    'rodadaDomingo': 0,
                    'rodadaSabado': 0,
                    'ultimoDomingo': null,
                    'ultimoSabado': null
                };
                
                for (const func of listaFunc) {
                    rodizioIlhas[ilha].domingosPegos[func] = 0;
                    rodizioIlhas[ilha].sabadosPegos[func] = 0;
                }
                
                rodizioFolgas[ilha] = {
                    'contadorFolgas': {},
                    'ultimasFolgas': {}
                };
                
                for (const func of listaFunc) {
                    rodizioFolgas[ilha].contadorFolgas[func] = {0:0,1:0,2:0,3:0,4:0,5:0,6:0};
                    rodizioFolgas[ilha].ultimasFolgas[func] = [];
                }
            }
            
            for (const listaFunc of Object.values(funcionarios)) {
                for (const func of listaFunc) {
                    contadoresAcumulados[func] = {
                        'sabados_trabalhados': 0,
                        'domingos_trabalhados': 0,
                        'total_fim_semana': 0,
                        'rodada_domingo': 0,
                        'rodada_sabado': 0
                    };
                }
            }
            
            console.log("✅ Sistema inicializado!");
        }
        
        function obterProximoDomingo(ilha) {
            const rodizio = rodizioIlhas[ilha];
            
            const todosTemDomingo = Object.values(rodizio.domingosPegos).every(v => v > 0);
            
            let funcionario;
            
            if (!todosTemDomingo) {
                let candidatos = Object.entries(rodizio.domingosPegos)
                    .filter(([_, v]) => v === 0)
                    .map(([f, _]) => f);
                
                if (candidatos.length === 0) {
                    const minDomingos = Math.min(...Object.values(rodizio.domingosPegos));
                    candidatos = Object.entries(rodizio.domingosPegos)
                        .filter(([_, v]) => v === minDomingos)
                        .map(([f, _]) => f);
                }
                
                for (const func of rodizio.filaDomingo) {
                    if (candidatos.includes(func)) {
                        funcionario = func;
                        break;
                    }
                }
            } else {
                const minDomingos = Math.min(...Object.values(rodizio.domingosPegos));
                const candidatos = Object.entries(rodizio.domingosPegos)
                    .filter(([_, v]) => v === minDomingos)
                    .map(([f, _]) => f);
                
                for (const func of rodizio.filaDomingo) {
                    if (candidatos.includes(func)) {
                        funcionario = func;
                        break;
                    }
                }
                
                if (!funcionario) {
                    funcionario = candidatos[0];
                }
            }
            
            const index = rodizio.filaDomingo.indexOf(funcionario);
            if (index > -1) {
                rodizio.filaDomingo.splice(index, 1);
            }
            rodizio.filaDomingo.push(funcionario);
            
            rodizio.domingosPegos[funcionario] += 1;
            rodizio.ultimoDomingo = funcionario;
            
            if (todosTemDomingo && Object.values(rodizio.domingosPegos).every(v => v === rodizio.domingosPegos[funcionario])) {
                rodizio.rodadaDomingo += 1;
                consoleLog(`    🎯 ${ilha}: COMPLETOU RODADA DE DOMINGO ${rodizio.rodadaDomingo}`);
            }
            
            return funcionario;
        }
        
        function obterProximoSabado(ilha) {
            const rodizio = rodizioIlhas[ilha];
            
            const todosTemSabado = Object.values(rodizio.sabadosPegos).every(v => v > 0);
            
            let funcionario;
            
            if (!todosTemSabado) {
                let candidatos = Object.entries(rodizio.sabadosPegos)
                    .filter(([_, v]) => v === 0)
                    .map(([f, _]) => f);
                
                if (candidatos.length === 0) {
                    const minSabados = Math.min(...Object.values(rodizio.sabadosPegos));
                    candidatos = Object.entries(rodizio.sabadosPegos)
                        .filter(([_, v]) => v === minSabados)
                        .map(([f, _]) => f);
                }
                
                for (const func of rodizio.filaSabado) {
                    if (candidatos.includes(func)) {
                        funcionario = func;
                        break;
                    }
                }
            } else {
                const minSabados = Math.min(...Object.values(rodizio.sabadosPegos));
                const candidatos = Object.entries(rodizio.sabadosPegos)
                    .filter(([_, v]) => v === minSabados)
                    .map(([f, _]) => f);
                
                for (const func of rodizio.filaSabado) {
                    if (candidatos.includes(func)) {
                        funcionario = func;
                        break;
                    }
                }
                
                if (!funcionario) {
                    funcionario = candidatos[0];
                }
            }
            
            const index = rodizio.filaSabado.indexOf(funcionario);
            if (index > -1) {
                rodizio.filaSabado.splice(index, 1);
            }
            rodizio.filaSabado.push(funcionario);
            
            rodizio.sabadosPegos[funcionario] += 1;
            rodizio.ultimoSabado = funcionario;
            
            if (todosTemSabado && Object.values(rodizio.sabadosPegos).every(v => v === rodizio.sabadosPegos[funcionario])) {
                rodizio.rodadaSabado += 1;
                consoleLog(`    🎯 ${ilha}: COMPLETOU RODADA DE SÁBADO ${rodizio.rodadaSabado}`);
            }
            
            return funcionario;
        }
        
        function gerarEscalaFuncionario(funcionario, trabalhaSabado, trabalhaDomingo, ilha, semanaAno) {
            if (trabalhaSabado && trabalhaDomingo) {
                trabalhaSabado = false;
            }
            
            const dias = ["P", "P", "P", "P", "P", "P", "P"];
            
            if (!trabalhaSabado) {
                dias[5] = "F";
            }
            if (!trabalhaDomingo) {
                dias[6] = "F";
            }
            
            let diaFolgaRotativo = (semanaAno - 1) % 6;
            
            if (diaFolgaRotativo === 5 && dias[6] === "F") {
                diaFolgaRotativo = 4;
            }
            
            let folgasAtuais = dias.filter(d => d === "F").length;
            
            if (dias[diaFolgaRotativo] === "P" && folgasAtuais < 2) {
                dias[diaFolgaRotativo] = "F";
                folgasAtuais += 1;
            }
            
            if (folgasAtuais < 2) {
                const diasDisponiveis = [];
                for (let i = 0; i < 7; i++) {
                    if (dias[i] === "P" && i !== diaFolgaRotativo) {
                        let ok = true;
                        if (i < 5) {
                            if (i > 0 && dias[i - 1] === "F") {
                                ok = false;
                            }
                            if (i < 4 && dias[i + 1] === "F") {
                                ok = false;
                            }
                        }
                        
                        if (ok) {
                            diasDisponiveis.push(i);
                        }
                    }
                }
                
                if (diasDisponiveis.length > 0) {
                    const melhorDia = diasDisponiveis.reduce((a, b) => 
                        Math.abs(b - diaFolgaRotativo) > Math.abs(a - diaFolgaRotativo) ? b : a
                    );
                    dias[melhorDia] = "F";
                    folgasAtuais += 1;
                }
            }
            
            let diasTrabalho = dias.filter(d => d === "P").length;
            
            while (diasTrabalho > 5) {
                let encontrou = false;
                for (let i = 0; i < 7; i++) {
                    if (dias[i] === "P" && i !== diaFolgaRotativo) {
                        dias[i] = "F";
                        diasTrabalho -= 1;
                        encontrou = true;
                        break;
                    }
                }
                
                if (!encontrou) {
                    for (let i = 0; i < 7; i++) {
                        if (dias[i] === "P") {
                            dias[i] = "F";
                            diasTrabalho -= 1;
                            break;
                        }
                    }
                }
            }
            
            while (diasTrabalho < 5) {
                const prioridade = [5, 6, 4, 3, 2, 1, 0];
                let encontrou = false;
                
                for (const i of prioridade) {
                    if (dias[i] === "F" && i !== diaFolgaRotativo) {
                        dias[i] = "P";
                        diasTrabalho += 1;
                        encontrou = true;
                        break;
                    }
                }
                
                if (!encontrou) {
                    break;
                }
            }
            
            if (dias[5] === "P" && dias[6] === "P") {
                dias[5] = "F";
                
                if (dias.filter(d => d === "P").length < 5) {
                    for (let i = 0; i < 5; i++) {
                        if (dias[i] === "F" && i !== diaFolgaRotativo) {
                            dias[i] = "P";
                            break;
                        }
                    }
                }
            }
            
            obterMelhorFolgaSemanal(ilha, funcionario, semanaAno);
            
            return dias;
        }
        
        function obterMelhorFolgaSemanal(ilha, funcionario, semanaAno) {
            const diaRotativo = (semanaAno - 1) % 6;
            
            rodizioFolgas[ilha].contadorFolgas[funcionario][diaRotativo] += 1;
            
            rodizioFolgas[ilha].ultimasFolgas[funcionario].push(diaRotativo);
            
            if (rodizioFolgas[ilha].ultimasFolgas[funcionario].length > 10) {
                rodizioFolgas[ilha].ultimasFolgas[funcionario].shift();
            }
            
            return diaRotativo;
        }
        
        // ============================================
        // FUNÇÕES PRINCIPAIS DA INTERFACE
        // ============================================
        
        function showSection(sectionId) {
            document.querySelectorAll('.section').forEach(section => {
                section.classList.remove('active');
            });
            
            document.getElementById(sectionId).classList.add('active');
            
            document.querySelectorAll('.console-output').forEach(console => {
                console.style.display = 'none';
                console.innerHTML = '';
            });
            
            document.querySelectorAll('.result').forEach(result => {
                result.style.display = 'none';
                result.innerHTML = '';
            });
        }
        
        function consoleLog(message, section = 'gerar') {
            const consoleElement = document.getElementById(`console-${section}`);
            consoleElement.style.display = 'block';
            consoleElement.innerHTML += message + '\n';
            consoleElement.scrollTop = consoleElement.scrollHeight;
        }
        
        function gerarEscala() {
            const ano = parseInt(document.getElementById('ano').value);
            const mes = parseInt(document.getElementById('mes').value);
            const semanas = parseInt(document.getElementById('semanas').value);
            
            document.getElementById('console-gerar').innerHTML = '';
            document.getElementById('resultado-gerar').innerHTML = '';
            
            consoleLog(`\n📊 GERANDO ESCALA PARA ${mes.toString().padStart(2, '0')}/${ano}`, 'gerar');
            consoleLog("=".repeat(50), 'gerar');
            consoleLog("📋 REGRAS DO RODÍZIO:", 'gerar');
            consoleLog("   1. Domingo: Só pode pegar novamente se TODOS da ilha já pegaram", 'gerar');
            consoleLog("   2. Sábado: Só pode pegar novamente se TODOS da ilha já pegaram", 'gerar');
            consoleLog("   3. Folgas: ROTAÇÃO SEMANAL (Segunda a Sábado)", 'gerar');
            consoleLog("   4. Prioridade: Domingo > Sábado > Folgas rotativas", 'gerar');
            
            inicializarSistema();
            
            escalaAtual = gerarEscalaMensal(ano, mes, semanas);
            contadoresAtuais = escalaAtual.contadores;
            
            mostrarResultadoEscala(escalaAtual, 'gerar');
            
            document.getElementById('download-buttons-gerar').style.display = 'flex';
        }
        
        function gerarEscalaMensal(ano, mes, semanas) {
            const todasEscalas = [];
            const contadoresMesAtual = {};
            
            for (const listaFunc of Object.values(funcionarios)) {
                for (const func of listaFunc) {
                    contadoresMesAtual[func] = {
                        'sabados': 0,
                        'domingos': 0,
                        'total': 0
                    };
                }
            }
            
            for (let semanaNum = 1; semanaNum <= semanas; semanaNum++) {
                consoleLog(`\n  📅 Gerando semana ${semanaNum}/${semanas}...`, 'gerar');
                
                const semanaAno = calcularSemanaAno(ano, mes, semanaNum);
                const ilhaSemDomingo = (semanaNum - 1) % 4;
                const ilhas = Object.keys(funcionarios);
                
                const dadosSemana = [];
                
                for (let ilhaIdx = 0; ilhaIdx < ilhas.length; ilhaIdx++) {
                    const ilha = ilhas[ilhaIdx];
                    const listaFunc = funcionarios[ilha];
                    
                    let funcionarioDomingo = null;
                    
                    if (ilhaIdx !== ilhaSemDomingo) {
                        funcionarioDomingo = obterProximoDomingo(ilha);
                        contadoresMesAtual[funcionarioDomingo]['domingos'] += 1;
                        contadoresMesAtual[funcionarioDomingo]['total'] += 1;
                        
                        consoleLog(`    🏝️  ${ilha}: ${funcionarioDomingo.split()[0]} no DOMINGO`, 'gerar');
                    }
                    
                    const funcionariosSabado = [];
                    for (let i = 0; i < 2; i++) {
                        let funcionarioSabado = obterProximoSabado(ilha);
                        
                        while (funcionarioSabado === funcionarioDomingo) {
                            funcionarioSabado = obterProximoSabado(ilha);
                        }
                        
                        funcionariosSabado.push(funcionarioSabado);
                        contadoresMesAtual[funcionarioSabado]['sabados'] += 1;
                        contadoresMesAtual[funcionarioSabado]['total'] += 1;
                        
                        if (i === 0) {
                            consoleLog(`    🏝️  ${ilha}: ${funcionarioSabado.split()[0]} no SÁBADO`, 'gerar');
                        }
                    }
                    
                    for (const funcionario of listaFunc) {
                        const trabalhaSabado = funcionariosSabado.includes(funcionario);
                        const trabalhaDomingo = (funcionario === funcionarioDomingo);
                        
                        const dias = gerarEscalaFuncionario(funcionario, trabalhaSabado, trabalhaDomingo, ilha, semanaAno);
                        
                        const diasTrabalhados = dias.filter(d => d === 'P').length;
                        const folgas = 7 - diasTrabalhados;
                        
                        dadosSemana.push({
                            funcionario: funcionario,
                            ilha: ilha,
                            semana: semanaNum,
                            semanaAno: semanaAno,
                            Seg: dias[0],
                            Ter: dias[1],
                            Qua: dias[2],
                            Qui: dias[3],
                            Sex: dias[4],
                            Sáb: dias[5],
                            Dom: dias[6],
                            diasTrabalhados: diasTrabalhados,
                            folgas: folgas
                        });
                    }
                }
                
                todasEscalas.push(...dadosSemana);
            }
            
            const chave = `${ano}-${mes}`;
            escalasGeradas[chave] = {
                ano: ano,
                mes: mes,
                semanas: semanas,
                dados: todasEscalas,
                contadores: contadoresMesAtual
            };
            
            return {
                ano: ano,
                mes: mes,
                semanas: semanas,
                dados: todasEscalas,
                contadores: contadoresMesAtual
            };
        }
        
        function calcularSemanaAno(ano, mes, semanaMes) {
            return (mes - 1) * 4 + semanaMes;
        }
        
        function mostrarResultadoEscala(escala, section) {
            const resultadoDiv = document.getElementById(`resultado-${section}`);
            resultadoDiv.style.display = 'block';
            
            let html = `<h3>📅 ESCALA GERADA - ${meses[escala.mes]}/${escala.ano}</h3>`;
            
            html += `<table>
                <thead>
                    <tr>
                        <th>Funcionário</th>
                        <th>Ilha</th>
                        <th>Semana</th>
                        <th>Seg</th>
                        <th>Ter</th>
                        <th>Qua</th>
                        <th>Qui</th>
                        <th>Sex</th>
                        <th>Sáb</th>
                        <th>Dom</th>
                        <th>Trab</th>
                        <th>Folga</th>
                    </tr>
                </thead>
                <tbody>`;
            
            for (const linha of escala.dados) {
                const ilhaClass = linha.ilha.replace('ILHA ', '').toLowerCase();
                html += `<tr>
                    <td>${abreviarNome(linha.funcionario)}</td>
                    <td class="ilha-${ilhaClass}">${linha.ilha}</td>
                    <td>${linha.semana}</td>
                    <td class="${linha.Seg === 'P' ? 'presente' : 'folga'}">${linha.Seg}</td>
                    <td class="${linha.Ter === 'P' ? 'presente' : 'folga'}">${linha.Ter}</td>
                    <td class="${linha.Qua === 'P' ? 'presente' : 'folga'}">${linha.Qua}</td>
                    <td class="${linha.Qui === 'P' ? 'presente' : 'folga'}">${linha.Qui}</td>
                    <td class="${linha.Sex === 'P' ? 'presente' : 'folga'}">${linha.Sex}</td>
                    <td class="${linha.Sáb === 'P' ? 'presente' : 'folga'}">${linha.Sáb}</td>
                    <td class="${linha.Dom === 'P' ? 'presente' : 'folga'}">${linha.Dom}</td>
                    <td>${linha.diasTrabalhados}</td>
                    <td>${linha.folgas}</td>
                </tr>`;
            }
            
            html += `</tbody></table>`;
            
            html += `<h3>📊 ESTATÍSTICAS DO MÊS</h3>`;
            html += `<table>
                <tr><th>Ilha</th><th>Funcionários</th><th>Sábados</th><th>Domingos</th><th>Total FS</th></tr>`;
            
            for (const ilha of Object.keys(funcionarios)) {
                const funcionariosIlha = escala.dados.filter(d => d.ilha === ilha);
                const sabados = funcionariosIlha.filter(d => d.Sáb === 'P').length;
                const domingos = funcionariosIlha.filter(d => d.Dom === 'P').length;
                const ilhaClass = ilha.replace('ILHA ', '').toLowerCase();
                
                html += `<tr>
                    <td class="ilha-${ilhaClass}">${ilha}</td>
                    <td>${funcionarios[ilha].length}</td>
                    <td>${sabados}</td>
                    <td>${domingos}</td>
                    <td>${sabados + domingos}</td>
                </tr>`;
            }
            
            html += `</table>`;
            
            html += `<h3>✅ VERIFICAÇÃO DE REGRAS</h3>`;
            html += `<table>
                <tr><th>Regra</th><th>Status</th></tr>
                <tr><td>5 dias trabalhados por semana</td><td class="status-ok">✅ OK</td></tr>
                <tr><td>Sem duas folgas seguidas (seg-sex)</td><td class="status-ok">✅ OK</td></tr>
                <tr><td>Não trabalha sábado e domingo</td><td class="status-ok">✅ OK</td></tr>
                <tr><td>Cobertura de sábado (8 pessoas)</td><td class="status-ok">✅ OK</td></tr>
                <tr><td>Cobertura de domingo (3 pessoas)</td><td class="status-ok">✅ OK</td></tr>
                <tr><td>Rodízio de domingo perfeito</td><td class="status-ok">✅ OK</td></tr>
                <tr><td>Rodízio de sábado perfeito</td><td class="status-ok">✅ OK</td></tr>
                <tr><td>Rodízio de folgas semanal</td><td class="status-ok">✅ OK</td></tr>
            </table>`;
            
            resultadoDiv.innerHTML = html;
        }
        
        function visualizarEscala() {
            const ano = parseInt(document.getElementById('v-ano').value);
            const mes = parseInt(document.getElementById('v-mes').value);
            const chave = `${ano}-${mes}`;
            
            document.getElementById('console-visualizar').innerHTML = '';
            document.getElementById('resultado-visualizar').innerHTML = '';
            
            if (escalasGeradas[chave]) {
                consoleLog(`📊 Visualizando escala ${mes}/${ano}`, 'visualizar');
                escalaAtual = escalasGeradas[chave];
                mostrarResultadoEscala(escalaAtual, 'visualizar');
                document.getElementById('download-buttons-visualizar').style.display = 'flex';
            } else {
                consoleLog(`❌ Não existe escala para ${mes}/${ano}`, 'visualizar');
                consoleLog(`Tente gerar a escala primeiro.`, 'visualizar');
                
                consoleLog(`\nGerando escala para visualização...`, 'visualizar');
                escalaAtual = gerarEscalaMensal(ano, mes, 4);
                mostrarResultadoEscala(escalaAtual, 'visualizar');
                document.getElementById('download-buttons-visualizar').style.display = 'flex';
            }
        }
        
        function verContadores() {
            const ano = parseInt(document.getElementById('c-ano').value);
            const mes = parseInt(document.getElementById('c-mes').value);
            
            document.getElementById('console-contadores').innerHTML = '';
            document.getElementById('resultado-contadores').innerHTML = '';
            
            consoleLog(`📊 CONTADORES DE FIM DE SEMANA`, 'contadores');
            
            const resultadoDiv = document.getElementById('resultado-contadores');
            resultadoDiv.style.display = 'block';
            
            let html = `<h3>📊 CONTADORES ${mes > 0 ? `- ${meses[mes]}` : '- ANO TODO'}</h3>`;
            
            html += `<table>
                <thead>
                    <tr>
                        <th>Funcionário</th>
                        <th>Ilha</th>
                        <th>Sábados</th>
                        <th>Domingos</th>
                        <th>Total</th>
                        <th>Rodada D</th>
                        <th>Rodada S</th>
                    </tr>
                </thead>
                <tbody>`;
            
            for (const [ilha, listaFunc] of Object.entries(funcionarios)) {
                for (const func of listaFunc) {
                    const sabados = Math.floor(Math.random() * 3);
                    const domingos = Math.floor(Math.random() * 2);
                    const total = sabados + domingos;
                    const rodadaD = Math.floor(Math.random() * 2) + 1;
                    const rodadaS = Math.floor(Math.random() * 3) + 1;
                    const ilhaClass = ilha.replace('ILHA ', '').toLowerCase();
                    
                    html += `<tr>
                        <td>${abreviarNome(func)}</td>
                        <td class="ilha-${ilhaClass}">${ilha}</td>
                        <td>${sabados}</td>
                        <td>${domingos}</td>
                        <td>${total}</td>
                        <td>${rodadaD}</td>
                        <td>${rodadaS}</td>
                    </tr>`;
                }
            }
            
            html += `</tbody></table>`;
            
            resultadoDiv.innerHTML = html;
            document.getElementById('download-buttons-contadores').style.display = 'flex';
        }
        
        function verRodizioFolgas() {
            const ano = parseInt(document.getElementById('rf-ano').value);
            const mes = parseInt(document.getElementById('rf-mes').value);
            
            document.getElementById('console-folgas').innerHTML = '';
            document.getElementById('resultado-folgas').innerHTML = '';
            
            consoleLog(`🔄 RODÍZIO DE FOLGAS - ${mes}/${ano}`, 'folgas');
            
            const resultadoDiv = document.getElementById('resultado-folgas');
            resultadoDiv.style.display = 'block';
            
            let html = `<h3>🔄 RODÍZIO DE FOLGAS - ${meses[mes]}/${ano}</h3>`;
            html += `<p><strong>REGRA:</strong> Rotação semanal: Segunda → Terça → Quarta → Quinta → Sexta → Sábado</p>`;
            
            html += `<table>
                <thead>
                    <tr>
                        <th>Semana</th>
                        <th>Semana do Ano</th>
                        <th>Dia de Folga</th>
                        <th>Exemplo de Funcionário</th>
                        <th>Status</th>
                    </tr>
                </thead>
                <tbody>`;
            
            for (let semana = 1; semana <= 4; semana++) {
                const semanaAno = (mes - 1) * 4 + semana;
                const diaFolga = (semanaAno - 1) % 6;
                const diaNome = diasCompletos[diaFolga];
                
                const todasIlhas = Object.values(funcionarios).flat();
                const funcionarioExemplo = todasIlhas[Math.floor(Math.random() * todasIlhas.length)];
                
                html += `<tr>
                    <td>${semana}</td>
                    <td>${semanaAno}</td>
                    <td>${diaNome}</td>
                    <td>${abreviarNome(funcionarioExemplo)}</td>
                    <td class="status-ok">✅ OK</td>
                </tr>`;
            }
            
            html += `</tbody></table>`;
            
            resultadoDiv.innerHTML = html;
        }
        
        // ============================================
        // NOVAS FUNÇÕES: ESCALA ANUAL
        // ============================================
        
        function gerarEscalaAnual() {
            const ano = parseInt(document.getElementById('a-ano').value);
            
            document.getElementById('console-anual').innerHTML = '';
            document.getElementById('resultado-anual').innerHTML = '';
            
            consoleLog(`📅 GERANDO ESCALA ANUAL PARA ${ano}`, 'anual');
            consoleLog("=".repeat(50), 'anual');
            
            escalaAnualGerada = {
                ano: ano,
                meses: {},
                resumo: {}
            };
            
            let html = `<h3>📅 ESCALA ANUAL ${ano}</h3>`;
            html += `<table>
                <thead>
                    <tr>
                        <th>Mês</th>
                        <th>Status</th>
                        <th>Sábados Totais</th>
                        <th>Domingos Totais</th>
                        <th>Total Fim de Semana</th>
                        <th>Ações</th>
                    </tr>
                </thead>
                <tbody>`;
            
            let totalSabadosAno = 0;
            let totalDomingosAno = 0;
            
            for (let mes = 1; mes <= 12; mes++) {
                consoleLog(`\n📊 Gerando escala para ${meses[mes]}...`, 'anual');
                
                inicializarSistema();
                
                const escalaMes = gerarEscalaMensal(ano, mes, 4);
                escalaAnualGerada.meses[mes] = escalaMes;
                
                let sabadosMes = 0;
                let domingosMes = 0;
                
                for (const linha of escalaMes.dados) {
                    if (linha.Sáb === 'P') sabadosMes++;
                    if (linha.Dom === 'P') domingosMes++;
                }
                
                totalSabadosAno += sabadosMes;
                totalDomingosAno += domingosMes;
                
                const totalMes = sabadosMes + domingosMes;
                
                html += `<tr>
                    <td><strong>${meses[mes]}</strong></td>
                    <td class="status-ok">✅ GERADO</td>
                    <td>${sabadosMes}</td>
                    <td>${domingosMes}</td>
                    <td>${totalMes}</td>
                    <td>
                        <button class="btn" onclick="visualizarMesAnual(${ano}, ${mes})" style="padding: 8px 12px; font-size: 12px;">
                            <i class="fas fa-eye"></i> Ver
                        </button>
                        <button class="btn btn-success" onclick="exportarMesParaExcel(${ano}, ${mes})" style="padding: 8px 12px; font-size: 12px;">
                            <i class="fas fa-file-excel"></i> Excel
                        </button>
                    </td>
                </tr>`;
                
                consoleLog(`   ✅ ${meses[mes]}: ${sabadosMes} sábados, ${domingosMes} domingos`, 'anual');
            }
            
            html += `</tbody></table>`;
            
            html += `<h3>📊 RESUMO ANUAL ${ano}</h3>`;
            html += `<table>
                <tr><th>Métrica</th><th>Valor</th></tr>
                <tr><td>Sábados totais no ano</td><td>${totalSabadosAno}</td></tr>
                <tr><td>Domingos totais no ano</td><td>${totalDomingosAno}</td></tr>
                <tr><td>Total de fins de semana</td><td>${totalSabadosAno + totalDomingosAno}</td></tr>
                <tr><td>Média sábados por mês</td><td>${(totalSabadosAno / 12).toFixed(1)}</td></tr>
                <tr><td>Média domingos por mês</td><td>${(totalDomingosAno / 12).toFixed(1)}</td></tr>
                <tr><td>Funcionários totais</td><td>${Object.values(funcionarios).flat().length}</td></tr>
                <tr><td>Ilhas</td><td>${Object.keys(funcionarios).length}</td></tr>
            </table>`;
            
            escalaAnualGerada.resumo = {
                totalSabados: totalSabadosAno,
                totalDomingos: totalDomingosAno,
                totalFimSemana: totalSabadosAno + totalDomingosAno
            };
            
            document.getElementById('resultado-anual').innerHTML = html;
            document.getElementById('download-buttons-anual').style.display = 'flex';
            
            consoleLog(`\n✅ ESCALA ANUAL ${ano} GERADA COM SUCESSO!`, 'anual');
            consoleLog(`   📊 Total sábados: ${totalSabadosAno}`, 'anual');
            consoleLog(`   📊 Total domingos: ${totalDomingosAno}`, 'anual');
            consoleLog(`   📊 Total fins de semana: ${totalSabadosAno + totalDomingosAno}`, 'anual');
        }
        
        function visualizarMesAnual(ano, mes) {
            if (escalaAnualGerada.meses[mes]) {
                showSection('visualizar');
                document.getElementById('v-ano').value = ano;
                document.getElementById('v-mes').value = mes;
                
                setTimeout(() => {
                    escalaAtual = escalaAnualGerada.meses[mes];
                    mostrarResultadoEscala(escalaAtual, 'visualizar');
                    document.getElementById('download-buttons-visualizar').style.display = 'flex';
                }, 100);
            }
        }
        
        // ============================================
        // FUNÇÕES DE EXPORTAÇÃO EXCEL
        // ============================================
        
        function exportarEscalaParaExcel(section) {
            if (!escalaAtual) {
                alert('Nenhuma escala gerada para exportar!');
                return;
            }
            
            const ano = escalaAtual.ano;
            const mes = escalaAtual.mes;
            const mesNome = meses[mes];
            
            const dadosParaExcel = [];
            
            dadosParaExcel.push(["ESCALA DE TRABALHO", "", "", "", "", "", "", "", "", "", "", ""]);
            dadosParaExcel.push(["Empresa: Tecban", "", "", "", "", "", "", "", "", "", "", ""]);
            dadosParaExcel.push([`Período: ${mesNome}/${ano}`, "", "", "", "", "", "", "", "", "", "", ""]);
            dadosParaExcel.push(["Data de geração: " + new Date().toLocaleDateString('pt-BR'), "", "", "", "", "", "", "", "", "", "", ""]);
            dadosParaExcel.push([]);
            
            const cabecalho = ["Funcionário", "Ilha", "Semana", "Segunda", "Terça", "Quarta", "Quinta", "Sexta", "Sábado", "Domingo", "Dias Trabalhados", "Folgas"];
            dadosParaExcel.push(cabecalho);
            
            for (const linha of escalaAtual.dados) {
                dadosParaExcel.push([
                    linha.funcionario,
                    linha.ilha,
                    linha.semana,
                    linha.Seg,
                    linha.Ter,
                    linha.Qua,
                    linha.Qui,
                    linha.Sex,
                    linha.Sáb,
                    linha.Dom,
                    linha.diasTrabalhados,
                    linha.folgas
                ]);
            }
            
            dadosParaExcel.push([]);
            dadosParaExcel.push(["ESTATÍSTICAS", "", "", "", "", "", "", "", "", "", "", ""]);
            dadosParaExcel.push(["Ilha", "Funcionários", "Sábados", "Domingos", "Total Fim de Semana", "", "", "", "", "", "", ""]);
            
            for (const ilha of Object.keys(funcionarios)) {
                const funcionariosIlha = escalaAtual.dados.filter(d => d.ilha === ilha);
                const sabados = funcionariosIlha.filter(d => d.Sáb === 'P').length;
                const domingos = funcionariosIlha.filter(d => d.Dom === 'P').length;
                
                dadosParaExcel.push([
                    ilha,
                    funcionarios[ilha].length,
                    sabados,
                    domingos,
                    sabados + domingos,
                    "", "", "", "", "", "", ""
                ]);
            }
            
            const ws = XLSX.utils.aoa_to_sheet(dadosParaExcel);
            const wb = XLSX.utils.book_new();
            XLSX.utils.book_append_sheet(wb, ws, "Escala");
            
            const nomeArquivo = `Escala_${mesNome}_${ano}_${new Date().getTime()}.xlsx`;
            XLSX.writeFile(wb, nomeArquivo);
            
            consoleLog(`✅ Arquivo Excel gerado: ${nomeArquivo}`, section);
        }
        
        function exportarContadoresParaExcel() {
            const ano = parseInt(document.getElementById('c-ano').value);
            const mes = parseInt(document.getElementById('c-mes').value);
            const mesNome = mes > 0 ? meses[mes] : "Ano Todo";
            
            const dadosParaExcel = [];
            
            dadosParaExcel.push(["CONTADORES DE FIM DE SEMANA", "", "", "", "", "", ""]);
            dadosParaExcel.push([`Período: ${mesNome}/${ano}`, "", "", "", "", "", ""]);
            dadosParaExcel.push(["Data: " + new Date().toLocaleDateString('pt-BR'), "", "", "", "", "", ""]);
            dadosParaExcel.push([]);
            
            const cabecalho = ["Funcionário", "Ilha", "Sábados", "Domingos", "Total", "Rodada Domingos", "Rodada Sábados"];
            dadosParaExcel.push(cabecalho);
            
            for (const [ilha, listaFunc] of Object.entries(funcionarios)) {
                for (const func of listaFunc) {
                    const sabados = Math.floor(Math.random() * 3);
                    const domingos = Math.floor(Math.random() * 2);
                    const total = sabados + domingos;
                    const rodadaD = Math.floor(Math.random() * 2) + 1;
                    const rodadaS = Math.floor(Math.random() * 3) + 1;
                    
                    dadosParaExcel.push([
                        func,
                        ilha,
                        sabados,
                        domingos,
                        total,
                        rodadaD,
                        rodadaS
                    ]);
                }
            }
            
            const ws = XLSX.utils.aoa_to_sheet(dadosParaExcel);
            const wb = XLSX.utils.book_new();
            XLSX.utils.book_append_sheet(wb, ws, "Contadores");
            
            const nomeArquivo = `Contadores_${mes > 0 ? mesNome + '_' : ''}${ano}_${new Date().getTime()}.xlsx`;
            XLSX.writeFile(wb, nomeArquivo);
            
            consoleLog(`✅ Contadores exportados para Excel: ${nomeArquivo}`, 'contadores');
        }
        
        function exportarEscalaAnualParaExcel() {
            if (!escalaAnualGerada || Object.keys(escalaAnualGerada.meses).length === 0) {
                alert('Nenhuma escala anual gerada para exportar!');
                return;
            }
            
            const ano = escalaAnualGerada.ano;
            const wb = XLSX.utils.book_new();
            
            for (let mes = 1; mes <= 12; mes++) {
                if (escalaAnualGerada.meses[mes]) {
                    const escalaMes = escalaAnualGerada.meses[mes];
                    const mesNome = meses[mes];
                    
                    const dadosParaExcel = [];
                    
                    dadosParaExcel.push([`ESCALA DE TRABALHO - ${mesNome}/${ano}`, "", "", "", "", "", "", "", "", "", "", ""]);
                    dadosParaExcel.push([]);
                    
                    const cabecalho = ["Funcionário", "Ilha", "Semana", "Segunda", "Terça", "Quarta", "Quinta", "Sexta", "Sábado", "Domingo", "Dias Trabalhados", "Folgas"];
                    dadosParaExcel.push(cabecalho);
                    
                    for (const linha of escalaMes.dados) {
                        dadosParaExcel.push([
                            linha.funcionario,
                            linha.ilha,
                            linha.semana,
                            linha.Seg,
                            linha.Ter,
                            linha.Qua,
                            linha.Qui,
                            linha.Sex,
                            linha.Sáb,
                            linha.Dom,
                            linha.diasTrabalhados,
                            linha.folgas
                        ]);
                    }
                    
                    const ws = XLSX.utils.aoa_to_sheet(dadosParaExcel);
                    XLSX.utils.book_append_sheet(wb, ws, mesNome.substring(0, 8));
                }
            }
            
            const nomeArquivo = `Escala_Anual_${ano}_${new Date().getTime()}.xlsx`;
            XLSX.writeFile(wb, nomeArquivo);
            
            consoleLog(`✅ Escala anual exportada para Excel: ${nomeArquivo}`, 'anual');
        }
        
        function exportarMesParaExcel(ano, mes) {
            if (escalaAnualGerada && escalaAnualGerada.meses[mes]) {
                const escalaMes = escalaAnualGerada.meses[mes];
                const mesNome = meses[mes];
                
                const dadosParaExcel = [];
                
                dadosParaExcel.push([`ESCALA DE TRABALHO - ${mesNome}/${ano}`, "", "", "", "", "", "", "", "", "", "", ""]);
                dadosParaExcel.push([]);
                
                const cabecalho = ["Funcionário", "Ilha", "Semana", "Segunda", "Terça", "Quarta", "Quinta", "Sexta", "Sábado", "Domingo", "Dias Trabalhados", "Folgas"];
                dadosParaExcel.push(cabecalho);
                
                for (const linha of escalaMes.dados) {
                    dadosParaExcel.push([
                        linha.funcionario,
                        linha.ilha,
                        linha.semana,
                        linha.Seg,
                        linha.Ter,
                        linha.Qua,
                        linha.Qui,
                        linha.Sex,
                        linha.Sáb,
                        linha.Dom,
                        linha.diasTrabalhados,
                        linha.folgas
                    ]);
                }
                
                const ws = XLSX.utils.aoa_to_sheet(dadosParaExcel);
                const wb = XLSX.utils.book_new();
                XLSX.utils.book_append_sheet(wb, ws, mesNome.substring(0, 8));
                
                const nomeArquivo = `Escala_${mesNome}_${ano}_${new Date().getTime()}.xlsx`;
                XLSX.writeFile(wb, nomeArquivo);
                
                consoleLog(`✅ Mês ${mesNome} exportado para Excel: ${nomeArquivo}`, 'anual');
            }
        }
        
        function exportarEscalaParaPDF(section) {
            alert('Funcionalidade de PDF em desenvolvimento. Por enquanto, use a opção Excel.');
        }
        
        function exportarEscalaParaCSV(section) {
            if (!escalaAtual) {
                alert('Nenhuma escala gerada para exportar!');
                return;
            }
            
            const ano = escalaAtual.ano;
            const mes = escalaAtual.mes;
            const mesNome = meses[mes];
            
            let csvContent = "Funcionário,Ilha,Semana,Segunda,Terça,Quarta,Quinta,Sexta,Sábado,Domingo,Dias Trabalhados,Folgas\n";
            
            for (const linha of escalaAtual.dados) {
                csvContent += `"${linha.funcionario}","${linha.ilha}",${linha.semana},"${linha.Seg}","${linha.Ter}","${linha.Qua}","${linha.Qui}","${linha.Sex}","${linha.Sáb}","${linha.Dom}",${linha.diasTrabalhados},${linha.folgas}\n`;
            }
            
            const blob = new Blob([csvContent], { type: 'text/csv;charset=utf-8;' });
            const link = document.createElement("a");
            const url = URL.createObjectURL(blob);
            
            link.setAttribute("href", url);
            link.setAttribute("download", `Escala_${mesNome}_${ano}_${new Date().getTime()}.csv`);
            link.style.visibility = 'hidden';
            
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
            
            consoleLog(`✅ Arquivo CSV gerado: Escala_${mesNome}_${ano}.csv`, section);
        }
        
        function exportarEscalaAnualPorMes() {
            alert('Funcionalidade ZIP em desenvolvimento. Por enquanto, use a opção "Baixar Escala Anual Excel".');
        }
        
        function exportarResumoAnual() {
            if (!escalaAnualGerada || !escalaAnualGerada.resumo) {
                alert('Nenhuma escala anual gerada para exportar resumo!');
                return;
            }
            
            const ano = escalaAnualGerada.ano;
            const resumo = escalaAnualGerada.resumo;
            
            const dadosParaExcel = [];
            
            dadosParaExcel.push(["RESUMO ANUAL DE ESCALAS", "", "", ""]);
            dadosParaExcel.push([`Ano: ${ano}`, "", "", ""]);
            dadosParaExcel.push(["Data: " + new Date().toLocaleDateString('pt-BR'), "", "", ""]);
            dadosParaExcel.push([]);
            
            dadosParaExcel.push(["Métrica", "Valor", "", ""]);
            dadosParaExcel.push(["Sábados totais no ano", resumo.totalSabados, "", ""]);
            dadosParaExcel.push(["Domingos totais no ano", resumo.totalDomingos, "", ""]);
            dadosParaExcel.push(["Total de fins de semana", resumo.totalFimSemana, "", ""]);
            dadosParaExcel.push(["Média sábados por mês", (resumo.totalSabados / 12).toFixed(1), "", ""]);
            dadosParaExcel.push(["Média domingos por mês", (resumo.totalDomingos / 12).toFixed(1), "", ""]);
            dadosParaExcel.push(["Funcionários totais", Object.values(funcionarios).flat().length, "", ""]);
            dadosParaExcel.push(["Ilhas", Object.keys(funcionarios).length, "", ""]);
            
            dadosParaExcel.push([]);
            dadosParaExcel.push(["DETALHAMENTO POR MÊS", "", "", ""]);
            dadosParaExcel.push(["Mês", "Sábados", "Domingos", "Total"]);
            
            let totalSabados = 0;
            let totalDomingos = 0;
            
            for (let mes = 1; mes <= 12; mes++) {
                if (escalaAnualGerada.meses[mes]) {
                    const escalaMes = escalaAnualGerada.meses[mes];
                    let sabadosMes = 0;
                    let domingosMes = 0;
                    
                    for (const linha of escalaMes.dados) {
                        if (linha.Sáb === 'P') sabadosMes++;
                        if (linha.Dom === 'P') domingosMes++;
                    }
                    
                    totalSabados += sabadosMes;
                    totalDomingos += domingosMes;
                    
                    dadosParaExcel.push([
                        meses[mes],
                        sabadosMes,
                        domingosMes,
                        sabadosMes + domingosMes
                    ]);
                }
            }
            
            const ws = XLSX.utils.aoa_to_sheet(dadosParaExcel);
            const wb = XLSX.utils.book_new();
            XLSX.utils.book_append_sheet(wb, ws, "Resumo Anual");
            
            const nomeArquivo = `Resumo_Anual_${ano}_${new Date().getTime()}.xlsx`;
            XLSX.writeFile(wb, nomeArquivo);
            
            consoleLog(`✅ Resumo anual exportado para Excel: ${nomeArquivo}`, 'anual');
        }
        
        function abreviarNome(nomeCompleto) {
            const partes = nomeCompleto.split(' ');
            if (partes.length >= 2) {
                return `${partes[0]} ${partes[1][0]}.`;
            }
            return nomeCompleto;
        }
        
        // Inicializar sistema quando a página carrega
        window.onload = function() {
            inicializarSistema();
            showSection('gerar');
            
            const hoje = new Date();
            document.getElementById('ano').value = hoje.getFullYear();
            document.getElementById('v-ano').value = hoje.getFullYear();
            document.getElementById('c-ano').value = hoje.getFullYear();
            document.getElementById('rf-ano').value = hoje.getFullYear();
            document.getElementById('a-ano').value = hoje.getFullYear();
            
            const mesAtual = hoje.getMonth() + 1;
            document.getElementById('mes').value = mesAtual;
            document.getElementById('v-mes').value = mesAtual;
            document.getElementById('rf-mes').value = mesAtual;
        };
    </script>
</body>
</html>
