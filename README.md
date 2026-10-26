<!DOCTYPE html>
<html lang="es" class="h-full bg-slate-900 text-slate-100">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Batec Mobility - Registro de Verificación RV-022 v3.0</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=JetBrains+Mono:wght@400;500&display=swap');
        body {
            font-family: 'Inter', sans-serif;
        }
        .code-font {
            font-family: 'JetBrains Mono', monospace;
        }
        /* Custom scrollbar for SAT environment */
        ::-webkit-scrollbar {
            width: 8px;
            height: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #0f172a;
        }
        ::-webkit-scrollbar-thumb {
            background: #334155;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #475569;
        }
    </style>
</head>
<body class="h-full flex flex-col bg-slate-950 text-slate-100 antialiased selection:bg-red-500 selection:text-white">

    <!-- TOP HEADER -->
    <header class="bg-slate-900 border-b border-slate-800 sticky top-0 z-30 shadow-lg">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-3">
            <div class="flex flex-wrap items-center justify-between gap-4">
                <!-- Logo & Title -->
                <div class="flex items-center space-x-3">
                    <div class="bg-gradient-to-tr from-red-600 to-red-500 p-2.5 rounded-xl shadow-md shadow-red-900/30">
                        <i class="fa-solid fa-wrench text-white text-xl"></i>
                    </div>
                    <div>
                        <div class="flex items-center space-x-2">
                            <h1 class="text-lg font-bold tracking-tight text-white">BATEC MOBILITY</h1>
                            <span class="bg-red-500/10 text-red-400 text-xs px-2 py-0.5 rounded border border-red-500/20 font-mono font-medium">SAT RV-022 v3.0</span>
                        </div>
                        <p class="text-xs text-slate-400">Registro de Verificación Técnica de Handbikes</p>
                    </div>
                </div>

                <!-- Global Progress Bar & Actions -->
                <div class="flex items-center space-x-4 flex-grow max-w-md">
                    <div class="w-full">
                        <div class="flex justify-between items-center text-xs mb-1">
                            <span class="text-slate-400 font-medium">Progreso Verificación:</span>
                            <span id="progress-text" class="font-bold text-red-400">0% (0/0)</span>
                        </div>
                        <div class="w-full bg-slate-800 h-2.5 rounded-full overflow-hidden border border-slate-700/50">
                            <div id="progress-bar" class="bg-gradient-to-r from-red-600 to-emerald-500 h-full w-0 transition-all duration-300"></div>
                        </div>
                    </div>
                </div>

                <!-- Global Quick Action Buttons -->
                <div class="flex items-center space-x-2">
                    <button onclick="markAllGlobal('OK')" class="px-3 py-1.5 bg-slate-800 hover:bg-slate-700 text-emerald-400 border border-emerald-500/30 rounded-lg text-xs font-semibold flex items-center space-x-1.5 transition">
                        <i class="fa-solid fa-check-double"></i>
                        <span class="hidden sm:inline">Todo OK</span>
                    </button>
                    <button onclick="resetAllChecklists()" class="px-3 py-1.5 bg-slate-800 hover:bg-slate-700 text-slate-400 border border-slate-700 rounded-lg text-xs font-semibold flex items-center space-x-1.5 transition">
                        <i class="fa-solid fa-rotate-right"></i>
                        <span class="hidden sm:inline">Reiniciar</span>
                    </button>
                    <button onclick="openFreshdeskModal()" class="px-3.5 py-1.5 bg-red-600 hover:bg-red-500 text-white rounded-lg text-xs font-bold shadow-md shadow-red-600/30 flex items-center space-x-2 transition transform active:scale-95">
                        <i class="fa-solid fa-code"></i>
                        <span>Copiar p/ Freshdesk</span>
                    </button>
                </div>
            </div>
        </div>

        <!-- NAVIGATION TABS -->
        <div class="bg-slate-900/80 border-t border-slate-800/80 backdrop-blur">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                <nav class="flex space-x-1 overflow-x-auto py-2 no-scrollbar" id="tab-nav">
                    <button onclick="switchTab('header-tab')" id="btn-header-tab" class="tab-btn active px-4 py-2 text-xs font-semibold rounded-lg flex items-center space-x-2 whitespace-nowrap transition bg-red-600/20 text-red-400 border border-red-500/30">
                        <i class="fa-solid fa-clipboard-list"></i>
                        <span>1. Datos Ticket y Parámetros</span>
                    </button>
                    <button onclick="switchTab('chassis-tab')" id="btn-chassis-tab" class="tab-btn px-4 py-2 text-xs font-semibold text-slate-400 hover:text-slate-200 hover:bg-slate-800 rounded-lg flex items-center space-x-2 whitespace-nowrap transition border border-transparent">
                        <i class="fa-solid fa-gears"></i>
                        <span>2. Chasis, Anclaje y Freno</span>
                    </button>
                    <button onclick="switchTab('electronics-tab')" id="btn-electronics-tab" class="tab-btn px-4 py-2 text-xs font-semibold text-slate-400 hover:text-slate-200 hover:bg-slate-800 rounded-lg flex items-center space-x-2 whitespace-nowrap transition border border-transparent">
                        <i class="fa-solid fa-bolt"></i>
                        <span>3. Electrónica y Consola</span>
                    </button>
                    <button onclick="switchTab('dynamic-tab')" id="btn-dynamic-tab" class="tab-btn px-4 py-2 text-xs font-semibold text-slate-400 hover:text-slate-200 hover:bg-slate-800 rounded-lg flex items-center space-x-2 whitespace-nowrap transition border border-transparent">
                        <i class="fa-solid fa-gauge-high"></i>
                        <span>4. Comprobación Dinámica y Híbridos</span>
                    </button>
                    <button onclick="switchTab('validation-tab')" id="btn-validation-tab" class="tab-btn px-4 py-2 text-xs font-semibold text-slate-400 hover:text-slate-200 hover:bg-slate-800 rounded-lg flex items-center space-x-2 whitespace-nowrap transition border border-transparent">
                        <i class="fa-solid fa-route"></i>
                        <span>5. Ruta Final y Validación</span>
                    </button>
                </nav>
            </div>
        </div>
    </header>

    <!-- MAIN CONTENT AREA -->
    <main class="flex-1 max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-6 space-y-6">

        <!-- TAB 1: DATOS CABECERA Y PARÁMETROS -->
        <div id="header-tab" class="tab-content space-y-6">
            <div class="bg-slate-900 border border-slate-800 rounded-xl p-5 shadow-sm space-y-4">
                <h2 class="text-sm font-bold text-red-400 uppercase tracking-wider flex items-center space-x-2 border-b border-slate-800 pb-3">
                    <i class="fa-solid fa-file-signature"></i>
                    <span>Información Registro de Verificación & Ticket Freshdesk</span>
                </h2>
                <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                    <div>
                        <label class="block text-xs font-medium text-slate-400 mb-1">Distribuidor</label>
                        <input type="text" id="distribuidor" placeholder="Ej: Mobility Spain S.L." class="w-full bg-slate-950 border border-slate-700 rounded-lg px-3 py-2 text-xs text-white focus:outline-none focus:border-red-500">
                    </div>
                    <div>
                        <label class="block text-xs font-medium text-slate-400 mb-1">Ticket Freshdesk #</label>
                        <input type="text" id="ticket_num" placeholder="Ej: 45892" class="w-full bg-slate-950 border border-slate-700 rounded-lg px-3 py-2 text-xs text-white focus:outline-none focus:border-red-500 font-mono">
                    </div>
                    <div>
                        <label class="block text-xs font-medium text-slate-400 mb-1">Fecha de Verificación</label>
                        <input type="date" id="fecha_registro" class="w-full bg-slate-950 border border-slate-700 rounded-lg px-3 py-2 text-xs text-white focus:outline-none focus:border-red-500">
                    </div>
                    <div class="md:col-span-3">
                        <label class="block text-xs font-medium text-slate-400 mb-1">Explicación del Ticket / Observaciones de Entrada</label>
                        <textarea id="observaciones" rows="2" placeholder="Motivo de la reparación o revisión periódica..." class="w-full bg-slate-950 border border-slate-700 rounded-lg px-3 py-2 text-xs text-white focus:outline-none focus:border-red-500"></textarea>
                    </div>
                </div>
            </div>

            <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
                <!-- Identificación & Partes Recibidas -->
                <div class="bg-slate-900 border border-slate-800 rounded-xl p-5 shadow-sm space-y-4">
                    <h2 class="text-sm font-bold text-slate-300 uppercase tracking-wider flex items-center space-x-2 border-b border-slate-800 pb-3">
                        <i class="fa-solid fa-box-open text-red-500"></i>
                        <span>Identificación de Handbike y Partes Recibidas</span>
                    </h2>
                    <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                        <div>
                            <label class="block text-xs font-medium text-slate-400 mb-1">Batec S/N</label>
                            <input type="text" id="batec_sn" placeholder="BAT-XXXXX" class="w-full bg-slate-950 border border-slate-700 rounded-lg px-3 py-2 text-xs text-white font-mono focus:border-red-500">
                        </div>
                        <div>
                            <label class="block text-xs font-medium text-slate-400 mb-1">Bastidor S/N</label>
                            <input type="text" id="bastidor_sn" placeholder="BAS-XXXXX" class="w-full bg-slate-950 border border-slate-700 rounded-lg px-3 py-2 text-xs text-white font-mono focus:border-red-500">
                        </div>
                    </div>
                    <div>
                        <span class="block text-xs font-medium text-slate-400 mb-2">Partes Recibidas en SAT:</span>
                        <div class="grid grid-cols-2 sm:grid-cols-4 gap-2">
                            <label class="flex items-center space-x-2 bg-slate-950 p-2 rounded-lg border border-slate-800 cursor-pointer">
                                <input type="checkbox" id="part_pesos" class="rounded border-slate-700 text-red-600 focus:ring-0">
                                <span class="text-xs text-slate-300">Pesos</span>
                            </label>
                            <label class="flex items-center space-x-2 bg-slate-950 p-2 rounded-lg border border-slate-800 cursor-pointer">
                                <input type="checkbox" id="part_cargador" class="rounded border-slate-700 text-red-600 focus:ring-0">
                                <span class="text-xs text-slate-300">Cargador</span>
                            </label>
                            <label class="flex items-center space-x-2 bg-slate-950 p-2 rounded-lg border border-slate-800 cursor-pointer">
                                <input type="checkbox" id="part_bateria" class="rounded border-slate-700 text-red-600 focus:ring-0">
                                <span class="text-xs text-slate-300">Batería</span>
                            </label>
                            <label class="flex items-center space-x-2 bg-slate-950 p-2 rounded-lg border border-slate-800 cursor-pointer">
                                <input type="checkbox" id="part_otros" class="rounded border-slate-700 text-red-600 focus:ring-0">
                                <span class="text-xs text-slate-300">Otros</span>
                            </label>
                        </div>
                    </div>
                </div>

                <!-- Telemetría Entrada / Salida -->
                <div class="bg-slate-900 border border-slate-800 rounded-xl p-5 shadow-sm space-y-4">
                    <h2 class="text-sm font-bold text-slate-300 uppercase tracking-wider flex items-center space-x-2 border-b border-slate-800 pb-3">
                        <i class="fa-solid fa-tachometer-alt text-red-500"></i>
                        <span>Métricas de Entrada / Salida</span>
                    </h2>
                    <div class="grid grid-cols-2 gap-4">
                        <div class="space-y-3 bg-slate-950/50 p-3 rounded-lg border border-slate-800">
                            <span class="text-xs font-bold text-slate-400 block border-b border-slate-800 pb-1">DATOS DE ENTRADA</span>
                            <div>
                                <label class="block text-[11px] text-slate-400 mb-0.5">Km / Millas Entrada</label>
                                <input type="number" step="0.1" id="km_entrada" placeholder="0.0" class="w-full bg-slate-950 border border-slate-700 rounded px-2.5 py-1.5 text-xs text-white font-mono">
                            </div>
                            <div>
                                <label class="block text-[11px] text-slate-400 mb-0.5">Km/h / MPH Entrada</label>
                                <input type="number" step="0.1" id="speed_entrada" placeholder="0.0" class="w-full bg-slate-950 border border-slate-700 rounded px-2.5 py-1.5 text-xs text-white font-mono">
                            </div>
                        </div>
                        <div class="space-y-3 bg-slate-950/50 p-3 rounded-lg border border-slate-800">
                            <span class="text-xs font-bold text-emerald-400 block border-b border-slate-800 pb-1">DATOS DE SALIDA</span>
                            <div>
                                <label class="block text-[11px] text-slate-400 mb-0.5">Km / Millas Salida</label>
                                <input type="number" step="0.1" id="km_salida" placeholder="0.0" class="w-full bg-slate-950 border border-slate-700 rounded px-2.5 py-1.5 text-xs text-white font-mono">
                            </div>
                            <div>
                                <label class="block text-[11px] text-slate-400 mb-0.5">Km/h / MPH Salida</label>
                                <input type="number" step="0.1" id="speed_salida" placeholder="0.0" class="w-full bg-slate-950 border border-slate-700 rounded px-2.5 py-1.5 text-xs text-white font-mono">
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Trazabilidad de Componentes & Alarmas -->
            <div class="bg-slate-900 border border-slate-800 rounded-xl p-5 shadow-sm space-y-4">
                <h2 class="text-sm font-bold text-slate-300 uppercase tracking-wider flex items-center space-x-2 border-b border-slate-800 pb-3">
                    <i class="fa-solid fa-microchip text-red-500"></i>
                    <span>Trazabilidad de Componentes & Alarmas</span>
                </h2>
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
                    <div>
                        <label class="block text-xs font-medium text-slate-400 mb-1">Controller / SW Versión (Original)</label>
                        <input type="text" id="controller_orig" placeholder="S/N u / v1.0" class="w-full bg-slate-950 border border-slate-700 rounded px-3 py-1.5 text-xs font-mono text-white">
                    </div>
                    <div>
                        <label class="block text-xs font-medium text-slate-400 mb-1">Controller / SW Versión (Spare/Recambio)</label>
                        <input type="text" id="controller_spare" placeholder="S/N repuesto" class="w-full bg-slate-950 border border-slate-700 rounded px-3 py-1.5 text-xs font-mono text-white">
                    </div>
                    <div>
                        <label class="block text-xs font-medium text-slate-400 mb-1">P Codificación / Doc #</label>
                        <input type="text" id="p_codificacion" placeholder="Doc #" class="w-full bg-slate-950 border border-slate-700 rounded px-3 py-1.5 text-xs font-mono text-white">
                    </div>
                    <div>
                        <label class="block text-xs font-medium text-slate-400 mb-1">Tipo de Batería</label>
                        <select id="battery_type" class="w-full bg-slate-950 border border-slate-700 rounded px-3 py-1.5 text-xs text-white">
                            <option value="36V">36V</option>
                            <option value="48V">48V</option>
                        </select>
                    </div>
                    <div>
                        <label class="block text-xs font-medium text-slate-400 mb-1">Batería S/N (Original)</label>
                        <input type="text" id="bat_sn_orig" placeholder="BAT-ORIG-XXXX" class="w-full bg-slate-950 border border-slate-700 rounded px-3 py-1.5 text-xs font-mono text-white">
                    </div>
                    <div>
                        <label class="block text-xs font-medium text-slate-400 mb-1">Batería S/N (Spare/Recambio)</label>
                        <input type="text" id="bat_sn_spare" placeholder="BAT-SPARE-XXXX" class="w-full bg-slate-950 border border-slate-700 rounded px-3 py-1.5 text-xs font-mono text-white">
                    </div>
                </div>

                <!-- Alarmas / Contador de Errores -->
                <div class="pt-3 border-t border-slate-800">
                    <span class="block text-xs font-bold text-amber-400 mb-2">CONTADOR DE ERRORES / ALARMAS REGISTRADAS:</span>
                    <div class="flex flex-wrap gap-3">
                        <label class="flex items-center space-x-1.5 bg-slate-950 px-3 py-1.5 rounded border border-slate-800 cursor-pointer">
                            <input type="checkbox" value="1" class="alarm-check rounded border-slate-700 text-amber-500">
                            <span class="text-xs font-mono font-bold text-slate-300">1</span>
                        </label>
                        <label class="flex items-center space-x-1.5 bg-slate-950 px-3 py-1.5 rounded border border-slate-800 cursor-pointer">
                            <input type="checkbox" value="2" class="alarm-check rounded border-slate-700 text-amber-500">
                            <span class="text-xs font-mono font-bold text-slate-300">2</span>
                        </label>
                        <label class="flex items-center space-x-1.5 bg-slate-950 px-3 py-1.5 rounded border border-slate-800 cursor-pointer">
                            <input type="checkbox" value="4" class="alarm-check rounded border-slate-700 text-amber-500">
                            <span class="text-xs font-mono font-bold text-slate-300">4</span>
                        </label>
                        <label class="flex items-center space-x-1.5 bg-slate-950 px-3 py-1.5 rounded border border-slate-800 cursor-pointer">
                            <input type="checkbox" value="8" class="alarm-check rounded border-slate-700 text-amber-500">
                            <span class="text-xs font-mono font-bold text-slate-300">8</span>
                        </label>
                        <label class="flex items-center space-x-1.5 bg-slate-950 px-3 py-1.5 rounded border border-slate-800 cursor-pointer">
                            <input type="checkbox" value="16" class="alarm-check rounded border-slate-700 text-amber-500">
                            <span class="text-xs font-mono font-bold text-slate-300">16</span>
                        </label>
                        <label class="flex items-center space-x-1.5 bg-slate-950 px-3 py-1.5 rounded border border-slate-800 cursor-pointer">
                            <input type="checkbox" value="32" class="alarm-check rounded border-slate-700 text-amber-500">
                            <span class="text-xs font-mono font-bold text-slate-300">32</span>
                        </label>
                        <label class="flex items-center space-x-1.5 bg-slate-950 px-3 py-1.5 rounded border border-slate-800 cursor-pointer">
                            <input type="checkbox" value="64" class="alarm-check rounded border-slate-700 text-amber-500">
                            <span class="text-xs font-mono font-bold text-slate-300">64</span>
                        </label>
                    </div>
                </div>
            </div>
        </div>

        <!-- TAB 2: CHASIS, ANCLAJE Y FRENO -->
        <div id="chassis-tab" class="tab-content hidden space-y-6">
            <div class="flex justify-between items-center bg-slate-900 p-4 rounded-xl border border-slate-800">
                <div>
                    <h2 class="text-base font-bold text-white">Mecánica Básica y Dinamometría</h2>
                    <p class="text-xs text-slate-400">Verificaciones de Pares de apriete, chasis, frenos y ruedas</p>
                </div>
                <button onclick="markSectionOK('section-chassis')" class="px-3 py-1.5 bg-slate-800 hover:bg-slate-700 text-emerald-400 border border-emerald-500/30 rounded-lg text-xs font-semibold">
                    Marcar sección como OK
                </button>
            </div>

            <div id="section-chassis" class="space-y-4">
                <!-- Section A -->
                <div class="checklist-card bg-slate-900 border border-slate-800 rounded-xl p-4">
                    <div class="flex items-center justify-between mb-3 pb-2 border-b border-slate-800">
                        <span class="text-xs font-bold text-red-400 uppercase">A. CHASIS - PAR DE APRIETE (Llave Dinamométrica / Allen 4-8mm)</span>
                        <span class="text-[10px] bg-slate-800 text-slate-400 px-2 py-0.5 rounded">Herramienta: DIN LLAVE</span>
                    </div>
                    <div class="space-y-3" id="group-A"></div>
                </div>

                <!-- Section B & C -->
                <div class="grid grid-cols-1 lg:grid-cols-2 gap-4">
                    <div class="checklist-card bg-slate-900 border border-slate-800 rounded-xl p-4">
                        <div class="flex items-center justify-between mb-3 pb-2 border-b border-slate-800">
                            <span class="text-xs font-bold text-red-400 uppercase">B. ANCLAJE</span>
                            <span class="text-[10px] bg-slate-800 text-slate-400 px-2 py-0.5 rounded">Manual / Visual</span>
                        </div>
                        <div class="space-y-3" id="group-B"></div>
                    </div>

                    <div class="checklist-card bg-slate-900 border border-slate-800 rounded-xl p-4">
                        <div class="flex items-center justify-between mb-3 pb-2 border-b border-slate-800">
                            <span class="text-xs font-bold text-red-400 uppercase">C. FRENO</span>
                            <span class="text-[10px] bg-slate-800 text-slate-400 px-2 py-0.5 rounded">Manual / Visual / Auditivo</span>
                        </div>
                        <div class="space-y-3" id="group-C"></div>
                    </div>
                </div>

                <!-- Section D, E, F, G -->
                <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                    <div class="checklist-card bg-slate-900 border border-slate-800 rounded-xl p-4">
                        <span class="text-xs font-bold text-red-400 uppercase block mb-3 pb-2 border-b border-slate-800">D. CABALLETE</span>
                        <div class="space-y-3" id="group-D"></div>
                    </div>
                    <div class="checklist-card bg-slate-900 border border-slate-800 rounded-xl p-4">
                        <span class="text-xs font-bold text-red-400 uppercase block mb-3 pb-2 border-b border-slate-800">E. NEUMÁTICO (Manómetro)</span>
                        <div class="space-y-3" id="group-E"></div>
                    </div>
                    <div class="checklist-card bg-slate-900 border border-slate-800 rounded-xl p-4">
                        <span class="text-xs font-bold text-red-400 uppercase block mb-3 pb-2 border-b border-slate-800">F. ACELERADOR</span>
                        <div class="space-y-3" id="group-F"></div>
                    </div>
                    <div class="checklist-card bg-slate-900 border border-slate-800 rounded-xl p-4">
                        <span class="text-xs font-bold text-red-400 uppercase block mb-3 pb-2 border-b border-slate-800">G. BATERÍA (Ajuste mecánico)</span>
                        <div class="space-y-3" id="group-G"></div>
                    </div>
                </div>
            </div>
        </div>

        <!-- TAB 3: ELECTRÓNICA Y CONSOLA -->
        <div id="electronics-tab" class="tab-content hidden space-y-6">
            <div class="flex justify-between items-center bg-slate-900 p-4 rounded-xl border border-slate-800">
                <div>
                    <h2 class="text-base font-bold text-white">Sistemas Electrónicos y Parámetros</h2>
                    <p class="text-xs text-slate-400">Verificación de luces, consola LCD, perímetros de rueda y cableado PCB</p>
                </div>
                <button onclick="markSectionOK('section-electronics')" class="px-3 py-1.5 bg-slate-800 hover:bg-slate-700 text-emerald-400 border border-emerald-500/30 rounded-lg text-xs font-semibold">
                    Marcar sección como OK
                </button>
            </div>

            <div id="section-electronics" class="space-y-4">
                <div class="grid grid-cols-1 lg:grid-cols-2 gap-4">
                    <div class="checklist-card bg-slate-900 border border-slate-800 rounded-xl p-4">
                        <span class="text-xs font-bold text-red-400 uppercase block mb-3 pb-2 border-b border-slate-800">H. BOCINA / LUZ</span>
                        <div class="space-y-3" id="group-H"></div>
                    </div>

                    <div class="checklist-card bg-slate-900 border border-slate-800 rounded-xl p-4">
                        <span class="text-xs font-bold text-red-400 uppercase block mb-3 pb-2 border-b border-slate-800">I. CONSOLA LCD & CONFIGURACIÓN</span>
                        <div class="space-y-3" id="group-I"></div>

                        <!-- Selector directo de Perímetro de Rueda -->
                        <div class="mt-4 p-3 bg-slate-950 rounded-lg border border-slate-800">
                            <span class="text-xs font-bold text-slate-300 block mb-2">Selección Rápida de Perímetro de Rueda (I.4):</span>
                            <div class="grid grid-cols-2 sm:grid-cols-3 gap-2 text-xs font-mono">
                                <button onclick="selectWheelPerimeter('M1', 1288)" class="perimeter-btn p-2 bg-slate-900 border border-slate-800 rounded hover:border-red-500 text-left">
                                    <span class="font-bold text-red-400">M1:</span> 1288
                                </button>
                                <button onclick="selectWheelPerimeter('M2', 0990)" class="perimeter-btn p-2 bg-slate-900 border border-slate-800 rounded hover:border-red-500 text-left">
                                    <span class="font-bold text-red-400">M2:</span> 0990
                                </button>
                                <button onclick="selectWheelPerimeter('E1/R1/H1/H1T', 1570)" class="perimeter-btn p-2 bg-slate-900 border border-slate-800 rounded hover:border-red-500 text-left">
                                    <span class="font-bold text-red-400">STD:</span> 1570
                                </button>
                                <button onclick="selectWheelPerimeter('E2/R2', 1445)" class="perimeter-btn p-2 bg-slate-900 border border-slate-800 rounded hover:border-red-500 text-left">
                                    <span class="font-bold text-red-400">E2/R2:</span> 1445
                                </button>
                                <button onclick="selectWheelPerimeter('S2', 1621)" class="perimeter-btn p-2 bg-slate-900 border border-slate-800 rounded hover:border-red-500 text-left">
                                    <span class="font-bold text-red-400">S2:</span> 1621
                                </button>
                                <button onclick="selectWheelPerimeter('H2/H2T', 1602)" class="perimeter-btn p-2 bg-slate-900 border border-slate-800 rounded hover:border-red-500 text-left">
                                    <span class="font-bold text-red-400">H2/H2T:</span> 1602
                                </button>
                            </div>
                            <input type="hidden" id="selected_perimeter" value="No seleccionado">
                            <div id="perimeter-display" class="mt-2 text-xs text-slate-400 italic">Perímetro seleccionado: <span class="text-emerald-400 font-bold">Ninguno</span></div>
                        </div>
                    </div>
                </div>

                <div class="checklist-card bg-slate-900 border border-slate-800 rounded-xl p-4">
                    <span class="text-xs font-bold text-red-400 uppercase block mb-3 pb-2 border-b border-slate-800">J. CABLEADO ELECTRÓNICO & CONTROLADOR</span>
                    <div class="space-y-3" id="group-J"></div>
                </div>
            </div>
        </div>

        <!-- TAB 4: COMPROBACIÓN DINÁMICA Y HÍBRIDOS -->
        <div id="dynamic-tab" class="tab-content hidden space-y-6">
            <div class="flex justify-between items-center bg-slate-900 p-4 rounded-xl border border-slate-800">
                <div>
                    <h2 class="text-base font-bold text-white">Comprobación Dinámica, Tolerancias y Modelos Híbridos</h2>
                    <p class="text-xs text-slate-400">Pruebas en parado/banco, giros de manillar y pedalero asistido H2/H2T</p>
                </div>
                <button onclick="markSectionOK('section-dynamic')" class="px-3 py-1.5 bg-slate-800 hover:bg-slate-700 text-emerald-400 border border-emerald-500/30 rounded-lg text-xs font-semibold">
                    Marcar sección como OK
                </button>
            </div>

            <div id="section-dynamic" class="space-y-4">
                <div class="checklist-card bg-slate-900 border border-slate-800 rounded-xl p-4">
                    <span class="text-xs font-bold text-red-400 uppercase block mb-3 pb-2 border-b border-slate-800">K. ACLERACIÓN, FRENADO & GIROS DE DIRECCIÓN</span>
                    <div class="space-y-3" id="group-K"></div>
                </div>

                <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                    <div class="checklist-card bg-slate-900 border border-slate-800 rounded-xl p-4">
                        <span class="text-xs font-bold text-red-400 uppercase block mb-3 pb-2 border-b border-slate-800">L. TOLERANCIA CABLEADO</span>
                        <div class="space-y-3" id="group-L"></div>
                    </div>

                    <div class="checklist-card bg-slate-900 border border-slate-800 rounded-xl p-4">
                        <span class="text-xs font-bold text-red-400 uppercase block mb-3 pb-2 border-b border-slate-800">M. DIRECCIÓN</span>
                        <div class="space-y-3" id="group-M"></div>
                    </div>
                </div>

                <div class="checklist-card bg-slate-900 border border-slate-800 rounded-xl p-4 border-l-4 border-l-amber-500">
                    <div class="flex items-center justify-between mb-3 pb-2 border-b border-slate-800">
                        <span class="text-xs font-bold text-amber-400 uppercase">N. ESPECÍFICO HÍBRIDOS (H2 / H2T)</span>
                        <span class="text-[10px] bg-amber-500/10 text-amber-400 border border-amber-500/20 px-2 py-0.5 rounded">Solo si aplica</span>
                    </div>
                    <div class="space-y-3" id="group-N"></div>
                </div>
            </div>
        </div>

        <!-- TAB 5: RUTA DE VALIDACIÓN FINAL -->
        <div id="validation-tab" class="tab-content hidden space-y-6">
            <div class="bg-slate-900 border border-slate-800 rounded-xl p-5 shadow-sm space-y-4">
                <h2 class="text-sm font-bold text-red-400 uppercase tracking-wider flex items-center space-x-2 border-b border-slate-800 pb-3">
                    <i class="fa-solid fa-road"></i>
                    <span>Prueba en Ruta de Validación Final (>= 4 km / 2.25 Millas)</span>
                </h2>
                <div class="p-4 bg-slate-950 rounded-xl border border-slate-800 space-y-3">
                    <p class="text-xs text-slate-300">
                        Conecte el software <strong class="text-white">'Batec Settings'</strong> y conduzca durante al menos 4 km / 2.25 millas. Verifique continuamente los siguientes parámetros dinámicos:
                    </p>
                    <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-3">
                        <label class="flex items-center space-x-2 bg-slate-900 p-2.5 rounded border border-slate-800 cursor-pointer">
                            <input type="checkbox" id="val_amperaje" class="rounded border-slate-700 text-emerald-500">
                            <span class="text-xs text-slate-300">Consumo de Amperaje OK</span>
                        </label>
                        <label class="flex items-center space-x-2 bg-slate-900 p-2.5 rounded border border-slate-800 cursor-pointer">
                            <input type="checkbox" id="val_gas" class="rounded border-slate-700 text-emerald-500">
                            <span class="text-xs text-slate-300">Respuesta Acelerador (GAS)</span>
                        </label>
                        <label class="flex items-center space-x-2 bg-slate-900 p-2.5 rounded border border-slate-800 cursor-pointer">
                            <input type="checkbox" id="val_subidas" class="rounded border-slate-700 text-emerald-500">
                            <span class="text-xs text-slate-300">Potencia en Subidas</span>
                        </label>
                        <label class="flex items-center space-x-2 bg-slate-900 p-2.5 rounded border border-slate-800 cursor-pointer">
                            <input type="checkbox" id="val_cambio" class="rounded border-slate-700 text-emerald-500">
                            <span class="text-xs text-slate-300">Sistema Cambio de Marchas</span>
                        </label>
                        <label class="flex items-center space-x-2 bg-slate-900 p-2.5 rounded border border-slate-800 cursor-pointer">
                            <input type="checkbox" id="val_asistencia" class="rounded border-slate-700 text-emerald-500">
                            <span class="text-xs text-slate-300">Asistencia de Pedaleo</span>
                        </label>
                    </div>
                </div>

                <!-- Datos del Técnico & Cierre -->
                <div class="pt-4 border-t border-slate-800 grid grid-cols-1 md:grid-cols-3 gap-4">
                    <div>
                        <label class="block text-xs font-medium text-slate-400 mb-1">Nombre / Número del Técnico SAT</label>
                        <input type="text" id="tecnico_nombre" placeholder="Ej: Juan Pérez (#T104)" class="w-full bg-slate-950 border border-slate-700 rounded px-3 py-2 text-xs text-white">
                    </div>
                    <div>
                        <label class="block text-xs font-medium text-slate-400 mb-1">Estado de Validación Final</label>
                        <select id="estado_final" class="w-full bg-slate-950 border border-slate-700 rounded px-3 py-2 text-xs font-bold text-emerald-400">
                            <option value="APTO">✅ VERIFICADO Y APTO PARA ENTREGA</option>
                            <option value="NO APTO">❌ NO APTO / REQUIERE ACCIÓN ADICIONAL</option>
                        </select>
                    </div>
                    <div class="flex items-end">
                        <button onclick="openFreshdeskModal()" class="w-full py-2 bg-emerald-600 hover:bg-emerald-500 text-white font-bold text-xs rounded-lg shadow-md shadow-emerald-900/30 transition flex items-center justify-center space-x-2">
                            <i class="fa-solid fa-check-circle"></i>
                            <span>Generar Informe Final Freshdesk</span>
                        </button>
                    </div>
                </div>
            </div>
        </div>

    </main>

    <!-- MODAL POPUP PARA CODIGO FRESHDESK -->
    <div id="freshdesk-modal" class="fixed inset-0 bg-slate-950/80 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
        <div class="bg-slate-900 border border-slate-800 rounded-2xl max-w-4xl w-full max-h-[90vh] flex flex-col shadow-2xl overflow-hidden">
            <!-- Modal Header -->
            <div class="p-4 border-b border-slate-800 flex justify-between items-center bg-slate-900">
                <div class="flex items-center space-x-2">
                    <i class="fa-solid fa-code text-red-500 text-lg"></i>
                    <h3 class="text-sm font-bold text-white">Exportación a Nota Interna de Freshdesk (Formato Código)</h3>
                </div>
                <button onclick="closeFreshdeskModal()" class="text-slate-400 hover:text-white p-1">
                    <i class="fa-solid fa-times text-lg"></i>
                </button>
            </div>

            <!-- Modal Body -->
            <div class="p-4 flex-1 overflow-y-auto space-y-3">
                <p class="text-xs text-slate-400">
                    Haga clic en el botón <strong class="text-slate-200">"Copiar al Portapapeles"</strong>. En Freshdesk, dentro de la nota interna, pulse el icono de código <code class="bg-slate-800 text-red-400 px-1 py-0.5 rounded">&lt;/&gt;</code> y pegue directamente el contenido.
                </p>

                <textarea id="freshdesk-log-output" readonly class="w-full h-96 bg-slate-950 border border-slate-800 rounded-xl p-4 text-xs font-mono text-emerald-400 code-font leading-relaxed focus:outline-none select-all"></textarea>
            </div>

            <!-- Modal Footer -->
            <div class="p-4 border-t border-slate-800 bg-slate-900 flex flex-wrap justify-between items-center gap-3">
                <span id="modal-toast" class="text-xs font-semibold text-emerald-400 hidden">
                    <i class="fa-solid fa-check-circle"></i> ¡Copiado al portapapeles con éxito!
                </span>
                <div class="flex items-center space-x-2 ml-auto">
                    <button onclick="closeFreshdeskModal()" class="px-4 py-2 bg-slate-800 hover:bg-slate-700 text-slate-300 rounded-lg text-xs font-semibold">
                        Cerrar
                    </button>
                    <button onclick="copyToClipboard()" class="px-4 py-2 bg-red-600 hover:bg-red-500 text-white font-bold rounded-lg text-xs shadow-lg shadow-red-600/30 flex items-center space-x-2">
                        <i class="fa-solid fa-copy"></i>
                        <span>Copiar al Portapapeles</span>
                    </button>
                </div>
            </div>
        </div>
    </div>

    <!-- JAVASCRIPT LOGIC -->
    <script>
        // DATA STRUCTURE FOR CHECKLIST ITEMS
        const checklistData = {
            'group-A': [
                { id: 'A1', text: '1. 2x M6 Puntera derecha (8 Nm) / 2x M6 Puntera izquierda (8 Nm)', type: 'DIN LLAVE' },
                { id: 'A2', text: '2. Tuerca izquierda buje (40 Nm) / Tuerca derecha buje (40 Nm)', type: 'DIN LLAVE' },
                { id: 'A3', text: '3. 4x M6 Adaptador de freno (8 Nm)', type: 'DIN LLAVE' },
                { id: 'A4', text: '4. 4x M6 Pinza de freno (8 Nm)', type: 'DIN LLAVE' },
                { id: 'A5', text: '5. M6 Palanca Diacompe 99 25 mm (15 Nm)', type: 'DIN LLAVE' },
                { id: 'A6', text: '6. Comprobar tornillos de soporte de luz apretados', type: 'MANUAL/VISUAL' },
                { id: 'A7', text: '7. Comprobar 2 tornillos de ajuste de dirección (6 Nm)', type: 'DIN LLAVE' }
            ],
            'group-B': [
                { id: 'B1', text: '1. Comprobar palanca de liberación libre sin atascos (REPITA 10 VECES)', type: 'MANUAL/VISUAL' },
                { id: 'B2', text: '2. Comprobar ajuste entre BARRA DE ANCLAJE y fijación', type: 'MANUAL/VISUAL' }
            ],
            'group-C': [
                { id: 'C1', text: '1. Comprobar pinzas centradas respecto al disco de freno', type: 'MANUAL/VISUAL' },
                { id: 'C2', text: '2. Comprobar estado de pastillas de freno', type: 'VISUAL/AUDITORY' },
                { id: 'C3', text: '3. Comprobar que funda de cable de freno no toque rueda', type: 'VISUAL' }
            ],
            'group-D': [
                { id: 'D1', text: '1. Comprobar libre movimiento de las ruedas', type: 'MANUAL' },
                { id: 'D2', text: '2. Comprobar presencia de Loctite (fuerza media)', type: 'MANUAL' }
            ],
            'group-E': [
                { id: 'E1', text: '1. Inflar neumático a 2.0 bar (+ 0.2 bar)', type: 'MANÓMETRO' }
            ],
            'group-F': [
                { id: 'F1', text: '1. Comprobar giro y retorno automático del acelerador', type: 'MANUAL' },
                { id: 'F2', text: '2. Mover cable acelerador sin alarmas en Display LCD', type: 'MANUAL/VISUAL' }
            ],
            'group-G': [
                { id: 'G1', text: '1. Inserción/Extracción y Conexión/Desconexión de batería', type: 'MANUAL' },
                { id: 'G2', text: '2. Pines conector Anderson en posición correcta (Batería/Batec)', type: 'MANUAL/VISUAL' }
            ],
            'group-H': [
                { id: 'H1', text: '1. Luces del./tras. (posición corta/larga) x4', type: 'MANUAL/VISUAL' },
                { id: 'H2', text: '2. Testigo luminoso correcto en consola', type: 'VISUAL' },
                { id: 'H3', text: '3. Funcionamiento y sonido de bocina', type: 'AUDITORY' }
            ],
            'group-I': [
                { id: 'I1', text: '1. Consola LCD: Funcionamiento e indicadores luminosos', type: 'MANUAL/VISUAL' },
                { id: 'I2', text: '2. Configuración de voltaje correcta (36V / 48V)', type: 'MANUAL/VISUAL' },
                { id: 'I3', text: '3. Funcionamiento puerto USB (Carga de móvil)', type: 'MANUAL' },
                { id: 'I4', text: '4. Configuración de perímetro de rueda', type: 'MANUAL/VISUAL' },
                { id: 'I5', text: '5. Fine Tune de batería en 0.0 (Presionar R+M x2)', type: 'MANUAL/VISUAL' }
            ],
            'group-J': [
                { id: 'J1', text: '1. Conexión cable motor - torsión (sin quemaduras/daños)', type: 'MANUAL/VISUAL' },
                { id: 'J2', text: '2. Conectores datos Driver PCB - Control PCB bien encajados', type: 'MANUAL/VISUAL' },
                { id: 'J3', text: '3. Condensadores en Driver PCB bien soldados y sin juego', type: 'MANUAL/VISUAL' },
                { id: 'J4', text: '4. Conectores potencia/tensión sin daños térmicos', type: 'MANUAL/VISUAL' },
                { id: 'J5', text: '5. Cables bien recogidos para holgura de cable de torsión', type: 'MANUAL/VISUAL' }
            ],
            'group-K': [
                { id: 'K1', text: '1. Acelerar avance/retroceso y niveles en LCD / Velocímetro / Ruidos motor', type: 'MANUAL/VISUAL' },
                { id: 'K2', text: '2. Frenado máx. velocidad / Sensor de corte LED / Mover cable', type: 'MANUAL/VISUAL' },
                { id: 'K3', text: '3. Rodadura en línea recta sin bloqueos', type: 'MANUAL/VISUAL' },
                { id: 'K4', text: '4. Giro manillar 90º acelerando (10 VECES por lado)', type: 'MANUAL/VISUAL' },
                { id: 'K5', text: '5. Comprobar ausencia de bloqueo tras giros', type: 'MANUAL/VISUAL' },
                { id: 'K6', text: '6. Simetría de manetas de freno sin tocar puños', type: 'MANUAL/VISUAL' },
                { id: 'K7', text: '7. Frenado total antes de tope mecánico (SOLO TETRA)', type: 'MANUAL/VISUAL' }
            ],
            'group-L': [
                { id: 'L1', text: '1. Sin tensión en cables eléctricos/frenado al girar 90º', type: 'MANUAL/VISUAL' }
            ],
            'group-M': [
                { id: 'M1', text: '1. Comprobar que la dirección no tenga holgura', type: 'MANUAL/VISUAL' },
                { id: 'M2', text: '2. Tensión del cierre rápido (Quick Release Clamp)', type: 'MANUAL' }
            ],
            'group-N': [
                { id: 'N1', text: '1. Funcionamiento asistencia electrónica con pedales + gas', type: 'VISUAL' },
                { id: 'N2', text: '2. Funcionamiento del cambio de marchas (H2/H2T)', type: 'MANUAL' },
                { id: 'N3', text: '3. Frenado completo antes de 1/16 vuelta atrás (H2T)', type: 'MANUAL' },
                { id: 'N4', text: '4. Funcionamiento del Magic Lever (H2T)', type: 'MANUAL' },
                { id: 'N5', text: '5. Tensiones de cableado ajustadas', type: 'MANUAL' }
            ]
        };

        // INITIALIZATION
        document.addEventListener('DOMContentLoaded', () => {
            // Set default date
            document.getElementById('fecha_registro').value = new Date().toISOString().split('T')[0];
            
            // Build UI Checklists
            buildChecklists();
            
            // Update global counters
            updateProgress();
        });

        // BUILD DYNAMIC CHECKLIST ITEM HTML
        function buildChecklists() {
            for (const [groupId, items] of Object.entries(checklistData)) {
                const container = document.getElementById(groupId);
                if (!container) continue;

                container.innerHTML = items.map(item => `
                    <div class="flex flex-col sm:flex-row sm:items-center justify-between p-2.5 bg-slate-950/60 rounded-lg border border-slate-800/80 gap-2 hover:border-slate-700 transition">
                        <div class="flex items-start space-x-2.5">
                            <span class="text-xs font-mono font-bold text-red-400 bg-red-500/10 px-1.5 py-0.5 rounded border border-red-500/20">${item.id}</span>
                            <span class="text-xs text-slate-200 leading-snug">${item.text}</span>
                        </div>
                        <div class="flex items-center space-x-1.5 self-end sm:self-auto">
                            <label class="px-2 py-1 bg-slate-900 border border-slate-800 rounded cursor-pointer hover:border-emerald-500/50 has-[:checked]:bg-emerald-500/20 has-[:checked]:border-emerald-500 has-[:checked]:text-emerald-400 text-[11px] font-bold text-slate-400 transition">
                                <input type="radio" name="chk_${item.id}" value="OK" onchange="updateProgress()" class="hidden">
                                <span>OK</span>
                            </label>
                            <label class="px-2 py-1 bg-slate-900 border border-slate-800 rounded cursor-pointer hover:border-red-500/50 has-[:checked]:bg-red-500/20 has-[:checked]:border-red-500 has-[:checked]:text-red-400 text-[11px] font-bold text-slate-400 transition">
                                <input type="radio" name="chk_${item.id}" value="NO" onchange="updateProgress()" class="hidden">
                                <span>NO</span>
                            </label>
                            <label class="px-2 py-1 bg-slate-900 border border-slate-800 rounded cursor-pointer hover:border-slate-600 has-[:checked]:bg-slate-800 has-[:checked]:border-slate-600 has-[:checked]:text-slate-200 text-[11px] font-bold text-slate-500 transition">
                                <input type="radio" name="chk_${item.id}" value="NA" onchange="updateProgress()" class="hidden">
                                <span>N/A</span>
                            </label>
                        </div>
                    </div>
                `).join('');
            }
        }

        // TAB SWITCHING
        function switchTab(tabId) {
            document.querySelectorAll('.tab-content').forEach(content => content.classList.add('hidden'));
            document.querySelectorAll('.tab-btn').forEach(btn => {
                btn.classList.remove('active', 'bg-red-600/20', 'text-red-400', 'border-red-500/30');
                btn.classList.add('text-slate-400', 'border-transparent');
            });

            document.getElementById(tabId).classList.remove('hidden');
            const activeBtn = document.getElementById(`btn-${tabId}`);
            if (activeBtn) {
                activeBtn.classList.add('active', 'bg-red-600/20', 'text-red-400', 'border-red-500/30');
                activeBtn.classList.remove('text-slate-400', 'border-transparent');
            }
        }

        // WHEEL PERIMETER SELECTION
        function selectWheelPerimeter(code, value) {
            document.getElementById('selected_perimeter').value = `${code} (${value})`;
            document.getElementById('perimeter-display').innerHTML = `Perímetro seleccionado: <span class="text-emerald-400 font-bold font-mono">${code} - ${value} mm</span>`;
            
            // Mark I4 as OK automatically
            const i4Radio = document.querySelector('input[name="chk_I4"][value="OK"]');
            if (i4Radio) {
                i4Radio.checked = true;
                updateProgress();
            }
        }

        // UPDATE PROGRESS BAR
        function updateProgress() {
            let total = 0;
            let checked = 0;

            for (const items of Object.values(checklistData)) {
                for (const item of items) {
                    total++;
                    const selected = document.querySelector(`input[name="chk_${item.id}"]:checked`);
                    if (selected) checked++;
                }
            }

            const percentage = total > 0 ? Math.round((checked / total) * 100) : 0;
            document.getElementById('progress-bar').style.width = `${percentage}%`;
            document.getElementById('progress-text').innerText = `${percentage}% (${checked}/${total})`;
        }

        // MARK ALL IN SECTION AS OK
        function markSectionOK(sectionContainerId) {
            const container = document.getElementById(sectionContainerId);
            if (!container) return;

            const radios = container.querySelectorAll('input[type="radio"][value="OK"]');
            radios.forEach(radio => radio.checked = true);
            updateProgress();
        }

        // MARK EVERYTHING GLOBAL AS OK
        function markAllGlobal(status) {
            for (const items of Object.values(checklistData)) {
                for (const item of items) {
                    const radio = document.querySelector(`input[name="chk_${item.id}"][value="${status}"]`);
                    if (radio) radio.checked = true;
                }
            }
            updateProgress();
        }

        // RESET ALL CHECKLISTS
        function resetAllChecklists() {
            for (const items of Object.values(checklistData)) {
                for (const item of items) {
                    const radios = document.querySelectorAll(`input[name="chk_${item.id}"]`);
                    radios.forEach(r => r.checked = false);
                }
            }
            updateProgress();
        }

        // GENERATE FRESHDESK LOG TEXT
        function generateFreshdeskLog() {
            const getVal = (id) => document.getElementById(id)?.value || 'N/A';
            const getChk = (id) => document.getElementById(id)?.checked ? '[X]' : '[ ]';
            
            const getStatus = (id) => {
                const sel = document.querySelector(`input[name="chk_${id}"]:checked`);
                return sel ? sel.value : '  ';
            };

            const selectedAlarms = Array.from(document.querySelectorAll('.alarm-check:checked')).map(c => c.value).join(', ') || 'Ninguna';

            return `================================================================================
                    REGISTRO DE VERIFICACIÓN TÉCNICA (RV-022 v3.0)
================================================================================

[1. DATOS DEL TICKET Y CABECERA]
--------------------------------------------------------------------------------
FECHA REGISTRO : ${getVal('fecha_registro')}
DISTRIBUIDOR   : ${getVal('distribuidor')}
TICKET / ORDEN : #${getVal('ticket_num')}
EXPLICACIÓN/OBS: ${getVal('observaciones')}

PARTES RECIBIDAS:
  ${getChk('part_pesos')} Pesos       ${getChk('part_cargador')} Cargador    ${getChk('part_bateria')} Batería
  ${getChk('part_otros')} Otros

DATOS DE ENTRADA Y SALIDA:
  BATEC S/N           : ${getVal('batec_sn')} | BASTIDOR S/N: ${getVal('bastidor_sn')}
  TOTAL KM / MILLAS   : ENTRADA [ ${getVal('km_entrada')} ] | SALIDA [ ${getVal('km_salida')} ]
  TOTAL KM/H / MPH    : ENTRADA [ ${getVal('speed_entrada')} ] | SALIDA [ ${getVal('speed_salida')} ]

TRAZABILIDAD DE COMPONENTES (ORIGINAL / SPARE):
  CONTROLLER S/N & SW : ORIGINAL [ ${getVal('controller_orig')} ] | SPARE [ ${getVal('controller_spare')} ]
  TIPO BATERÍA        : [ ${getVal('battery_type')} ]
  BATERÍA S/N         : ORIGINAL [ ${getVal('bat_sn_orig')} ] | SPARE [ ${getVal('bat_sn_spare')} ]
  P CODIFICACIÓN      : ${getVal('p_codificacion')}

CONTADOR DE ERRORES Y ALARMAS:
  ALARMAS ACTIVAS     : ${selectedAlarms}

================================================================================
[2. PASOS DE COMPROBACIÓN Y VERIFICACIÓN TÉCNICA]
================================================================================
(Leyenda estado: [OK] Conforme | [NO] Defectuoso | [NA] No aplica)

A. CHASIS - PAR DE APRIETE (Dinamométrica):
  [${getStatus('A1')}] A.1 Punteras derecha/izquierda (2x M6 @ 8 Nm)
  [${getStatus('A2')}] A.2 Tuercas buje izquierda/derecha (@ 40 Nm)
  [${getStatus('A3')}] A.3 Adaptador de freno (4x M6 @ 8 Nm)
  [${getStatus('A4')}] A.4 Pinza de freno (4x M6 @ 8 Nm)
  [${getStatus('A5')}] A.5 Palanca Diacompe 99 25mm (@ 15 Nm)
  [${getStatus('A6')}] A.6 Soporte de luz apretado
  [${getStatus('A7')}] A.7 Dirección: 2 tornillos de ajuste (@ 6 Nm)

B. ANCLAJE:
  [${getStatus('B1')}] B.1 Palanca de liberación libre (10x)
  [${getStatus('B2')}] B.2 Ajuste Barra de Anclaje y Fijación

C. FRENO:
  [${getStatus('C1')}] C.1 Centrado de pinza respecto al disco
  [${getStatus('C2')}] C.2 Estado de pastillas de freno
  [${getStatus('C3')}] C.3 Funda de cable de freno sin roce

D. CABALLETE & E. NEUMÁTICO:
  [${getStatus('D1')}] D.1 Libre movimiento de ruedas
  [${getStatus('D2')}] D.2 Fijación Loctite
  [${getStatus('E1')}] E.1 Inflado de neumático a 2.0 bar (+ 0.2 bar)

F. ACELERADOR & G. BATERÍA:
  [${getStatus('F1')}] F.1 Giro y retorno automático / Sujeción
  [${getStatus('F2')}] F.2 Cable acelerador sin alarmas en display
  [${getStatus('G1')}] G.1 Inserción/Extracción de batería fluida
  [${getStatus('G2')}] G.2 Posición de pines Anderson

H. ELECTRÓNICA & I. CONSOLA LCD:
  [${getStatus('H1')}] H.1 Encendido luces del/tras (corta/larga x4)
  [${getStatus('H2')}] H.2 Testigo luminoso en consola
  [${getStatus('H3')}] H.3 Funcionamiento de bocina
  [${getStatus('I1')}] I.1 Test general de display LCD
  [${getStatus('I2')}] I.2 Configuración de voltaje (36V/48V)
  [${getStatus('I3')}] I.3 Carga puerto USB
  [${getStatus('I4')}] I.4 Perímetro de rueda: ${getVal('selected_perimeter')}
  [${getStatus('I5')}] I.5 Fine Tune de batería en 0.0

J. CABLEADO ELECTRÓNICO & CONTROLADOR:
  [${getStatus('J1')}] J.1 Cable motor - torsión sin daños
  [${getStatus('J2')}] J.2 Conectores datos Driver/Control PCB
  [${getStatus('J3')}] J.3 Condensadores en Driver PCB firmes
  [${getStatus('J4')}] J.4 Conectores potencia sin fallo térmico
  [${getStatus('J5')}] J.5 Cableado recogido con holgura

K. COMPROBACIÓN DINÁMICA & GIROS:
  [${getStatus('K1')}] K.1 Aceleración/Velocímetro/Ruido motor
  [${getStatus('K2')}] K.2 Frenado máx. velocidad / Sensor corte
  [${getStatus('K3')}] K.3 Rodadura recta sin bloqueos
  [${getStatus('K4')}] K.4 Giro manillar 90º acelerando (10x por lado)
  [${getStatus('K5')}] K.5 Ausencia de bloqueo tras giros
  [${getStatus('K6')}] K.6 Simetría de manetas de freno
  [${getStatus('K7')}] K.7 Frenado antes de tope mecánico (Tetra)

L. TOLERANCIA, M. DIRECCIÓN & N. HÍBRIDOS:
  [${getStatus('L1')}] L.1 Cables sin tensión en girado 90º
  [${getStatus('M1')}] M.1 Holgura de dirección verificada
  [${getStatus('M2')}] M.2 Tensión de cierre rápido (Quick Release)
  [${getStatus('N1')}] N.1 Asistencia electrónica pedalier + gas
  [${getStatus('N2')}] N.2 Cambio de marchas (H2/H2T)
  [${getStatus('N3')}] N.3 Frenado a 1/16 vuelta atrás (H2T)
  [${getStatus('N4')}] N.4 Magic Lever (H2T)
  [${getStatus('N5')}] N.5 Tensiones de cableado ajustadas

================================================================================
[3. VALIDACIÓN FINAL EN RUTA Y FIRMA]
================================================================================

RUTA DE VALIDACIÓN (>= 4 km / 2.25 mi):
  ${getChk('val_amperaje')} Consumo Amperaje  ${getChk('val_gas')} Acelerador (GAS)  ${getChk('val_subidas')} Potencia Subidas
  ${getChk('val_cambio')} Cambio Marchas    ${getChk('val_asistencia')} Asistencia Pedaleo

ESTADO FINAL : ${getVal('estado_final')}
TÉCNICO SAT  : ${getVal('tecnico_nombre')}
================================================================================`;
        }

        // OPEN FRESHDESK MODAL
        function openFreshdeskModal() {
            const logText = generateFreshdeskLog();
            document.getElementById('freshdesk-log-output').value = logText;
            document.getElementById('freshdesk-modal').classList.remove('hidden');
        }

        // CLOSE FRESHDESK MODAL
        function closeFreshdeskModal() {
            document.getElementById('freshdesk-modal').classList.add('hidden');
            document.getElementById('modal-toast').classList.add('hidden');
        }

        // COPY TO CLIPBOARD
        function copyToClipboard() {
            const textarea = document.getElementById('freshdesk-log-output');
            textarea.select();
            
            try {
                document.execCommand('copy');
                const toast = document.getElementById('modal-toast');
                toast.classList.remove('hidden');
                setTimeout(() => toast.classList.add('hidden'), 3000);
            } catch (err) {
                console.error('Error al copiar: ', err);
            }
        }
    </script>
</body>
</html>
