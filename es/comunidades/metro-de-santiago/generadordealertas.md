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
            // Line 1
            "San Pablo L1", "Neptuno", "Pajaritos", "Las Rejas", "Ecuador", 
            "San Alberto Hurtado", "Universidad de Santiago", "Estación Central", 
            "U.L.A.", "República", "Los Héroes L1", "La Moneda", "Universidad de Chile L1", 
            "Santa Lucía", "Universidad Católica", "Baquedano L1", "Salvador", 
            "Manuel Montt", "Pedro de Valdivia", "Los Leones L1", "Tobalaba L1", 
            "El Golf", "Alcántara", "Escuela Militar", "Manquehue", 
            "Hernando de Magallanes", "Los Dominicos",

            // Line 2
            "Vespucio Norte", "Zapadores", "Dorsal", "Einstein", "Cementerios", 
            "Cerro Blanco", "Patronato", "Puente Cal y Canto L2", "Santa Ana L2", 
            "Los Héroes L2", "Toesca", "Parque O'Higgins", "Rondizzoni", 
            "Franklin L2", "El Llano", "San Miguel", "Lo Vial", "Departamental", 
            "Ciudad del Niño", "Lo Ovalle", "El Parrón", "La Cisterna L2", 
            "El Bosque", "Observatorio", "Copa Lo Martinez", "Hospital El Pino",

            // Line 3
            "Plaza Quilicura", "Lo Cruzat", "Ferrocarril", "Los Libertadores", 
            "Cardenal Caro", "Vivaceta", "Conchalí", "Plaza Chacabuco", 
            "Hospitales", "Puente Cal y Canto L3", "Plaza de Armas L3", 
            "Universidad de Chile L3", "Parque Almagro", "Matta", "Irarrázaval L3", 
            "Monseñor Eyzaguirre", "Ñuñoa L3", "Chile España", "Villa Frei", 
            "Plaza Egaña L3", "Fernando Castillo Velasco",

            // Line 4
            "Tobalaba L4", "Cristóbal Colón", "Francisco Bilbao", "Príncipe de Gales", 
            "Simón Bolivar", "Plaza Egaña L4", "Los Orientales", "Grecia", 
            "Los Presidentes", "Quilín", "Las Torres", "Macul", "Vicuña Mackenna L4", 
            "Vicente Valdés L4", "Rojas Magallanes", "Trinidad", 
            "San José de la Estrella", "Los Quillayes", "Elisa Correa", 
            "Hospital Sótero del Río", "Protectora de la Infancia", "Las Mercedes", 
            "Plaza de Puente Alto",

            // Line 4A
            "Vicuña Mackenna L4A", "Santa Julia", "La Granja", "Santa Rosa", 
            "San Ramón", "La Cisterna L4A",

            // Line 5
            "Plaza de Maipú", "Santiago Bueras", "Del Sol", "Monte Tabor", 
            "Las Parcelas", "Laguna Sur", "Barrancas", "Pudahuel", "San Pablo L5", 
            "Lo Prado", "Blanqueado", "Gruta de Lourdes", "Quinta Normal", 
            "Cumming", "Santa Ana L5", "Plaza de Armas L5", "Bellas Artes", 
            "Baquedano L5", "Parque Bustamante", "Santa Isabel", "Irarrázaval L5", 
            "Ñuble L5", "Rodrigo de Araya", "Carlos Valdovinos", "Camino Agrícola", 
            "San Joaquín", "Pedrero", "Mirador", "Bellavista de La Florida", 
            "Vicente Valdés L5",

            // Line 6
            "Cerrillos", "Lo Valledor", "Pdte. Pedro Aguirre Cerda", "Franklin L6", 
            "Bío Bío", "Ñuble L6", "Estadio Nacional", "Ñuñoa L6", 
            "Inés de Suárez", "Los Leones L6"
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
                'delays': 'Atrasos en el servicio',
                'power_outage': 'Corte de corriente',
                'health_incident': 'Incidente de salud',
                'express_route': 'Ruta expresa',
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
            
            document.getElementById('procedure-text').value = procedureTextMap[procedure] || '';
            
            // Set default details for certain procedures
            const detailsMap = {
                'person_on_tracks': 'Persona que descendió a las vías',
                'severe_accident': 'Accidente grave en las vías',
                'emergency_brake': 'Procedimiento de freno de emergencia',
                'train_failure': 'Tren detenido bajo revisión técnica',
                'door_failure': 'Avería en puertas de tren',
                'delays': 'Anticipar demoras en el servicio',
                'power_outage': 'Corte de corriente momentáneo',
                'health_incident': 'Procedimiento de salud activado',
                'express_route': 'Trenes operando como ruta expresa',
                'service_resumed': 'Servicio se ha restablecido',
                'slow_service': 'Operando con lentitud',
                'controlled_access': 'Accesos controlados en estación',
                'station_closed': 'Estación cerrada temporalmente',
                'line_suspended': 'Servicio suspendido en toda la línea',
                'problems_with': 'Problemas técnicos detectados',
                'platform_issues': 'Problemas reportados en andenes',
                'security_procedure': 'Procedimiento de seguridad activado',
                'police_procedure': 'Procedimiento policial en curso'
            };
            
            if (detailsMap[procedure]) {
                document.getElementById('details').value = detailsMap[procedure];
            }
            
            // Special handling for service status
            if (procedure === 'severe_accident' || procedure === 'line_suspended') {
                setServiceStatus('suspended');
            } else if (['train_failure', 'door_failure', 'person_on_tracks', 'delays', 'slow_service'].includes(procedure)) {
                setServiceStatus('delayed');
            } else if (procedure === 'service_resumed') {
                setServiceStatus('normal');
            }
            
            // Show delay-only option for delays
            document.getElementById('delay-only-container').style.display = 
                (procedure === 'delays') ? 'block' : 'none';
        }

        function setServiceStatus(status) {
            currentServiceStatus = status;
            const segmentContainer = document.getElementById('segment-container');
            
            if (status === 'suspended') {
                segmentContainer.style.display = 'block';
            } else {
                segmentContainer.style.display = 'none';
            }
            
            // Update UI indicators
            document.querySelectorAll('.status-indicator').forEach(el => {
                el.style.backgroundColor = '';
                el.style.color = '';
            });
            
            if (status === 'normal') {
                document.querySelector('.status-normal').style.backgroundColor = '#d4edda';
                document.querySelector('.status-normal').style.color = '#155724';
            } else if (status === 'delayed') {
                document.querySelector('.status-delayed').style.backgroundColor = '#fff3cd';
                document.querySelector('.status-delayed').style.color = '#856404';
            } else if (status === 'suspended') {
                document.querySelector('.status-suspended').style.backgroundColor = '#f8d7da';
                document.querySelector('.status-suspended').style.color = '#721c24';
            }
        }

        function selectEmoji(emoji) {
            document.getElementById('custom-emoji').value = emoji;
        }

        function generateAlert() {
            const emoji = document.getElementById('custom-emoji').value;
            let procedureText = document.getElementById('procedure-text').value;
            const lines = Array.from(document.getElementById('line').selectedOptions)
                .map(option => option.text);
            const station = document.getElementById('station').value;
            const direction = document.getElementById('direction').value;
            const includeTime = document.getElementById('include-time').checked;
            const time = document.getElementById('incident-time').value;
            const details = document.getElementById('details').value;
            const notes = document.getElementById('notes').value;
            
            // Handle problem type if selected
            if (currentProcedure === 'problems_with') {
                const problemType = document.getElementById('problem-type').value;
                procedureText += ` ${problemType}`;
            }
            
            // Handle location type if selected
            if (['platform_issues', 'security_procedure', 'police_procedure'].includes(currentProcedure)) {
                const locationType = document.getElementById('location-type').value;
                procedureText += ` ${locationType}`;
            }
            
            // Get service segments
            const segments = [];
            document.querySelectorAll('.segment-row').forEach(row => {
                const from = row.querySelector('.segment-from').value;
                const to = row.querySelector('.segment-to').value;
                if (from && to) {
                    segments.push({ from, to });
                }
            });

            let alertText = emoji || '⚠️';
            
            // Add time if included
            if (includeTime && time) {
                const formattedTime = `[${time}]`;
                alertText += ` ${formattedTime}`;
            }
            
            // Add procedure text
            if (procedureText) {
                alertText += ` ${procedureText}`;
            }
            
            // Add station if selected
            if (station) {
                alertText += ` en ${station}`;
            }
            
            // Add direction if selected
            if (direction) {
                alertText += ` Dirección ${direction}`;
            }
            
            // Add lines if selected
            if (lines.length > 0) {
                alertText += ` (${lines.join(', ')})`;
            }
            
            // Add details
            if (details && !(currentProcedure === 'delays' && delayOnly)) {
                alertText += `\n\n${emoji === 'ℹ️' ? 'ℹ️' : '⌛'} ${details}`;
            } else if (currentProcedure === 'delays' && delayOnly) {
                alertText += `\n\n⌛ Anticipar demoras en el servicio`;
            }
            
            // Add service status information
            if (currentServiceStatus === 'suspended' && segments.length > 0) {
                alertText += `\n\n⛔ Servicio solo disponible en:\n`;
                segments.forEach(segment => {
                    alertText += `⤵️ ${segment.from}\n⤴️ ${segment.to}\n`;
                });
            } else if (currentServiceStatus === 'delayed' && currentProcedure !== 'delays') {
                alertText += `\n\n⌛ Anticipar demoras y esperas mayores a la habitual`;
            }
            
            // Add notes if provided
            if (notes) {
                alertText += `\n\n👀 ${notes}`;
            }
            
            // Special handling for service resumed
            if (currentProcedure === 'service_resumed') {
                alertText += `\n\nℹ️ Recordar que esto no significa que estará todo bien, anticipar atrasos, demoras y saturación en andenes`;
            }

            document.getElementById('alert-preview').textContent = alertText;
        }

        function copyToClipboard() {
            const preview = document.getElementById('alert-preview');
            navigator.clipboard.writeText(preview.textContent)
                .then(() => alert('Alerta copiada al portapapeles!'))
                .catch(err => alert('Error al copiar: ' + err));
        }

        // Initialize
        window.onload = function() {
            loadStations();
            // Set current time as default
            const now = new Date();
            const hours = now.getHours().toString().padStart(2, '0');
            const minutes = now.getMinutes().toString().padStart(2, '0');
            document.getElementById('incident-time').value = `${hours}:${minutes}`;
            
            // Set default procedure
            setProcedure('custom');
        };
    </script>
</body>
</html>
