<index.html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Portal del Expediente Electrónico - Poder Judicial</title>
    <!-- Fuentes e Iconos Modernos -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <style>
        :root {
            --magenta-primary: #8B005B;
            --magenta-dark: #660046;
            --magenta-light: #fdf2f8;
            --magenta-border: #fbcfe8;
            --bg-body: #ffffff;
            --text-main: #1e293b;
            --text-muted: #64748b;
            --card-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.05), 0 8px 10px -6px rgba(0, 0, 0, 0.01);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Inter', sans-serif;
        }

        body {
            background-color: var(--bg-body);
            color: var(--text-main);
            display: flex;
            flex-direction: column;
            min-height: 100vh;
        }

        /* 1. CARGAPANTALLA INICIAL (SPLASH SCREEN) */
        #splash-screen {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(255, 255, 255, 0.98);
            backdrop-filter: blur(5px);
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            z-index: 9999;
            transition: opacity 0.5s ease, visibility 0.5s ease;
        }

        .loader-brand {
            font-size: 2rem;
            font-weight: 800;
            color: var(--magenta-primary);
            margin-bottom: 20px;
            letter-spacing: -0.5px;
        }

        .spinner-modern {
            width: 48px;
            height: 48px;
            border: 4px solid var(--magenta-border);
            border-top: 4px solid var(--magenta-primary);
            border-radius: 50%;
            animation: spin 0.8s linear infinite;
            margin-bottom: 25px;
        }

        @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }

        .academic-toast {
            background: linear-gradient(135deg, var(--magenta-primary), var(--magenta-dark));
            color: white;
            padding: 16px 24px;
            border-radius: 12px;
            font-size: 0.88rem;
            text-align: center;
            max-width: 500px;
            box-shadow: 0 20px 25px -5px rgba(139, 0, 91, 0.25);
            line-height: 1.5;
        }

        /* 2. ENCABEZADO Y BRANDING */
        .top-header {
            padding: 12px 6%;
            display: flex;
            justify-content: flex-end;
            align-items: center;
            border-bottom: 1px solid #f1f5f9;
        }

        .brand-title {
            color: var(--magenta-primary);
            font-size: 1.25rem;
            font-weight: 800;
            letter-spacing: -0.3px;
            text-transform: uppercase;
        }

        /* 3. BARRA DE MENÚ HORIZONTAL MAGENTA MODERNA */
        .navbar-magenta {
            background: var(--magenta-primary);
            padding: 0 6%;
            display: flex;
            justify-content: space-between;
            align-items: center;
            position: sticky;
            top: 0;
            z-index: 100;
            box-shadow: 0 4px 20px rgba(139, 0, 91, 0.15);
        }

        .nav-menu {
            display: flex;
            list-style: none;
        }

        .nav-menu li a {
            display: flex;
            align-items: center;
            gap: 8px;
            padding: 16px 18px;
            color: rgba(255, 255, 255, 0.9);
            text-decoration: none;
            font-size: 0.88rem;
            font-weight: 500;
            transition: all 0.2s;
            cursor: pointer;
        }

        .nav-menu li a:hover, .nav-menu li a.active {
            background: var(--magenta-dark);
            color: #ffffff;
        }

        .btn-search-nav {
            background: rgba(255, 255, 255, 0.15) !important;
            font-weight: 700 !important;
            border-radius: 6px;
            margin: 6px 0;
        }

        .widgets-bar {
            display: flex;
            gap: 16px;
            background: rgba(0, 0, 0, 0.15);
            padding: 6px 14px;
            border-radius: 20px;
            font-size: 0.78rem;
            color: white;
            font-weight: 600;
        }

        /* 4. CONTENEDOR PRINCIPAL */
        .main-container {
            max-width: 1150px;
            margin: 30px auto;
            padding: 0 20px;
            flex: 1;
            width: 100%;
        }

        /* Info del Menú */
        .info-card {
            background: var(--magenta-light);
            border: 1px solid var(--magenta-border);
            padding: 16px 20px;
            margin-bottom: 25px;
            border-radius: 10px;
            display: none;
        }

        .info-card h4 { color: var(--magenta-primary); margin-bottom: 4px; }

        /* Búsqueda y Filtros */
        .search-section {
            background: #ffffff;
            border: 1px solid #e2e8f0;
            border-radius: 16px;
            padding: 30px;
            box-shadow: var(--card-shadow);
            margin-bottom: 30px;
        }

        .section-title-main {
            font-size: 1.2rem;
            font-weight: 700;
            color: var(--text-main);
            margin-bottom: 20px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .filter-tabs {
            display: flex;
            gap: 8px;
            background: #f8fafc;
            padding: 4px;
            border-radius: 10px;
            width: fit-content;
            margin-bottom: 25px;
        }

        .tab-btn {
            padding: 8px 20px;
            border: none;
            background: transparent;
            cursor: pointer;
            font-weight: 600;
            border-radius: 8px;
            font-size: 0.85rem;
            color: var(--text-muted);
            transition: all 0.2s;
        }

        .tab-btn.active {
            background: #ffffff;
            color: var(--magenta-primary);
            box-shadow: 0 2px 8px rgba(0,0,0,0.08);
        }

        .form-content { display: none; }
        .form-content.active { display: block; }

        .form-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
            gap: 20px;
            margin-bottom: 20px;
        }

        .form-group label {
            display: block;
            font-size: 0.8rem;
            font-weight: 700;
            color: #334155;
            margin-bottom: 6px;
        }

        .form-group input, .form-group select {
            width: 100%;
            padding: 11px 14px;
            border: 1px solid #cbd5e1;
            border-radius: 8px;
            font-size: 0.9rem;
            transition: border-color 0.2s;
        }

        .form-group input:focus, .form-group select:focus {
            outline: none;
            border-color: var(--magenta-primary);
        }

        /* NVO: BLOQUE DE CAPTCHA REAL DISTORSIONADO */
        .captcha-container {
            background: #f8fafc;
            border: 1px solid #e2e8f0;
            padding: 16px;
            border-radius: 10px;
            display: flex;
            align-items: center;
            gap: 15px;
            flex-wrap: wrap;
            margin-bottom: 25px;
            width: fit-content;
        }

        .captcha-code-canvas {
            background: #e2e8f0;
            padding: 8px 16px;
            font-family: 'Courier New', Courier, monospace;
            font-size: 1.3rem;
            font-weight: 900;
            letter-spacing: 5px;
            color: var(--magenta-primary);
            font-style: italic;
            text-decoration: line-through;
            user-select: none;
            border-radius: 6px;
            border: 1px dashed var(--magenta-primary);
        }

        .captcha-refresh {
            cursor: pointer;
            color: var(--text-muted);
            transition: color 0.2s;
        }

        .captcha-refresh:hover { color: var(--magenta-primary); }

        .btn-submit {
            background: var(--magenta-primary);
            color: white;
            border: none;
            padding: 12px 28px;
            font-size: 0.9rem;
            font-weight: 700;
            border-radius: 8px;
            cursor: pointer;
            transition: background 0.2s;
            display: inline-flex;
            align-items: center;
            gap: 8px;
        }

        .btn-submit:hover { background: var(--magenta-dark); }

        /* 5. VISTA DEL EXPEDIENTE */
        #expediente-view { display: none; }

        .card-header-exp {
            background: var(--magenta-primary);
            color: white;
            padding: 16px 24px;
            border-radius: 12px 12px 0 0;
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-weight: 700;
        }

        .badge-status {
            background: #22c55e;
            color: white;
            font-size: 0.75rem;
            padding: 4px 12px;
            border-radius: 20px;
        }

        .data-card-body {
            border: 1px solid #e2e8f0;
            border-top: none;
            padding: 24px;
            background: #ffffff;
            border-radius: 0 0 12px 12px;
            margin-bottom: 30px;
        }

        .table-custom {
            width: 100%;
            border-collapse: collapse;
            font-size: 0.88rem;
        }

        .table-custom td {
            padding: 12px;
            border-bottom: 1px solid #f1f5f9;
        }

        .table-custom tr:last-child td { border-bottom: none; }
        .td-label { font-weight: 700; color: #475569; width: 25%; }

        /* LÍNEA DE TIEMPO DINÁMICA */
        .timeline-box {
            background: #ffffff;
            border: 1px solid #e2e8f0;
            border-radius: 12px;
            padding: 24px;
            margin-bottom: 30px;
            box-shadow: var(--card-shadow);
        }

        .timeline-steps {
            display: flex;
            justify-content: space-between;
            position: relative;
            margin-top: 20px;
            flex-wrap: wrap;
            gap: 15px;
        }

        .timeline-steps::before {
            content: '';
            position: absolute;
            top: 18px; left: 0; width: 100%; height: 3px;
            background: #e2e8f0;
            z-index: 1;
        }

        .t-step {
            position: relative;
            z-index: 2;
            background: #ffffff;
            padding: 0 10px;
            text-align: center;
            flex: 1;
        }

        .t-icon {
            width: 38px; height: 38px;
            border-radius: 50%;
            background: #cbd5e1;
            color: white;
            display: flex; align-items: center; justify-content: center;
            margin: 0 auto 10px;
            font-size: 0.85rem;
            font-weight: 700;
        }

        .t-step.completed .t-icon { background: #22c55e; }
        .t-step.active .t-icon { background: var(--magenta-primary); box-shadow: 0 0 0 4px var(--magenta-border); }

        /* ENTES INTEROPERABLES */
        .entes-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(230px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }

        .ente-card {
            border: 1px solid #e2e8f0;
            border-radius: 12px;
            padding: 20px;
            text-align: center;
            background: #ffffff;
            cursor: pointer;
            transition: all 0.2s;
            box-shadow: var(--card-shadow);
        }

        .ente-card:hover {
            transform: translateY(-4px);
            border-color: var(--magenta-primary);
        }

        .ente-avatar {
            width: 55px; height: 55px;
            border-radius: 50%;
            background: var(--magenta-light);
            color: var(--magenta-primary);
            display: flex; align-items: center; justify-content: center;
            margin: 0 auto 12px;
            font-size: 1.4rem;
        }

        /* DOCUMENTOS Y RESOLUCIONES */
        .docs-table {
            width: 100%;
            border-collapse: collapse;
            font-size: 0.85rem;
            background: #ffffff;
            border: 1px solid #e2e8f0;
            border-radius: 8px;
            overflow: hidden;
        }

        .docs-table th {
            background: #f8fafc;
            color: #334155;
            padding: 12px 16px;
            text-align: left;
            font-weight: 700;
            border-bottom: 1px solid #e2e8f0;
        }

        .docs-table td { padding: 12px 16px; border-bottom: 1px solid #f1f5f9; }

        .btn-pdf {
            background: #ef4444;
            color: white;
            border: none;
            padding: 6px 12px;
            border-radius: 6px;
            font-size: 0.75rem;
            font-weight: 600;
            cursor: pointer;
        }

        /* MODALES */
        .modal-overlay {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(15, 23, 42, 0.6);
            backdrop-filter: blur(4px);
            display: flex; justify-content: center; align-items: center;
            z-index: 10000;
            display: none;
        }

        .modal-card {
            background: #ffffff;
            border-radius: 16px;
            max-width: 520px;
            width: 90%;
            padding: 28px;
            position: relative;
            box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25);
        }

        .close-btn {
            position: absolute; top: 16px; right: 20px;
            font-size: 1.2rem; color: var(--text-muted);
            cursor: pointer; border: none; background: none;
        }

        footer {
            background: #0f172a;
            color: #94a3b8;
            text-align: center;
            padding: 16px;
            font-size: 0.8rem;
            margin-top: auto;
        }

        @media(max-width:768px){
            .navbar-magenta { flex-direction: column; padding: 10px; }
            .nav-menu { width: 100%; justify-content: center; }
            .timeline-steps::before { display: none; }
        }
    </style>
</head>
<body>

    <!-- CARGAPANTALLA INICIAL -->
    <div id="splash-screen">
        <div class="loader-brand"><i class="fa-solid fa-scale-balanced"></i> Portal EJE</div>
        <div class="spinner-modern"></div>
        <div class="academic-toast">
            <strong>PROTOTIPO ACADÉMICO</strong><br>
            Asignatura: <strong>Gobierno Digital y Derecho Informático</strong><br>
            Estudiante: <em>Sonia Pilar Condori Ruelas</em> | Docente: <em>Michael Espinoza Coila</em>
        </div>
    </div>

    <!-- ENCABEZADO -->
    <header class="top-header">
        <div class="brand-title">Portal del Expediente Electrónico</div>
    </header>

    <!-- BARRA DE MENÚ HORIZONTAL MAGENTA -->
    <nav class="navbar-magenta">
        <ul class="nav-menu">
            <li><a class="active" onclick="showInfo('Inicio', 'Bienvenido al Portal del Expediente Electrónico. Utilice el buscador para consultar procesos judiciales.')"><i class="fa-solid fa-house"></i> Inicio</a></li>
            <li><a onclick="showInfo('Misión', 'Garantizar el acceso transparente y digital a los procesos judiciales mediante la modernización del EJE.')"><i class="fa-solid fa-bullseye"></i> Misión</a></li>
            <li><a onclick="showInfo('Visión', 'Ser una plataforma de justicia digital eficiente, confiable e interoperable.')"><i class="fa-solid fa-eye"></i> Visión</a></li>
            <li><a onclick="showInfo('Transparencia', 'Acceso libre a resoluciones y jurisprudencia conforme a ley.')"><i class="fa-solid fa-shield-halved"></i> Transparencia</a></li>
            <li><a onclick="showInfo('Contáctanos', 'Soporte Técnico EJE: soporte_eje@pj.gob.pe | Teléfono: (01) 410-0000')"><i class="fa-solid fa-envelope"></i> Contáctanos</a></li>
            <li><a class="btn-search-nav" onclick="scrollToSearch()"><i class="fa-solid fa-magnifying-glass"></i> Búsqueda</a></li>
        </ul>

        <div class="widgets-bar">
            <span><i class="fa-regular fa-clock"></i> <strong id="clock-display">00:00:00</strong></span>
            <span><i class="fa-solid fa-hourglass-start"></i> <strong id="timer-display">07:00</strong></span>
        </div>
    </nav>

    <!-- CONTENEDOR PRINCIPAL -->
    <main class="main-container">

        <div id="info-box" class="info-card">
            <h4 id="info-title">Inicio</h4>
            <p id="info-text" style="font-size: 0.88rem; color: #475569;"></p>
        </div>

        <!-- BÚSQUEDA DE EXPEDIENTE -->
        <section id="search-section" class="search-section">
            <div class="section-title-main"><i class="fa-solid fa-folder-search" style="color:var(--magenta-primary)"></i> Búsqueda de Expediente Judicial</div>
            
            <div class="filter-tabs">
                <button class="tab-btn active" onclick="switchFilter('numero')">Por Número de Expediente</button>
                <button class="tab-btn" onclick="switchFilter('partes')">Por Partes Procesales</button>
            </div>

            <!-- FILTRO 1: CÓDIGO -->
            <div id="filter-numero" class="form-content active">
                <form onsubmit="executeSearch(event, 'code')">
                    <div class="form-grid">
                        <div class="form-group">
                            <label>CÓDIGO DE EXPEDIENTE</label>
                            <input type="text" id="exp-code-input" value="00174-2019-0-2111-JR-LA-02" required>
                        </div>
                        <div class="form-group">
                            <label>DISTRITO JUDICIAL</label>
                            <select required><option selected>PUNO</option></select>
                        </div>
                    </div>

                    <!-- CAPTCHA INTERACTIVO -->
                    <div class="captcha-container">
                        <div class="captcha-code-canvas" id="captcha-code-1">8F2K9</div>
                        <i class="fa-solid fa-rotate-right captcha-refresh" onclick="generateCaptcha(1)"></i>
                        <input type="text" id="captcha-user-1" placeholder="Ingrese el código" style="padding: 8px 12px; border: 1px solid #cbd5e1; border-radius: 6px; width: 140px;" required>
                    </div>

                    <button type="submit" class="btn-submit"><i class="fa-solid fa-magnifying-glass"></i> Consultar Expediente</button>
                </form>
            </div>

            <!-- FILTRO 2: PARTES PROCESALES -->
            <div id="filter-partes" class="form-content">
                <form onsubmit="executeSearch(event, 'partes')">
                    <div class="form-grid">
                        <div class="form-group">
                            <label>NOMBRES Y APELLIDOS / RAZÓN SOCIAL</label>
                            <input type="text" placeholder="Ej: Andrés Supo Quispe" required>
                        </div>
                        <div class="form-group">
                            <label>DOCUMENTO DE IDENTIDAD (DNI / RUC)</label>
                            <input type="text" placeholder="Ej: 02167445">
                        </div>
                    </div>

                    <!-- CAPTCHA INTERACTIVO -->
                    <div class="captcha-container">
                        <div class="captcha-code-canvas" id="captcha-code-2">X4P7L</div>
                        <i class="fa-solid fa-rotate-right captcha-refresh" onclick="generateCaptcha(2)"></i>
                        <input type="text" id="captcha-user-2" placeholder="Ingrese el código" style="padding: 8px 12px; border: 1px solid #cbd5e1; border-radius: 6px; width: 140px;" required>
                    </div>

                    <button type="submit" class="btn-submit"><i class="fa-solid fa-user-check"></i> Buscar por Partes</button>
                </form>
            </div>
        </section>

        <!-- VISTA DETALLADA DEL EXPEDIENTE POSTERIOR A LA BÚSQUEDA -->
        <div id="expediente-view">
            
            <div class="card-header-exp">
                <span><i class="fa-solid fa-file-contract"></i> DATOS GENERALES: N° 00174-2019-0-2111-JR-LA-02</span>
                <span class="badge-status">EN TRÁMITE</span>
            </div>
            <div class="data-card-body">
                <table class="table-custom">
                    <tr><td class="td-label">Órgano Jurisdiccional:</td><td>Juzgado de Trabajo - Zona Norte (Juliaca)</td></tr>
                    <tr><td class="td-label">Juez / Especialista:</td><td>Gonzalo Víctor Huamán Romero / Rosario Carlos Villán</td></tr>
                    <tr><td class="td-label">Materia / Proceso:</td><td>Desnaturalización de Contrato / Proceso Ordinario Laboral</td></tr>
                    <tr><td class="td-label">Demandante:</td><td>Andrés Leonidas Supo Quispe (DNI: 02167445)</td></tr>
                    <tr><td class="td-label">Demandado:</td><td>Seguro Social de Salud - EsSalud (Red Asistencial Juliaca)</td></tr>
                    <tr><td class="td-label">Pretensión:</td><td>Inclusión en planillas a plazo indeterminado como Almacenero desde el 01/12/1996.</td></tr>
                </table>
            </div>

            <!-- LÍNEA DE TIEMPO DINÁMICA -->
            <div class="timeline-box">
                <div class="section-title-main" style="font-size:1.05rem;"><i class="fa-solid fa-timeline" style="color:var(--magenta-primary)"></i> Línea de Tiempo Procesal</div>
                <div class="timeline-steps">
                    <div class="t-step completed">
                        <div class="t-icon"><i class="fa-solid fa-check"></i></div>
                        <div style="font-weight:700; font-size:0.8rem;">Demanda</div>
                        <div style="font-size:0.72rem; color:#64748b;">26/06/2019</div>
                    </div>
                    <div class="t-step completed">
                        <div class="t-icon"><i class="fa-solid fa-check"></i></div>
                        <div style="font-weight:700; font-size:0.8rem;">Admisibilidad</div>
                        <div style="font-size:0.72rem; color:#64748b;">28/08/2019</div>
                    </div>
                    <div class="t-step active">
                        <div class="t-icon"><i class="fa-solid fa-pen-to-square"></i></div>
                        <div style="font-weight:700; font-size:0.8rem;">Contestación</div>
                        <div style="font-size:0.72rem; color:#64748b;">25/09/2019</div>
                    </div>
                    <div class="t-step">
                        <div class="t-icon">4</div>
                        <div style="font-weight:700; font-size:0.8rem;">Audiencia</div>
                        <div style="font-size:0.72rem; color:#64748b;">Pendiente</div>
                    </div>
                    <div class="t-step">
                        <div class="t-icon">5</div>
                        <div style="font-weight:700; font-size:0.8rem;">Sentencia</div>
                        <div style="font-size:0.72rem; color:#64748b;">Pendiente</div>
                    </div>
                </div>
            </div>

            <!-- INTEROPERABILIDAD DE ENTES -->
            <div class="section-title-main" style="font-size:1.05rem;"><i class="fa-solid fa-network-wired" style="color:var(--magenta-primary)"></i> Interoperabilidad con Entes Públicos (PISDP)</div>
            <div class="entes-grid">
                <div class="ente-card" onclick="openEnte('RENIEC')">
                    <div class="ente-avatar"><i class="fa-solid fa-id-card"></i></div>
                    <div style="font-weight:700; font-size:0.9rem;">RENIEC</div>
                    <div style="font-size:0.75rem; color:#64748b;">Ficha de Identidad C4</div>
                </div>
                <div class="ente-card" onclick="openEnte('MIGRACIONES')">
                    <div class="ente-avatar"><i class="fa-solid fa-plane"></i></div>
                    <div style="font-weight:700; font-size:0.9rem;">MIGRACIONES</div>
                    <div style="font-size:0.75rem; color:#64748b;">Movimiento Migratorio</div>
                </div>
                <div class="ente-card" onclick="openEnte('PNP')">
                    <div class="ente-avatar"><i class="fa-solid fa-user-shield"></i></div>
                    <div style="font-weight:700; font-size:0.9rem;">PNP</div>
                    <div style="font-size:0.75rem; color:#64748b;">Requisitorias Policiales</div>
                </div>
                <div class="ente-card" onclick="openEnte('INPE')">
                    <div class="ente-avatar"><i class="fa-solid fa-gavel"></i></div>
                    <div style="font-weight:700; font-size:0.9rem;">INPE</div>
                    <div style="font-size:0.75rem; color:#64748b;">Antecedentes Penales</div>
                </div>
            </div>

            <!-- TABLA DE DOCUMENTOS -->
            <div class="section-title-main" style="font-size:1.05rem; margin-top:20px;"><i class="fa-solid fa-folder-open" style="color:var(--magenta-primary)"></i> Resoluciones y Actuados Procesales</div>
            <table class="docs-table">
                <thead>
                    <tr>
                        <th>Fecha</th>
                        <th>Acto Procesal</th>
                        <th>Descripción Resumida</th>
                        <th>Documento</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>25/09/2019</td>
                        <td>Escrito N° 01</td>
                        <td>Contestación de la demanda por parte de EsSalud solicitando infundada.</td>
                        <td><button class="btn-pdf"><i class="fa-solid fa-file-pdf"></i> Ver Escrito</button></td>
                    </tr>
                    <tr>
                        <td>28/08/2019</td>
                        <td>Resolución N° 02</td>
                        <td>Admitir a trámite en la vía Ordinaria Laboral y dar traslado a EsSalud.</td>
                        <td><button class="btn-pdf"><i class="fa-solid fa-file-pdf"></i> Ver Res. 02</button></td>
                    </tr>
                    <tr>
                        <td>13/08/2019</td>
                        <td>Resolución N° 01</td>
                        <td>Admisibilidad provisional con plazo de 3 días para aclaración de partes.</td>
                        <td><button class="btn-pdf"><i class="fa-solid fa-file-pdf"></i> Ver Res. 01</button></td>
                    </tr>
                </tbody>
            </table>

        </div>

    </main>

    <!-- MODAL DE CARGA Y PROTECCIÓN DE DATOS (MINJUSDH) -->
    <div id="modal-data-protection" class="modal-overlay">
        <div class="modal-card">
            <button class="close-btn" onclick="closeDataModal()">&times;</button>
            <div style="color:var(--magenta-primary); font-weight:700; font-size:1.1rem; margin-bottom:12px;">
                <i class="fa-solid fa-shield-cat"></i> Medida de Protección de Datos Personales
            </div>
            <div style="font-size:0.85rem; color:#475569; line-height:1.6; margin-bottom:20px;">
                A partir de la fecha, se ha incluido un nuevo campo como medida técnica de protección, para que solo las partes puedan acceder a sus expedientes; a requerimiento de la Autoridad Nacional de Protección de Datos Personales y la Dirección de Fiscalización e Instrucción del Ministerio de Justicia y Derechos Humanos - MINJUSDH. Al amparo de la Ley N° 29733, Ley de Protección de Datos Personales.
            </div>
            <div style="text-align: right;">
                <button class="btn-submit" onclick="confirmDataProtection()">Aceptar y Ver Expediente</button>
            </div>
        </div>
    </div>

    <!-- MODAL DE CONSULTA DE ENTES -->
    <div id="ente-modal" class="modal-overlay">
        <div class="modal-card">
            <button class="close-btn" onclick="closeEnteModal()">&times;</button>
            <div id="ente-modal-title" style="color:var(--magenta-primary); font-weight:700; font-size:1.1rem; margin-bottom:15px;"></div>
            <div id="ente-modal-body" style="font-size:0.85rem; color:#475569;"></div>
        </div>
    </div>

    <footer>
        Portal del Expediente Electrónico © 2026 | Gobierno Digital y Derecho Informático
    </footer>

    <!-- LÓGICA JAVASCRIPT -->
    <script>
        // Carga inicial (Splash Screen)
        window.addEventListener('DOMContentLoaded', () => {
            setTimeout(() => {
                const splash = document.getElementById('splash-screen');
                splash.style.opacity = '0';
                splash.style.visibility = 'hidden';
            }, 2000);
            generateCaptcha(1);
            generateCaptcha(2);
        });

        // Reloj y Temporizador
        function updateClock() {
            const now = new Date();
            document.getElementById('clock-display').textContent = 
                `${String(now.getHours()).padStart(2, '0')}:${String(now.getMinutes()).padStart(2, '0')}:${String(now.getSeconds()).padStart(2, '0')}`;
        }
        setInterval(updateClock, 1000);
        updateClock();

        let timeLeft = 7 * 60;
        setInterval(() => {
            const minutes = Math.floor(timeLeft / 60);
            const seconds = timeLeft % 60;
            document.getElementById('timer-display').textContent = 
                `${String(minutes).padStart(2, '0')}:${String(seconds).padStart(2, '0')}`;
            if (timeLeft > 0) timeLeft--;
        }, 1000);

        // Generador de Captchas
        let currentCaptchas = {};
        function generateCaptcha(num) {
            const chars = "ABCDEFGHJKLMNPQRSTUVWXYZ23456789";
            let code = "";
            for (let i = 0; i < 5; i++) {
                code += chars.charAt(Math.floor(Math.random() * chars.length));
            }
            currentCaptchas[num] = code;
            document.getElementById(`captcha-code-${num}`).textContent = code;
        }

        function showInfo(title, text) {
            const infoBox = document.getElementById('info-box');
            document.getElementById('info-title').textContent = title;
            document.getElementById('info-text').textContent = text;
            infoBox.style.display = 'block';
        }

        function scrollToSearch() {
            document.getElementById('search-section').scrollIntoView({ behavior: 'smooth' });
        }

        function switchFilter(type) {
            document.querySelectorAll('.tab-btn').forEach(btn => btn.classList.remove('active'));
            document.querySelectorAll('.form-content').forEach(form => form.classList.remove('active'));
            if (type === 'numero') {
                event.target.classList.add('active');
                document.getElementById('filter-numero').classList.add('active');
            } else {
                event.target.classList.add('active');
                document.getElementById('filter-partes').classList.add('active');
            }
        }

        // Ejecutar Búsqueda con Validación de Captcha
        function executeSearch(event, filterType) {
            event.preventDefault();
            const num = filterType === 'code' ? 1 : 2;
            const userInput = document.getElementById(`captcha-user-${num}`).value.trim().toUpperCase();

            if (userInput !== currentCaptchas[num]) {
                alert("El código CAPTCHA ingresado es incorrecto. Por favor verifique e intente nuevamente.");
                generateCaptcha(num);
                document.getElementById(`captcha-user-${num}`).value = "";
                return;
            }

            // Mostrar el modal de carga/protección de datos
            document.getElementById('modal-data-protection').style.display = 'flex';
        }

        function closeDataModal() {
            document.getElementById('modal-data-protection').style.display = 'none';
        }

        function confirmDataProtection() {
            document.getElementById('modal-data-protection').style.display = 'none';
            document.getElementById('expediente-view').style.display = 'block';
            document.getElementById('expediente-view').scrollIntoView({ behavior: 'smooth' });
        }

        // Consultas simuladas de Entes Públicos
        function openEnte(ente) {
            const title = document.getElementById('ente-modal-title');
            const body = document.getElementById('ente-modal-body');

            if (ente === 'RENIEC') {
                title.innerHTML = '<i class="fa-solid fa-id-card"></i> RENIEC - Consulta de Identidad';
                body.innerHTML = `
                    <div style="display:flex; gap:15px; align-items:center;">
                        <div style="width:80px; height:100px; background:#e2e8f0; border-radius:6px; display:flex; align-items:center; justify-content:center; color:#94a3b8; font-size:0.75rem; text-align:center;">FOTO RENIEC</div>
                        <div>
                            <p><strong>DNI:</strong> 02167445</p>
                            <p><strong>Nombres:</strong> Andrés Leonidas Supo Quispe</p>
                            <p><strong>Estado Civil:</strong> Soltero</p>
                            <p><strong>Dirección:</strong> Av. Manco Cápac N° 964, Juliaca</p>
                            <p><strong>Ficha C4:</strong> Verificada y Emitida</p>
                        </div>
                    </div>`;
            } else if (ente === 'MIGRACIONES') {
                title.innerHTML = '<i class="fa-solid fa-plane"></i> MIGRACIONES - Control Pasajeros';
                body.innerHTML = `
                    <p><strong>Ciudadano:</strong> Andrés Leonidas Supo Quispe</p>
                    <p><strong>Alerta de Impedimento de Salida:</strong> NO REGISTRA</p>
                    <p><strong>Movimiento Migratorio:</strong> Sin salidas recientes registradas.</p>`;
            } else if (ente === 'PNP') {
                title.innerHTML = '<i class="fa-solid fa-user-shield"></i> PNP - Antecedentes Policiales';
                body.innerHTML = `
                    <p><strong>Sujeto:</strong> Andrés Leonidas Supo Quispe (DNI: 02167445)</p>
                    <p><strong>Antecedentes Policiales:</strong> SIN ANTECEDENTES</p>
                    <p><strong>Requisitorias (ESINPOL):</strong> Ninguna Orden de Captura Vigente</p>`;
            } else if (ente === 'INPE') {
                title.innerHTML = '<i class="fa-solid fa-gavel"></i> INPE - Antecedentes Penales';
                body.innerHTML = `
                    <p><strong>Evaluado:</strong> Andrés Leonidas Supo Quispe</p>
                    <p><strong>Antecedentes Penales:</strong> NO REGISTRA</p>
                    <p><strong>Condición Legal:</strong> Libre</p>`;
            }
            document.getElementById('ente-modal').style.display = 'flex';
        }

        function closeEnteModal() {
            document.getElementById('ente-modal').style.display = 'none';
        }
    </script>
</body>
</html>
