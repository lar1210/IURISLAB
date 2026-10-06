<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Portal del Expediente Electrónico</title>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;500;700&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Roboto', sans-serif;
        }

        body {
            background-color: #ffffff;
            color: #333333;
            display: flex;
            flex-direction: column;
            min-height: 100vh;
        }

        /* -------------------------------------------------------------
           1. PANTALLA DE CARGA (SPLASH SCREEN)
        ------------------------------------------------------------- */
        #splash-screen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: #ffffff;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            z-index: 9999;
            transition: opacity 0.5s ease, visibility 0.5s ease;
        }

        .loader-title {
            color: #8B005B;
            font-size: 1.8rem;
            font-weight: 700;
            text-align: center;
            margin-bottom: 20px;
        }

        .spinner {
            border: 4px solid #f3f3f3;
            border-top: 4px solid #8B005B;
            border-radius: 50%;
            width: 50px;
            height: 50px;
            animation: spin 1s linear infinite;
            margin-bottom: 20px;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        /* Toast / Notificación Prototipo Académico */
        .academic-toast {
            background-color: #8B005B;
            color: #ffffff;
            padding: 12px 20px;
            border-radius: 8px;
            font-size: 0.85rem;
            text-align: center;
            box-shadow: 0 4px 12px rgba(0,0,0,0.15);
            max-width: 90%;
            animation: fadeIn 1s ease-in-out;
        }

        /* -------------------------------------------------------------
           2. ENCABEZADO Y MARCA SUPERIOR
        ------------------------------------------------------------- */
        .top-header {
            padding: 12px 5%;
            display: flex;
            justify-content: flex-end;
            align-items: center;
            background-color: #ffffff;
            border-bottom: 1px solid #f0f0f0;
        }

        .brand-title {
            color: #8B005B;
            font-size: 1.4rem;
            font-weight: 700;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            text-align: right;
        }

        /* -------------------------------------------------------------
           3. BARRA DE MENÚ HORIZONTAL (MAGENTA) Y WIDGETS
        ------------------------------------------------------------- */
        .navbar-magenta {
            background-color: #8B005B;
            color: #ffffff;
            padding: 0 5%;
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }

        .nav-menu {
            display: flex;
            list-style: none;
            flex-wrap: wrap;
        }

        .nav-menu li a {
            display: block;
            padding: 14px 16px;
            color: #ffffff;
            text-decoration: none;
            font-size: 0.9rem;
            font-weight: 500;
            transition: background 0.3s;
            cursor: pointer;
        }

        .nav-menu li a:hover, .nav-menu li a.active {
            background-color: #660046;
        }

        .btn-search-nav {
            background-color: #a8006e;
            font-weight: 700 !important;
            border-left: 1px solid #660046;
        }

        /* Reloj y Temporizador */
        .widgets-bar {
            display: flex;
            gap: 15px;
            background-color: #660046;
            padding: 6px 14px;
            border-radius: 4px;
            font-size: 0.8rem;
            font-weight: 500;
            margin: 6px 0;
        }

        /* -------------------------------------------------------------
           4. CONTENIDO PRINCIPAL Y MODALES
        ------------------------------------------------------------- */
        .main-container {
            max-width: 1100px;
            margin: 20px auto;
            padding: 0 20px;
            flex: 1;
            width: 100%;
        }

        /* Caja de Info Dinámica del Menú */
        .info-card {
            background-color: #fcf8fa;
            border-left: 4px solid #8B005B;
            padding: 15px 20px;
            margin-bottom: 20px;
            border-radius: 0 4px 4px 0;
            display: none;
        }

        .info-card h4 {
            color: #8B005B;
            margin-bottom: 5px;
        }

        /* Sección Búsqueda de Expediente */
        .search-section {
            border: 1px solid #e0e0e0;
            border-radius: 8px;
            padding: 25px;
            background-color: #ffffff;
            box-shadow: 0 2px 10px rgba(0,0,0,0.03);
        }

        .search-section h3 {
            color: #1a202c;
            margin-bottom: 15px;
            font-size: 1.15rem;
            border-bottom: 2px solid #8B005B;
            padding-bottom: 8px;
            display: inline-block;
        }

        /* Pestañas de Filtro */
        .filter-tabs {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
        }

        .tab-btn {
            padding: 10px 18px;
            border: 1px solid #cbd5e0;
            background-color: #f7fafc;
            cursor: pointer;
            font-weight: 500;
            border-radius: 4px;
            font-size: 0.88rem;
            transition: all 0.3s;
        }

        .tab-btn.active {
            background-color: #8B005B;
            color: #ffffff;
            border-color: #8B005B;
        }

        /* Formulario y Grids */
        .form-content {
            display: none;
        }

        .form-content.active {
            display: block;
        }

        .form-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
            gap: 15px;
            margin-bottom: 15px;
        }

        .form-group label {
            display: block;
            font-size: 0.8rem;
            font-weight: 700;
            color: #4a5568;
            margin-bottom: 5px;
        }

        .form-group input, .form-group select {
            width: 100%;
            padding: 9px 12px;
            border: 1px solid #cbd5e0;
            border-radius: 4px;
            font-size: 0.9rem;
        }

        /* Bloque CAPTCHA Simulado */
        .captcha-box {
            background-color: #f8f9fa;
            border: 1px solid #e2e8f0;
            padding: 12px 16px;
            border-radius: 6px;
            display: flex;
            align-items: center;
            gap: 12px;
            width: fit-content;
            margin-bottom: 20px;
        }

        .captcha-code {
            background-color: #e2e8f0;
            padding: 6px 12px;
            font-weight: 700;
            letter-spacing: 3px;
            color: #8B005B;
            user-select: none;
            border-radius: 4px;
        }

        .btn-submit {
            background-color: #8B005B;
            color: white;
            border: none;
            padding: 10px 24px;
            font-size: 0.9rem;
            font-weight: bold;
            border-radius: 4px;
            cursor: pointer;
            transition: background 0.3s;
        }

        .btn-submit:hover {
            background-color: #660046;
        }

        /* -------------------------------------------------------------
           5. PANTALLA DE CARGA Y POPUP DE PROTECCIÓN DE DATOS
        ------------------------------------------------------------- */
        #search-loading {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0,0,0,0.6);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 10000;
            display: none;
        }

        .data-modal {
            background-color: #ffffff;
            border-radius: 8px;
            max-width: 550px;
            width: 90%;
            padding: 24px;
            position: relative;
            box-shadow: 0 10px 25px rgba(0,0,0,0.3);
            animation: modalSlide 0.3s ease-out;
        }

        @keyframes modalSlide {
            from { transform: translateY(-20px); opacity: 0; }
            to { transform: translateY(0); opacity: 1; }
        }

        .close-btn {
            position: absolute;
            top: 12px;
            right: 16px;
            font-size: 1.4rem;
            font-weight: bold;
            color: #718096;
            cursor: pointer;
            border: none;
            background: none;
        }

        .close-btn:hover {
            color: #8B005B;
        }

        .modal-title {
            color: #8B005B;
            font-size: 1.1rem;
            font-weight: 700;
            margin-bottom: 12px;
        }

        .modal-body {
            font-size: 0.85rem;
            color: #4a5568;
            line-height: 1.6;
        }

        footer {
            background-color: #1a202c;
            color: #a0aec0;
            text-align: center;
            padding: 12px;
            font-size: 0.78rem;
            margin-top: auto;
        }

        /* Adaptabilidad Celular (Responsive) */
        @media (max-width: 768px) {
            .navbar-magenta {
                flex-direction: column;
                padding: 10px;
            }
            .nav-menu {
                width: 100%;
                justify-content: center;
            }
            .widgets-bar {
                width: 100%;
                justify-content: center;
            }
            .top-header {
                justify-content: center;
            }
            .brand-title {
                text-align: center;
                font-size: 1.1rem;
            }
        }
    </style>
</head>
<body>

    <!-- 1. CARGAPANTALLA INICIAL (SPLASH SCREEN) -->
    <div id="splash-screen">
        <div class="loader-title">Portal del Expediente Electrónico</div>
        <div class="spinner"></div>
        <div class="academic-toast">
            <strong>Aviso:</strong> Este sitio web es un prototipo académico desarrollado para la asignatura de <strong>Gobierno Digital y Derecho Informático</strong>.<br>
            Estudiante: <em>Sonia Pilar Condori Ruelas</em> | Docente: <em>Michael Espinoza Coila</em>
        </div>
    </div>

    <!-- 2. ENCABEZADO DERECHO SUPERIOR -->
    <header class="top-header">
        <div class="brand-title">Portal del Expediente Electrónico</div>
    </header>

    <!-- 3. BARRA DE MENÚ MAGENTA CON WIDGETS -->
    <nav class="navbar-magenta">
        <ul class="nav-menu">
            <li><a class="active" onclick="showInfo('inicio', 'Inicio', 'Bienvenido al Portal del Expediente Electrónico. Seleccione una opción del menú para interactuar con los módulos del sistema.')">Inicio</a></li>
            <li><a onclick="showInfo('mision', 'Misión Institucional', 'Garantizar el acceso transparente, rápido y digital a los procesos judiciales mediante la modernización del Expediente Judicial Electrónico (EJE).')">Misión</a></li>
            <li><a onclick="showInfo('vision', 'Visión Institucional', 'Ser una plataforma de justicia digital eficiente, confiable e interoperable al servicio de la ciudadanía y los operadores del derecho.')">Visión</a></li>
            <li><a onclick="showInfo('transparencia', 'Portal de Transparencia', 'Acceso libre a resoluciones, jurisprudencia y estadísticas judiciales conforme al principio de máxima divulgación pública.')">Transparencia</a></li>
            <li><a onclick="showInfo('contactanos', 'Contáctanos', 'Mesa de Ayuda Técnica - Atención al Ciudadano: Soporte EJE | Teléfono: (01) 410-0000 | Correo: soporte_eje@pj.gob.pe')">Contáctanos</a></li>
            <li><a class="btn-search-nav" onclick="scrollToSearch()">Búsqueda de Expediente</a></li>
        </ul>

        <!-- Reloj y Temporizador -->
        <div class="widgets-bar">
            <span>🕒 Hora: <strong id="clock-display">00:00:00</strong></span>
            <span>⏱️ Sesión: <strong id="timer-display">07:00</strong></span>
        </div>
    </nav>

    <!-- 4. CUERPO PRINCIPAL -->
    <main class="main-container">

        <!-- Caja de Información del Menú (Simulación de clicks) -->
        <div id="info-box" class="info-card">
            <h4 id="info-title">Inicio</h4>
            <p id="info-text" style="font-size: 0.88rem; color: #4a5568;"></p>
        </div>

        <!-- Módulo de Búsqueda de Expediente -->
        <section id="search-section" class="search-section">
            <h3>Búsqueda de Expediente</h3>
            
            <!-- Pestañas de Filtro -->
            <div class="filter-tabs">
                <button class="tab-btn active" onclick="switchFilter('numero')">Por Número de Expediente</button>
                <button class="tab-btn" onclick="switchFilter('partes')">Por Partes Procesales</button>
            </div>

            <!-- Filtro 1: Por Número de Expediente -->
            <div id="filter-numero" class="form-content active">
                <form onsubmit="executeSearch(event)">
                    <div class="form-grid">
                        <div class="form-group">
                            <label>CÓDIGO DE EXPEDIENTE</label>
                            <input type="text" placeholder="Ej: 00174-2019-0-2111-JR-LA-02" required>
                        </div>
                        <div class="form-group">
                            <label>DISTRITO JUDICIAL</label>
                            <select required>
                                <option value="">-- Seleccione --</option>
                                <option selected>PUNO</option>
                                <option>LIMA</option>
                            </select>
                        </div>
                    </div>

                    <!-- CAPTCHA -->
                    <div class="captcha-box">
                        <input type="checkbox" id="captcha1" required>
                        <label for="captcha1" style="font-size: 0.85rem;">No soy un robot</label>
                        <span class="captcha-code">EJE2026</span>
                    </div>

                    <button type="submit" class="btn-submit">Consultar Expediente</button>
                </form>
            </div>

            <!-- Filtro 2: Por Partes Procesales -->
            <div id="filter-partes" class="form-content">
                <form onsubmit="executeSearch(event)">
                    <div class="form-grid">
                        <div class="form-group">
                            <label>TIPO DE PERSONA</label>
                            <select>
                                <option>Persona Natural</option>
                                <option>Persona Jurídica</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label>NOMBRES / Razón Social</label>
                            <input type="text" placeholder="Ej: Andrés Supo Quispe" required>
                        </div>
                        <div class="form-group">
                            <label>DNI / RUC</label>
                            <input type="text" placeholder="Ej: 02167445">
                        </div>
                    </div>

                    <!-- CAPTCHA -->
                    <div class="captcha-box">
                        <input type="checkbox" id="captcha2" required>
                        <label for="captcha2" style="font-size: 0.85rem;">No soy un robot</label>
                        <span class="captcha-code">PJ9842</span>
                    </div>

                    <button type="submit" class="btn-submit">Buscar por Partes</button>
                </form>
            </div>

        </section>

    </main>

    <!-- 5. CARGAPANTALLA Y NOTIFICACIÓN POPUP DE PROTECCIÓN DE DATOS (MINJUSDH) -->
    <div id="search-loading">
        <div class="data-modal">
            <button class="close-btn" onclick="closeDataModal()">&times;</button>
            <div class="modal-title">Aviso de Protección de Datos Personales</div>
            <div class="modal-body">
                A partir de la fecha, se ha incluido un nuevo campo como medida técnica de protección, para que solo las partes puedan acceder a sus expedientes; a requerimiento de la Autoridad Nacional de Protección de Datos Personales y la Dirección de Fiscalización e Instrucción del Ministerio de Justicia y Derechos Humanos - MINJUSDH. Al amparo de la Ley N° 29733, Ley de Protección de Datos Personales.
            </div>
        </div>
    </div>

    <!-- PIE DE PÁGINA -->
    <footer>
        Portal del Expediente Electrónico © 2026 | Gobierno Digital y Derecho Informático
    </footer>

    <!-- LÓGICA JAVASCRIPT -->
    <script>
        // Ocultar pantalla de carga inicial a los 2.5 segundos
        window.addEventListener('DOMContentLoaded', () => {
            setTimeout(() => {
                const splash = document.getElementById('splash-screen');
                splash.style.opacity = '0';
                splash.style.visibility = 'hidden';
            }, 2500);
        });

        // Reloj en Tiempo Real
        function updateClock() {
            const now = new Date();
            const hours = String(now.getHours()).padStart(2, '0');
            const minutes = String(now.getMinutes()).padStart(2, '0');
            const seconds = String(now.getSeconds()).padStart(2, '0');
            document.getElementById('clock-display').textContent = `${hours}:${minutes}:${seconds}`;
        }
        setInterval(updateClock, 1000);
        updateClock();

        // Temporizador de 7 Minutos
        let timeLeft = 7 * 60;
        function updateTimer() {
            const minutes = Math.floor(timeLeft / 60);
            const seconds = timeLeft % 60;
            document.getElementById('timer-display').textContent = 
                `${String(minutes).padStart(2, '0')}:${String(seconds).padStart(2, '0')}`;
            if (timeLeft > 0) timeLeft--;
        }
        setInterval(updateTimer, 1000);

        // Mostrar información simulada al hacer click en el Menú
        function showInfo(id, title, text) {
            const infoBox = document.getElementById('info-box');
            document.getElementById('info-title').textContent = title;
            document.getElementById('info-text').textContent = text;
            infoBox.style.display = 'block';
        }

        function scrollToSearch() {
            document.getElementById('search-section').scrollIntoView({ behavior: 'smooth' });
        }

        // Alternar Filtros de Búsqueda
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

        // Simular Carga y Mostrar Popup de Protección de Datos
        function executeSearch(event) {
            event.preventDefault();
            const modal = document.getElementById('search-loading');
            modal.style.display = 'flex';
        }

        function closeDataModal() {
            document.getElementById('search-loading').style.display = 'none';
        }
    </script>
</body>
</html>
