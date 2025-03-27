<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Navegador Moderno</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.4/css/all.min.css">
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>
    <style>
        * {
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', sans-serif;
            margin: 0;
            padding: 20px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .search-container {
            width: 95%;
            max-width: 800px;
            margin: 20px 0;
            position: relative;
        }

        .search-box {
            display: flex;
            gap: 10px;
            position: relative;
        }

        #searchInput {
            flex: 1;
            padding: 18px 25px 18px 60px;
            border: none;
            border-radius: 30px;
            background: rgba(255, 255, 255, 0.95);
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
            font-size: 16px;
            transition: all 0.3s ease;
        }

        .search-icon-container {
            position: absolute;
            left: 20px;
            top: 50%;
            transform: translateY(-50%);
            width: 40px;
            height: 40px;
            display: flex;
            justify-content: center;
            align-items: center;
            pointer-events: none;
        }

        .water-ring {
            position: absolute;
            width: 130%;
            height: 130%;
            border: 2px solid rgba(74, 84, 225, 0.2);
            border-radius: 50%;
            animation: waterFlow 3s infinite ease-in-out;
        }

        .water-ring:nth-child(2) {
            animation-delay: -1s;
            width: 160%;
            height: 160%;
            border-color: rgba(21, 161, 255, 0.15);
        }

        @keyframes waterFlow {
            0% {
                transform: scale(0.9) translateX(-3px);
                opacity: 0.8;
            }
            50% {
                transform: scale(1.1) translateX(3px);
                opacity: 0.4;
            }
            100% {
                transform: scale(0.9) translateX(-3px);
                opacity: 0.8;
            }
        }

        .search-icon {
            color: #4a54e1;
            font-size: 20px;
            position: relative;
            z-index: 2;
            transition: all 0.3s ease;
        }

        #searchInput:focus {
            outline: none;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.2);
            transform: scale(1.02);
        }

        #searchInput:focus ~ .search-icon-container .search-icon {
            transform: scale(1.1);
            color: #15a1ff;
        }

        #searchInput:focus ~ .search-icon-container .water-ring {
            animation-duration: 2s;
            border-color: rgba(21, 161, 255, 0.3);
        }

        #searchButton {
            padding: 15px 25px;
            border: none;
            border-radius: 30px;
            background: linear-gradient(45deg, #4a54e1, #15a1ff);
            color: white;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
        }

        #searchButton:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(0, 0, 0, 0.2);
            background: linear-gradient(45deg, #15a1ff, #4a54e1);
        }

        #engineOptionsContainer {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%) scale(0.95);
            background: rgba(255, 255, 255, 0.98);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 20px;
            width: 90%;
            max-width: 400px;
            opacity: 0;
            visibility: hidden;
            transition: all 0.3s cubic-bezier(0.68, -0.55, 0.27, 1.55);
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.15);
        }

        #engineOptionsContainer.show {
            opacity: 1;
            visibility: visible;
            transform: translate(-50%, -50%) scale(1);
        }

        .search-engine-option {
            display: flex;
            align-items: center;
            padding: 15px;
            margin: 10px 0;
            border-radius: 15px;
            background: white;
            cursor: pointer;
            transition: all 0.2s ease;
            border: 1px solid rgba(0, 0, 0, 0.05);
        }

        .search-engine-option:hover {
            transform: translateX(10px);
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
            background: linear-gradient(45deg, #f8f9fa, #ffffff);
        }

        .search-engine-option img {
            width: 30px;
            height: 30px;
            margin-right: 15px;
            border-radius: 50%;
        }

        #changeEngineButton {
            margin-top: 15px;
            padding: 12px 25px;
            border: none;
            border-radius: 25px;
            background: rgba(255, 255, 255, 0.9);
            color: #4a54e1;
            cursor: pointer;
            transition: all 0.3s ease;
            font-weight: 500;
            backdrop-filter: blur(5px);
        }

        #changeEngineButton:hover {
            background: rgba(255, 255, 255, 1);
            transform: translateY(-2px);
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
        }

        .notification {
            position: fixed;
            top: 50px;
            left: 50%;
            transform: translateX(-50%);
            background: rgba(255, 255, 255, 0.95);
            padding: 10px 20px;
            border-radius: 25px;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
            opacity: 0;
            visibility: hidden;
            transition: all 0.3s ease;
            font-size: 14px;
            max-width: 80%;
            white-space: nowrap;
        }

        .notification.show {
            opacity: 1;
            visibility: visible;
            top: 60px;
        }

        @media (max-width: 768px) {
            body {
                padding: 10px;
                min-height: calc(100vh - env(safe-area-inset-top) - env(safe-area-inset-bottom));
            }

            .search-container {
                max-width: 100%;
                margin: 10px 0;
            }

            #searchInput {
                padding: 14px 20px 14px 50px;
                font-size: 14px;
            }

            .search-icon-container {
                left: 15px;
                width: 35px;
                height: 35px;
            }

            .search-icon {
                font-size: 16px;
            }

            #searchButton {
                padding: 12px 20px;
            }

            #changeEngineButton {
                width: 100%;
                margin-top: 10px;
                padding: 10px 15px;
                font-size: 14px;
            }
        }
    </style>
</head>
<body>
    <div class="search-container">
        <div class="search-box">
            <div class="search-icon-container">
                <div class="water-ring"></div>
                <div class="water-ring"></div>
                <i class="fas fa-search search-icon"></i>
            </div>
            <input type="text" id="searchInput" placeholder="Buscar en la web o ingresar URL">
            <button id="searchButton" type="button">
                <i class="fas fa-search"></i>
            </button>
        </div>
    </div>

    <button id="changeEngineButton" type="button">
        <i class="fas fa-cog"></i> Cambiar Motor
    </button>

    <div id="engineOptionsContainer">
        <div class="search-engine-option" data-engine="Google">
            <img src="https://www.google.com/favicon.ico" alt="Google">
            Google
        </div>
        <div class="search-engine-option" data-engine="Bing">
            <img src="https://www.bing.com/sa/simg/bing_p_rr_teal_min.ico" alt="Bing">
            Bing
        </div>
        <div class="search-engine-option" data-engine="DuckDuckGo">
            <img src="https://duckduckgo.com/favicon.ico" alt="DuckDuckGo">
            DuckDuckGo
        </div>
        <div class="search-engine-option" data-engine="Yahoo">
            <img src="https://s.yimg.com/rz/p/yahoo_frontpage_en-US_s_f_p_bestfit_frontpage_2x.png" alt="Yahoo">
            Yahoo
        </div>
    </div>

    <div class="notification" id="notification"></div>

    <script>
        $(document).ready(function() {
            let currentEngine = localStorage.getItem('searchEngine') || 'Google';
            
            function showNotification(text) {
                const notification = $('#notification');
                notification.text(text).addClass('show');
                setTimeout(() => notification.removeClass('show'), 2000);
            }

            function search(query) {
                try {
                    new URL(query);
                    window.location.href = query.startsWith('http') ? query : `https://${query}`;
                } catch {
                    const engines = {
                        Google: `https://www.google.com/search?q=${encodeURIComponent(query)}`,
                        Bing: `https://www.bing.com/search?q=${encodeURIComponent(query)}`,
                        DuckDuckGo: `https://duckduckgo.com/?q=${encodeURIComponent(query)}`,
                        Yahoo: `https://search.yahoo.com/search?p=${encodeURIComponent(query)}`
                    };
                    window.open(engines[currentEngine], '_self');
                }
            }

            $('#searchButton').on('click', () => {
                const query = $('#searchInput').val().trim();
                if (query) search(query);
            });

            $('#searchInput').on('keypress', (e) => {
                if (e.key === 'Enter') {
                    const query = $('#searchInput').val().trim();
                    if (query) search(query);
                }
            });

            $('#changeEngineButton').click(() => {
                $('#engineOptionsContainer').toggleClass('show');
            });

            $('.search-engine-option').click(function() {
                currentEngine = $(this).data('engine');
                localStorage.setItem('searchEngine', currentEngine);
                $('#engineOptionsContainer').removeClass('show');
                showNotification(`Motor actual: ${currentEngine}`);
                $('#searchInput').focus();
            });

            $(document).mouseup(e => {
                if (!$('#engineOptionsContainer').is(e.target) && 
                    $('#engineOptionsContainer').has(e.target).length === 0) {
                    $('#engineOptionsContainer').removeClass('show');
                }
            });
        });
    </script>
</body>
</html>



<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NovaCore - Menú Inteligente</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.4/css/all.min.css">
    <style>
        :root {
            --color1: #667eea;
            --color2: #764ba2;
            --nav-bg: #2c3e50;
            --text-color: #ecf0f1;
            --menu-item-gap: 1.5rem;
        }

        body {
            min-height: 100vh;
            background: linear-gradient(135deg, var(--color1), var(--color2));
            transition: background 0.5s ease;
            font-family: 'Segoe UI', sans-serif;
            padding-top: 80px;
        }

        .navbar-custom {
            background-color: var(--nav-bg);
            padding: 12px 0;
            position: fixed;
            top: 0;
            width: 100%;
            z-index: 1030;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
            border-radius: 0 0 20px 20px;
        }

        .nav-link {
            color: var(--text-color) !important;
            margin: 0 var(--menu-item-gap);
            transition: all 0.3s ease;
            padding: 8px 25px !important;
            border-radius: 30px;
            position: relative;
            overflow: hidden;
            border: 2px solid transparent;
        }

        .nav-link::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(255, 255, 255, 0.1);
            transform: scaleX(0);
            transform-origin: right;
            transition: transform 0.4s cubic-bezier(0.4, 0, 0.2, 1);
            z-index: -1;
            border-radius: 25px;
        }

        .nav-link:hover::before {
            transform: scaleX(1);
            transform-origin: left;
        }

        .nav-link.active {
            color: #ffffff !important;
            font-weight: 600;
            background: linear-gradient(45deg, transparent, rgba(255, 255, 255, 0.15));
            border: 2px solid rgba(255, 255, 255, 0.2);
        }

        .btn-personalizar {
            background: linear-gradient(45deg, var(--color1), var(--color2));
            color: var(--text-color) !important;
            border-radius: 30px;
            padding: 8px 25px !important;
            margin-left: var(--menu-item-gap);
            transition: all 0.3s ease;
            border: none;
            position: relative;
            overflow: hidden;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
        }

        .btn-personalizar::after {
            content: '🎨';
            position: absolute;
            right: -20px;
            opacity: 0;
            transition: all 0.3s ease;
        }

        .btn-personalizar:hover {
            padding-right: 45px !important;
            transform: translateY(-2px);
        }

        .btn-personalizar:hover::after {
            right: 15px;
            opacity: 1;
        }

        .panel-backdrop {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0, 0, 0, 0.7);
            backdrop-filter: blur(12px);
            opacity: 0;
            pointer-events: none;
            transition: opacity 0.4s cubic-bezier(0.4, 0, 0.2, 1);
            z-index: 1040;
        }

        .custom-panel {
            background: rgba(255, 255, 255, 0.98);
            border-radius: 20px;
            padding: 2rem;
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.3);
            max-width: 450px;
            opacity: 0;
            transform: translate(-50%, -45%) scale(0.95);
            transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
            position: fixed;
            top: 50%;
            left: 50%;
            z-index: 1050;
            pointer-events: none;
        }

        .custom-panel.active {
            opacity: 1;
            transform: translate(-50%, -50%) scale(1);
            pointer-events: auto;
        }

        .color-option {
            width: 50px;
            height: 50px;
            border-radius: 15px;
            transition: all 0.3s ease;
            transform: scale(1);
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
            cursor: pointer;
            border: 2px solid transparent;
            background: linear-gradient(45deg, var(--c1), var(--c2));
        }

        .color-option.active {
            transform: scale(1.1);
            box-shadow: 0 0 0 3px var(--color1), 0 8px 25px rgba(0, 0, 0, 0.3);
        }

        .panel-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1.5rem;
        }

        .theme-section {
            margin-bottom: 2rem;
        }

        .theme-title {
            color: #2c3e50;
            font-size: 1.1rem;
            font-weight: 600;
            margin-bottom: 1rem;
            padding-bottom: 0.5rem;
            border-bottom: 2px solid #eee;
        }

        .color-label {
            font-size: 0.75rem;
            color: #666;
            text-align: center;
            margin-top: 0.5rem;
        }

        .custom-color-picker {
            display: flex;
            gap: 1rem;
            justify-content: center;
            align-items: center;
        }

        .color-input-group {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 0.5rem;
        }

        .color-input-label {
            font-size: 0.85rem;
            color: #444;
            font-weight: 500;
        }

        .btn-restore {
            background: #f8f9fa;
            color: #666;
            border: 1px solid #ddd;
            transition: all 0.3s ease;
        }

        .btn-restore:hover {
            background: #e9ecef;
            color: #444;
        }

        .preset-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 1rem;
            margin-bottom: 1.5rem;
        }

        @media (max-width: 991px) {
            body {
                padding-top: 60px;
            }
            
            .navbar-custom {
                border-radius: 0 0 15px 15px;
            }
            
            .color-option {
                width: 40px;
                height: 40px;
                border-radius: 12px;
            }
            
            .nav-link {
                margin: 5px 0;
                text-align: center;
            }
            
            .custom-panel {
                width: 90%;
                padding: 1.5rem;
            }
        }

        @keyframes slideDown {
            from { transform: translateY(-20px); opacity: 0; }
            to { transform: translateY(0); opacity: 1; }
        }
    </style>
</head>
<body>

<nav class="navbar navbar-expand-lg navbar-custom fixed-top">
    <div class="container">
        <a class="navbar-brand text-white fw-bold" href="#">NovaCore</a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#menuPrincipal">
            <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="menuPrincipal">
            <ul class="navbar-nav ms-auto align-items-lg-center">
                <li class="nav-item">
                    <a class="nav-link active" href="#">Inicio</a>
                </li>
                <li class="nav-item">
                    <a class="nav-link" href="#">Servicios</a>
                </li>
                <li class="nav-item">
                    <a class="nav-link" href="#">Portafolio</a>
                </li>
                <li class="nav-item">
                    <a class="nav-link" href="#">Contacto</a>
                </li>
                <li class="nav-item">
                    <button class="btn-personalizar nav-link">
                        Personalizar
                    </button>
                </li>
            </ul>
        </div>
    </div>
</nav>

<div class="panel-backdrop"></div>
<div class="custom-panel">
    <div class="panel-header">
        <h5>🎨 Personalización Avanzada</h5>
        <button class="btn-close btn btn-link text-secondary p-0">
            <i class="fas fa-times"></i>
        </button>
    </div>
    
    <div class="theme-section">
        <h6 class="theme-title">Temas Predefinidos</h6>
        <div class="preset-grid">
            <div class="d-flex flex-column align-items-center">
                <div class="color-option active" data-theme="classic" style="--c1: #667eea; --c2: #764ba2"></div>
                <span class="color-label">Clásico</span>
            </div>
            <div class="d-flex flex-column align-items-center">
                <div class="color-option" data-theme="warm" style="--c1: #ff6b6b; --c2: #ff8e53"></div>
                <span class="color-label">Cálido</span>
            </div>
            <div class="d-flex flex-column align-items-center">
                <div class="color-option" data-theme="fresh" style="--c1: #4ecdc4; --c2: #45b7af"></div>
                <span class="color-label">Fresco</span>
            </div>
            <div class="d-flex flex-column align-items-center">
                <div class="color-option" data-theme="pastel" style="--c1: #a18cd1; --c2: #fbc2eb"></div>
                <span class="color-label">Pastel</span>
            </div>
        </div>
    </div>

    <div class="theme-section">
        <h6 class="theme-title">Personalización Avanzada</h6>
        <div class="custom-color-picker">
            <div class="color-input-group">
                <label class="color-input-label">Primario</label>
                <input type="color" class="form-control form-control-color" id="color1">
            </div>
            <div class="color-input-group">
                <label class="color-input-label">Secundario</label>
                <input type="color" class="form-control form-control-color" id="color2">
            </div>
        </div>
    </div>

    <div class="d-grid gap-2">
        <button class="btn-accept btn btn-primary w-100 py-2 fw-bold" data-action="apply">
            <i class="fas fa-check-circle me-2"></i>Aplicar Cambios
        </button>
        <button class="btn-restore btn w-100 py-2" data-action="reset">
            <i class="fas fa-undo me-2"></i>Restablecer Valores
        </button>
    </div>
</div>

<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
<script>
document.addEventListener('DOMContentLoaded', () => {
    const panel = document.querySelector('.custom-panel');
    const backdrop = document.querySelector('.panel-backdrop');
    const personalizarBtn = document.querySelector('.btn-personalizar');
    const navbar = document.querySelector('.navbar-custom');
    
    const colorPresets = [
        { theme: 'classic', c1: '#667eea', c2: '#764ba2' },
        { theme: 'warm', c1: '#ff6b6b', c2: '#ff8e53' },
        { theme: 'fresh', c1: '#4ecdc4', c2: '#45b7af' },
        { theme: 'pastel', c1: '#a18cd1', c2: '#fbc2eb' }
    ];
    
    const defaultColors = { color1: '#667eea', color2: '#764ba2' };
    let selectedColors = { ...defaultColors };

    // Funciones principales
    const updateBodyPadding = () => {
        const navbarHeight = navbar.offsetHeight;
        document.body.style.paddingTop = `${navbarHeight + 20}px`;
    };

    const loadSavedColors = () => {
        const saved = localStorage.getItem('themeSettings');
        if(saved) {
            const { color1, color2 } = JSON.parse(saved);
            selectedColors = { color1, color2 };
            applyColors(color1, color2);
            updateColorInputs(color1, color2);
            markActivePreset(color1, color2);
        }
    };

    const applyColors = (c1, c2) => {
        document.documentElement.style.setProperty('--color1', c1);
        document.documentElement.style.setProperty('--color2', c2);
        document.documentElement.style.setProperty('--nav-bg', darkenColor(c1, 35));
        showNotification('Tema actualizado correctamente');
        updateBodyPadding();
    };

    const darkenColor = (hex, percent) => {
        const num = parseInt(hex.replace('#',''), 16);
        const amt = Math.round(2.55 * percent);
        return `#${(num - amt).toString(16).padStart(6, '0')}`;
    };

    const updateColorInputs = (c1, c2) => {
        document.getElementById('color1').value = c1;
        document.getElementById('color2').value = c2;
    };

    const markActivePreset = (c1, c2) => {
        document.querySelectorAll('.color-option').forEach(option => {
            const theme = option.dataset.theme;
            const preset = colorPresets.find(p => p.theme === theme);
            option.classList.toggle('active', preset?.c1 === c1 && preset?.c2 === c2);
        });
    };

    const togglePanel = () => {
        panel.classList.toggle('active');
        backdrop.classList.toggle('active');
        if(window.innerWidth < 992) {
            new bootstrap.Collapse(document.getElementById('menuPrincipal')).hide();
        }
    };

    const restoreDefaults = () => {
        selectedColors = { ...defaultColors };
        applyColors(defaultColors.color1, defaultColors.color2);
        localStorage.removeItem('themeSettings');
        updateColorInputs(defaultColors.color1, defaultColors.color2);
        markActivePreset(defaultColors.color1, defaultColors.color2);
        showNotification('Valores restablecidos');
    };

    const showNotification = (message) => {
        const notification = document.createElement('div');
        notification.className = 'position-fixed bottom-0 end-0 m-3 p-3 bg-success text-white rounded-3';
        notification.style.zIndex = '1060';
        notification.textContent = message;
        document.body.appendChild(notification);
        
        setTimeout(() => {
            notification.remove();
        }, 2000);
    };

    // Event Listeners
    personalizarBtn.addEventListener('click', togglePanel);
    backdrop.addEventListener('click', togglePanel);
    document.querySelector('.btn-close').addEventListener('click', togglePanel);

    document.querySelectorAll('.color-option').forEach(option => {
        option.addEventListener('click', function() {
            const theme = this.dataset.theme;
            const preset = colorPresets.find(p => p.theme === theme);
            if(preset) {
                selectedColors = { color1: preset.c1, color2: preset.c2 };
                updateColorInputs(preset.c1, preset.c2);
                markActivePreset(preset.c1, preset.c2);
            }
        });
    });

    document.getElementById('color1').addEventListener('input', (e) => {
        selectedColors.color1 = e.target.value;
        markActivePreset(null, null);
    });

    document.getElementById('color2').addEventListener('input', (e) => {
        selectedColors.color2 = e.target.value;
        markActivePreset(null, null);
    });

    document.querySelector('[data-action="apply"]').addEventListener('click', () => {
        applyColors(selectedColors.color1, selectedColors.color2);
        localStorage.setItem('themeSettings', JSON.stringify(selectedColors));
        togglePanel();
    });

    document.querySelector('[data-action="reset"]').addEventListener('click', restoreDefaults);

    // Inicialización
    updateBodyPadding();
    window.addEventListener('resize', updateBodyPadding);
    loadSavedColors();
});
</script>
</body>
</html>






<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Accesos Directos</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background-color: #f0f2f5;
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            min-height: 100vh;
            display: flex;
            align-items: center;
        }

        .contenedor {
            width: 100%;
            max-width: 400px;
            margin: 0 auto;
            padding: 15px;
        }

        .botones-contenedor {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 10px;
        }

        .boton {
            background: white;
            border: none;
            border-radius: 12px;
            padding: 12px;
            cursor: pointer;
            transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1);
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
            text-align: center;
            text-decoration: none;
            display: block;
        }

        .boton:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
        }

        .boton:active {
            transform: translateY(0);
            box-shadow: 0 1px 4px rgba(0, 0, 0, 0.1);
        }

        .boton img {
            width: 30px;
            height: 30px;
            margin-bottom: 6px;
            object-fit: contain;
            pointer-events: none;
        }

        .boton span {
            display: block;
            font-size: 12px;
            color: #444;
            font-weight: 500;
            pointer-events: none;
        }

        /* Colores y estilos específicos */
        .noticias { background: #e8f5e9; }
        .facebook { background: #1877f2; }
        .youtube { background: #ff0000; }
        .wikipedia { background: #f8f9fa; }

        .facebook span,
        .youtube span { color: white; }

        @media (max-width: 480px) {
            .boton {
                padding: 10px;
                border-radius: 10px;
            }
            
            .boton img {
                width: 26px;
                height: 26px;
            }
            
            .boton span {
                font-size: 11px;
            }
        }
    </style>
</head>
<body>
    <div class="contenedor">
        <div class="botones-contenedor">
            <a href="https://elpais.com/hemeroteca/2025-03-08/" class="boton noticias" target="_blank" rel="noopener">
                <img src="https://cdn-icons-png.flaticon.com/512/21/21601.png" alt="Noticias" loading="lazy">
                <span>Noticias</span>
            </a>
            
            <a href="https://m.facebook.com/?locale=es_ES" class="boton facebook" target="_blank" rel="noopener">
                <img src="https://cdn-icons-png.flaticon.com/512/124/124010.png" alt="Facebook" loading="lazy">
                <span>Facebook</span>
            </a>
            
            <a href="https://www.youtube.com/" class="boton youtube" target="_blank" rel="noopener">
                <img src="https://cdn-icons-png.flaticon.com/512/1384/1384060.png" alt="YouTube" loading="lazy">
                <span>YouTube</span>
            </a>
            
            <a href="https://es.m.wikipedia.org/wiki/Wikipedia:Portada" class="boton wikipedia" target="_blank" rel="noopener">
                <img src="https://cdn-icons-png.flaticon.com/512/5968/5968870.png" alt="Wikipedia" loading="lazy">
                <span>Wikipedia</span>
            </a>
        </div>
    </div>
</body>
</html>


