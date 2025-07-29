<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Generador de Alertas - Metro de Santiago</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            background-color: #f5f5f5;
        }
        .container {
            background-color: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }
        h1 {
            color: #005baa;
            text-align: center;
        }
        .form-group {
            margin-bottom: 15px;
        }
        label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
        }
        select, input, textarea {
            width: 100%;
            padding: 8px;
            border: 1px solid #ddd;
            border-radius: 4px;
            box-sizing: border-box;
        }
        textarea {
            height: 100px;
            resize: vertical;
        }
        button {
            background-color: #005baa;
            color: white;
            border: none;
            padding: 10px 15px;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
            margin-right: 10px;
            margin-bottom: 10px;
        }
        button:hover {
            background-color: #004080;
        }
        .alert-preview {
            margin-top: 20px;
            padding: 15px;
            background-color: #f8f9fa;
            border-left: 4px solid #005baa;
            white-space: pre-wrap;
            font-family: monospace;
        }
        .emoji-selector {
            display: flex;
            flex-wrap: wrap;
            gap: 5px;
            margin-bottom: 10px;
        }
        .emoji-option {
            font-size: 20px;
            cursor: pointer;
            padding: 5px;
            border-radius: 4px;
            background-color: #f0f0f0;
        }
        .emoji-option:hover {
            background-color: #e0e0e0;
        }
        .time-input {
            display: flex;
            align-items: center;
            gap: 10px;
        }
        .time-input input {
            width: 60px;
        }
        .procedure-buttons {
            display: flex;
            flex-wrap: wrap;
            gap: 5px;
            margin-bottom: 15px;
        }
        .procedure-btn {
            background-color: #e9ecef;
            color: #495057;
            border: 1px solid #ced4da;
        }
        .procedure-btn:hover {
            background-color: #d6d8db;
        }
        .direction-container {
            display: flex;
            gap: 10px;
        }
        .direction-container select {
            flex: 1;
        }
        .status-indicator {
            padding: 5px 10px;
            border-radius: 4px;
            font-weight: bold;
            display: inline-block;
            margin-right: 10px;
            cursor: pointer;
        }
        .status-normal {
            background-color: #d4edda;
            color: #155724;
        }
        .status-delayed {
            background-color: #fff3cd;
            color: #856404;
        }
        .status-suspended {
            background-color: #f8d7da;
            color: #721c24;
        }
        .segment-container {
            display: none;
            margin-top: 10px;
            border: 1px solid #ddd;
            padding: 10px;
            border-radius: 4px;
        }
        .segment-row {
            display: flex;
            gap: 10px;
            margin-bottom: 5px;
            align-items: center;
        }
        .segment-arrow {
            font-size: 20px;
        }
        .add-segment {
            margin-top: 5px;
            background-color: #e9ecef;
            color: #495057;
        }
        .delay-only-container {
            display: none;
            margin-top: 10px;
            padding: 10px;
            background-color: #fff3cd;
            border-radius: 4px;
        }
        .problem-selector {
            margin-top: 10px;
            display: none;
        }
        .location-selector {
            margin-top: 10px;
            display: none;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Generador de Alertas Metro de Santiago</h1>
        
        <div class="form-group">
            <label>Tipo de Incidente/Procedimiento</label>
            <div class="procedure-buttons">
                <button class="procedure-btn" onclick="setProcedure('person_on_tracks')">🚷 Persona en Vías</button>
                <button class="procedure-btn" onclick="setProcedure('severe_accident')">🚨 Accidente Grave</button>
                <button class="procedure-btn" onclick="setProcedure('emergency_brake')">⚠️ Frenazo de Emergencia</button>
                <button class="procedure-btn" onclick="setProcedure('train_failure')">⚙️ Avería de Tren</button>
                <button class="procedure-btn" onclick="setProcedure('door_failure')">⚙️ Avería de Puertas</button>
                <button class="procedure-btn" onclick="setProcedure('delays')">⏳ Atrasos</button>
                <button class="procedure-btn" onclick="setProcedure('power_outage')">🔌 Corte de Corriente</button>
                <button class="procedure-btn" onclick="setProcedure('health_incident')">🆘 Incidente de Salud</button>
                <button class="procedure-btn" onclick="setProcedure('express_route')">ℹ️ Ruta Expresa</button>
                <button class="procedure-btn" onclick="setProcedure('service_resumed')">✅ Servicio Reestablecido</button>
                <button class="procedure-btn" onclick="setProcedure('slow_service')">🐢 Servicio Lento</button>
                <button class="procedure-btn" onclick="setProcedure('controlled_access')">🛡️ Accesos Controlados</button>
                <button class="procedure-btn" onclick="setProcedure('station_closed')">⛔ Estación Cerrada</button>
                <button class="procedure-btn" onclick="setProcedure('line_suspended')">🚫 Línea Suspendida</button>
                <button class="procedure-btn" onclick="setProcedure('problems_with')">🔧 Problemas con</button>
                <button class="procedure-btn" onclick="setProcedure('platform_issues')">🚉 Problemas en Andén</button>
                <button class="procedure-btn" onclick="setProcedure('security_procedure')">👮 Procedimiento de Seguridad</button>
                <button class="procedure-btn" onclick="setProcedure('police_procedure')">🚔 Procedimiento Policial</button>
                <button class="procedure-btn" onclick="setProcedure('custom')">Personalizado</button>
            </div>
            <input type="text" id="procedure-text" placeholder="Texto del procedimiento (ej: 'Procedimiento de salud')" style="margin-top: 10px;">
            
            <div id="problem-selector" class="problem-selector">
                <select id="problem-type">
                    <option value="sistema de puertas">Sistema de puertas</option>
                    <option value="conducción automática">Conducción automática</option>
                    <option value="sistema eléctrico">Sistema eléctrico</option>
                    <option value="sistema de frenos">Sistema de frenos</option>
                    <option value="sistema de señalización">Sistema de señalización</option>
                </select>
            </div>
            
            <div id="location-selector" class="location-selector">
                <select id="location-type">
                    <option value="al interior">al interior</option>
                    <option value="al exterior">al exterior</option>
                    <option value="en andenes">en andenes</option>
                    <option value="en accesos">en accesos</option>
                </select>
            </div>
        </div>

        <div class="form-group">
            <label>Emoji/Icono</label>
            <div class="emoji-selector">
                <div class="emoji-option" onclick="selectEmoji('🐢')">🐢</div>
                <div class="emoji-option" onclick="selectEmoji('⚙️')">⚙️</div>
                <div class="emoji-option" onclick="selectEmoji('⚠️')">⚠️</div>
                <div class="emoji-option" onclick="selectEmoji('✅')">✅</div>
                <div class="emoji-option" onclick="selectEmoji('🚷')">🚷</div>
                <div class="emoji-option" onclick="selectEmoji('🛡️')">🛡️</div>
                <div class="emoji-option" onclick="selectEmoji('🔌')">🔌</div>
                <div class="emoji-option" onclick="selectEmoji('⌛')">⌛</div>
                <div class="emoji-option" onclick="selectEmoji('⏳')">⏳</div>
                <div class="emoji-option" onclick="selectEmoji('🚨')">🚨</div>
                <div class="emoji-option" onclick="selectEmoji('ℹ️')">ℹ️</div>
                <div class="emoji-option" onclick="selectEmoji('🚄')">🚄</div>
                <div class="emoji-option" onclick="selectEmoji('👀')">👀</div>
                <div class="emoji-option" onclick="selectEmoji('⛔')">⛔</div>
                <div class="emoji-option" onclick="selectEmoji('🆘')">🆘</div>
                <div class="emoji-option" onclick="selectEmoji('🤷‍♂️')">🤷‍♂️</div>
                <div class="emoji-option" onclick="selectEmoji('🔧')">🔧</div>
                <div class="emoji-option" onclick="selectEmoji('🚉')">🚉</div>
                <div class="emoji-option" onclick="selectEmoji('👮')">👮</div>
                <div class="emoji-option" onclick="selectEmoji('🚔')">🚔</div>
                <div class="emoji-option" onclick="selectEmoji('🚫')">🚫</div>
            </div>
            <input type="text" id="custom-emoji" placeholder="O escribe tu emoji aquí">
        </div>

        <div class="form-group">
            <label>Línea(s) afectada(s)</label>
            <select id="line" multiple>
                <option value="1">Línea 1</option>
                <option value="2">Línea 2</option>
                <option value="3">Línea 3</option>
                <option value="4">Línea 4</option>
                <option value="4A">Línea 4A</option>
                <option value="5">Línea 5</option>
                <option value="6">Línea 6</option>
            </select>
        </div>

        <div class="form-group">
            <label>Estación</label>
            <select id="station">
                <option value="">Seleccionar estación...</option>
                <!-- Stations will be loaded from JavaScript -->
            </select>
        </div>

        <div class="form-group">
            <label>Dirección del tren</label>
            <div class="direction-container">
                <select id="direction">
                    <option value="">No especificar</option>
                    <option value="San Pablo">San Pablo</option>
                    <option value="Los Dominicos">Los Dominicos</option>
                    <option value="Hospital El Pino">Hospital El Pino</option>
                    <option value="Vespucio Norte">Vespucio Norte</option>
                    <option value="Plaza Quilicura">Plaza Quilicura</option>
                    <option value="Fernando Castillo Velasco">Fernando Castillo Velasco</option>
                    <option value="Tobalaba">Tobalaba</option>
                    <option value="Plaza de Puente Alto">Plaza de Puente Alto</option>
                    <option value="Vicuña Mackenna">Vicuña Mackenna</option>
                    <option value="La Cisterna">La Cisterna</option>
                    <option value="Plaza de Maipú">Plaza de Maipú</option>
                    <option value="Vicente Valdés">Vicente Valdés</option>
                    <option value="Cerrillos">Cerrillos</option>
                    <option value="Los Leones">Los Leones</option>
                </select>
            </div>
        </div>

        <div class="form-group">
            <label>Hora del incidente</label>
            <div class="time-input">
                <input type="checkbox" id="include-time" checked>
                <input type="time" id="incident-time">
            </div>
        </div>

        <div class="form-group">
            <label>Detalles principales</label>
            <textarea id="details" placeholder="Ej: Tren continuó sin servicio..."></textarea>
        </div>

        <div class="form-group">
            <label>Notas adicionales (aparecerán con 👀)</label>
            <textarea id="notes" placeholder="Ej: Se estará retomando la frecuencia normal..."></textarea>
        </div>

        <div class="form-group">
            <label>Estado del servicio</label>
            <div>
                <span class="status-indicator status-normal" onclick="setServiceStatus('normal')">Normal</span>
                <span class="status-indicator status-delayed" onclick="setServiceStatus('delayed')">Con Demoras</span>
                <span class="status-indicator status-suspended" onclick="setServiceStatus('suspended')">Suspendido Parcial</span>
            </div>
            <div id="segment-container" class="segment-container">
                <div id="segments">
                    <div class="segment-row">
                        <span class="segment-arrow">⤵️</span>
                        <select class="segment-from" style="flex: 1;">
                            <option value="">Desde estación...</option>
                        </select>
                        <span class="segment-arrow">⤴️</span>
                        <select class="segment-to" style="flex: 1;">
                            <option value="">Hasta estación...</option>
                        </select>
                    </div>
                </div>
                <button class="add-segment" onclick="addSegment()">+ Añadir otro segmento</button>
            </div>
            <div id="delay-only-container" class="delay-only-container">
                <input type="checkbox" id="delay-only" onchange="toggleDelayOnly()"> 
                <label for="delay-only">Solo informar atrasos (sin detalles específicos)</label>
            </div>
        </div>

        <button onclick="generateAlert()">Generar Alerta</button>
        <button onclick="copyToClipboard()">Copiar al Portapapeles</button>

        <div class="form-group">
            <label>Vista previa:</label>
            <div class="alert-preview" id="alert-preview"></div>
        </div>
    </div>

    <script>
        // Current procedure type
        let currentProcedure = '';
        let currentServiceStatus = 'normal';
        let delayOnly = false;
        
        // Station data
        const metroStations = [
            "San Pablo", "Los Dominicos", "Hospital El Pino", "Vespucio Norte", 
            "Plaza Quilicura", "Fernando Castillo Velasco", "Tobalaba", 
            "Plaza de Puente Alto", "Vicuña Mackenna", "La Cisterna", 
            "Plaza de Maipú", "Vicente Valdés", "Cerrillos", "Los Leones",
            "Estación Central", "Santa Isabel", "Ñuble", "Estación del Sol",
            "Rodrigo de Araya", "Patronato", "Las Torres", "Baquedano",
            "Los Héroes", "Blanqueado", "Salvador", "Einstein", "Cal y Canto"
        ].sort();

        // Load stations
        function loadStations() {
            const stationSelect = document.getElementById('station');
            const segmentFrom = document.querySelector('.segment-from');
            const segmentTo = document.querySelector('.segment-to');
            
            // Clear existing options
            stationSelect.innerHTML = '<option value="">Seleccionar estación...</option>';
            segmentFrom.innerHTML = '<option value="">Desde estación...</option>';
            segmentTo.innerHTML = '<option value="">Hasta estación...</option>';
            
            metroStations.forEach(station => {
                const option = document.createElement('option');
                option.value = station;
                option.textContent = station;
                
                stationSelect.appendChild(option.cloneNode(true));
                segmentFrom.appendChild(option.cloneNode(true));
                segmentTo.appendChild(option.cloneNode(true));
            });
        }

        function toggleDelayOnly() {
            delayOnly = document.getElementById('delay-only').checked;
        }

        function addSegment() {
            const segmentsDiv = document.getElementById('segments');
            const newSegment = document.createElement('div');
            newSegment.className = 'segment-row';
            newSegment.innerHTML = `
                <span class="segment-arrow">⤵️</span>
                <select class="segment-from" style="flex: 1;">
                    <option value="">Desde estación...</option>
                    ${document.querySelector('.segment-from').innerHTML}
                </select>
                <span class="segment-arrow">⤴️</span>
                <select class="segment-to" style="flex: 1;">
                    <option value="">Hasta estación...</option>
                    ${document.querySelector('.segment-to').innerHTML}
                </select>
                <button onclick="this.parentNode.remove()" style="background: #f8d7da; color: #721c24;">×</button>
            `;
            segmentsDiv.appendChild(newSegment);
        }

        function setProcedure(procedure) {
            currentProcedure = procedure;
            const emojiMap = {
                'person_on_tracks': '🚷',
                'severe_accident': '🚨',
                'emergency_brake': '⚠️',
                'train_failure': '⚙️',
                'door_failure': '⚙️',
                'delays': '⏳',
                'power_outage': '🔌',
                'health_incident': '🆘',
                'express_route': 'ℹ️',
                'service_resumed': '✅',
                'slow_service': '🐢',
                'controlled_access': '🛡️',
                'station_closed': '⛔',
                'line_suspended': '🚫',
                'problems_with': '🔧',
                'platform_issues': '🚉',
                'security_procedure': '👮',
                'police_procedure': '🚔',
                'custom': ''
            };
            
            document.getElementById('custom-emoji').value = emojiMap[procedure] || '';
            
            // Show/hide problem selector
            document.getElementById('problem-selector').style.display = 
                (procedure === 'problems_with') ? 'block' : 'none';
            
            // Show/hide location selector
            document.getElementById('location-selector').style.display = 
                (['platform_issues', 'security_procedure', 'police_procedure'].includes(procedure)) ? 'block' : 'none';
            
            // Set default procedure text
            const procedureTextMap = {
                'person_on_tracks': 'Persona en las vías',
                'severe_accident': 'Accidente grave en las vías',
                'emergency_brake': 'Freno de emergencia',
                'train_failure': 'Avería de tren',
                'door_failure': 'Avería de puertas',
                'power_outage': 'Corte de corriente',
                'health_incident': 'Incidente de salud',
                'service_resumed': 'Servicio reestablecido',
                'slow_service': 'Servicio lento',
                'controlled_access': 'Accesos controlados',
                'station_closed': 'Estación cerrada',
                'line_suspended': 'Línea suspendida',
                'problems_with': 'Problemas con',
                'platform_issues': 'Problemas en andén',
                'security_procedure': 'Procedimiento de seguridad',
                'police_procedure': 'Procedimiento policial'
            };
            
            d
