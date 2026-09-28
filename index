<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>RTO Grid Operations Notice Generator</title>
    <style>
        :root {
            --bg-color: #f0f2f5;
            --card-bg: #ffffff;
            --text-main: #1c1e21;
            --text-muted: #65676b;
            --border-color: #3b82f6;
            --border-light: #e4e6eb;
            --primary: #2563eb;
            --primary-hover: #1d4ed8;
            --viber-purple: #7360f2;
            --viber-hover: #5d48db;
            --shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
            --radius: 12px;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
            -webkit-tap-highlight-color: transparent;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-main);
            padding: 12px;
            padding-bottom: 40px;
            max-width: 500px;
            margin: 0 auto;
        }

        .header {
            text-align: center;
            margin-bottom: 14px;
            padding: 6px 0;
        }

        .header h1 {
            font-size: 1.2rem;
            font-weight: 700;
            color: #050505;
        }

        .header p {
            font-size: 0.78rem;
            color: var(--text-muted);
            margin-top: 2px;
        }

        .card {
            background: var(--card-bg);
            border-radius: var(--radius);
            padding: 16px;
            box-shadow: var(--shadow);
            margin-bottom: 14px;
        }

        .form-group {
            margin-bottom: 12px;
        }

        .form-group:last-child {
            margin-bottom: 0;
        }

        label {
            display: block;
            font-size: 0.75rem;
            font-weight: 700;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            color: var(--text-muted);
            margin-bottom: 4px;
        }

        label.required::after {
            content: " *";
            color: #dc2626;
        }

        select, input, textarea {
            width: 100%;
            padding: 10px 12px;
            border: 1px solid var(--border-light);
            border-radius: 8px;
            font-size: 0.9rem;
            background-color: #f8f9fa;
            color: var(--text-main);
            outline: none;
            transition: border-color 0.2s, background-color 0.2s;
        }

        select:focus, input:focus, textarea:focus {
            border-color: var(--primary);
            background-color: #ffffff;
        }

        select {
            appearance: none;
            background-image: url("data:image/svg+xml;charset=UTF-8,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='none' stroke='%3c2563eb' stroke-width='2' stroke-linecap='round' stroke-linejoin='round'%3e%3cpolyline points='6 9 12 15 18 9'%3e%3c/polyline%3e%3c/svg%3e");
            background-repeat: no-repeat;
            background-position: right 12px center;
            background-size: 16px;
            font-weight: 600;
            color: var(--primary);
            border-color: var(--border-color);
        }

        textarea {
            resize: vertical;
            min-height: 70px;
        }

        .btn {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            width: 100%;
            padding: 14px;
            border: none;
            border-radius: 8px;
            font-size: 0.95rem;
            font-weight: 700;
            cursor: pointer;
            transition: background-color 0.2s, transform 0.1s;
        }

        .btn:active {
            transform: scale(0.98);
        }

        .btn-viber {
            background-color: var(--viber-purple);
            color: #ffffff;
        }

        .btn-viber:hover {
            background-color: var(--viber-hover);
        }

        .preview-container {
            position: relative;
            background: #e5ddd5;
            background-image: radial-gradient(#cbd5e1 1px, transparent 0);
            background-size: 12px 12px;
            border-radius: var(--radius);
            padding: 12px;
            margin-top: 6px;
        }

        .chat-bubble {
            background: #ffffff;
            border-radius: 8px 8px 8px 0px;
            padding: 12px;
            box-shadow: 0 1px 2px rgba(0,0,0,0.15);
            position: relative;
            font-family: -apple-system, Roboto, sans-serif;
            white-space: pre-wrap;
            word-wrap: break-word;
            font-size: 0.88rem;
            line-height: 1.45;
            color: #111b21;
        }

        .toast {
            position: fixed;
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%) translateY(100px);
            background: #1e293b;
            color: white;
            padding: 12px 20px;
            border-radius: 25px;
            font-size: 0.85rem;
            font-weight: 600;
            box-shadow: 0 4px 12px rgba(0,0,0,0.25);
            transition: transform 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            z-index: 1000;
            pointer-events: none;
        }

        .toast.show {
            transform: translateX(-50%) translateY(0);
        }

        .error-border {
            border-color: #dc2626 !important;
            background-color: #fef2f2 !important;
        }
    </style>
</head>
<body>

    <div class="header">
        <h1>RTO Notice Generator</h1>
        <p>Operational Notice & Report Formatting Tool</p>
    </div>

    <!-- Notice Selection -->
    <div class="card">
        <div class="form-group">
            <label for="noticeType">Select Report / Notice Type</label>
            <select id="noticeType" onchange="renderFormFields()">
                <option value="contingency_removal">Contingency List Removal Notice</option>
                <option value="hvdc_limit">HVDC Limit Change Update</option>
                <option value="market_intervention">Market Intervention Notice</option>
                <option value="lifting_market_intervention">Lifting of Market Intervention Notice</option>
                <option value="contingency_congestion">Contingency Congestion Notice</option>
                <option value="base_case_congestion">Base Case Congestion Notice</option>
                <option value="load_curtailment">Regional Load Curtailment Notice</option>
            </select>
        </div>
    </div>

    <!-- Dynamic Operational Form -->
    <div class="card" id="formFields"></div>

    <!-- Reporter Signature -->
    <div class="card">
        <div class="form-group">
            <label for="reporterName" class="required">Dispatcher / Reporter Name</label>
            <input type="text" id="reporterName" placeholder="e.g. Gian Salle" oninput="saveReporterInfo(); updatePreview();">
        </div>
        <div class="form-group">
            <label for="reporterRole">Role / Shift (Optional)</label>
            <input type="text" id="reporterRole" placeholder="e.g. RTO-Visayas / Duty Dispatcher" oninput="saveReporterInfo(); updatePreview();">
        </div>
    </div>

    <!-- Live Preview & Viber Dispatch Action -->
    <div class="card">
        <label>Live Operational Preview</label>
        <div class="preview-container">
            <div class="chat-bubble" id="previewText">Generating preview...</div>
        </div>
        <button class="btn btn-viber" onclick="copyAndRedirectViber()" style="margin-top: 14px;">
            <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor"><path d="M19.37 16.03c-.52-.35-2.92-1.44-3.37-1.61-.45-.16-.78-.24-1.11.25-.33.49-1.28 1.61-1.57 1.94-.29.33-.58.37-1.1.11-.52-.26-2.19-.81-4.18-2.58-1.55-1.38-2.6-3.09-2.9-3.61-.3-.52-.03-.8.23-1.06.23-.23.52-.61.78-.91.26-.3.35-.52.52-.87.17-.35.09-.65-.04-.91-.13-.26-1.11-2.68-1.52-3.67-.4-.96-.82-.83-1.12-.85-.29-.02-.63-.02-.97-.02-.35 0-.91.13-1.38.65-.47.52-1.8 1.76-1.8 4.29 0 2.53 1.84 4.97 2.1 5.32.26.35 3.62 5.53 8.78 7.75 1.23.53 2.19.85 2.94 1.09 1.23.39 2.35.33 3.23.2 1-.15 3.07-1.25 3.5-2.46.43-1.21.43-2.25.3-2.47-.12-.22-.43-.35-.95-.61z"/></svg>
            Copy Report & Open Viber
        </button>
    </div>

    <div class="toast" id="toast">Copied to clipboard! Opening Viber...</div>

    <script>
        const schemas = {
            contingency_removal: {
                title: 'Contingency List Removal Notice',
                fields: [
                    { id: 'marketRun', label: 'Market Run', placeholder: 'e.g. RTD' },
                    { id: 'effective', label: 'Effective Time', placeholder: 'e.g. 1655H RTD' },
                    { id: 'contingencyEquipment', label: 'Contingency Equipment', placeholder: 'e.g. 1SJO_1MRL1' },
                    { id: 'outageRelated', label: 'Outage Related', placeholder: 'e.g. 3TAY_3TWP1' },
                    { id: 'outageDate', label: 'Outage Date & Time', placeholder: 'e.g. 09/27/26 0300H - 1700H' },
                    { id: 'actualOnline', label: 'Actual Online Details', type: 'textarea', placeholder: 'e.g. Tayabas - Tanay Wind Power 500kV Line restored at 1637H.' }
                ]
            },
            hvdc_limit: {
                title: 'HVDC Limit Change Update',
                fields: [
                    { id: 'event', label: 'Event', placeholder: 'e.g. Luz-Vis HVDC Limit Adjustment' },
                    { id: 'parameter', label: 'Parameter', placeholder: 'e.g. HVDC Reverse Limit' },
                    { id: 'previousLimit', label: 'Previous Limit', placeholder: 'e.g. 50MW' },
                    { id: 'newLimit', label: 'New Limit', placeholder: 'e.g. 120MW' },
                    { id: 'date', label: 'Date', placeholder: 'e.g. 09/27/2026' },
                    { id: 'effective', label: 'Effective Time', placeholder: 'e.g. 1710H RTD' }
                ]
            },
            market_intervention: {
                title: 'Market Intervention Notice',
                fields: [
                    { id: 'region', label: 'Region', placeholder: 'e.g. Visayas' },
                    { id: 'event', label: 'Event', placeholder: 'e.g. System Operator (SO) Initiated Market Intervention' },
                    { id: 'date', label: 'Date', placeholder: 'e.g. 09/23/2026' },
                    { id: 'start', label: 'Start Time', placeholder: 'e.g. 1515H-ongoing' },
                    { id: 'cause', label: 'Cause', type: 'textarea', placeholder: 'e.g. Implementation of Manual Load Dropping (MLD)...' },
                    { id: 'marketImpact', label: 'Market Impact', type: 'textarea', placeholder: 'e.g. Administered Pricing (AP) applied to Visayas.' },
                    { id: 'actionTaken', label: 'Action Taken', type: 'textarea', placeholder: 'e.g. AP Flag activated in COP reflected starting 1525H.' }
                ]
            },
            lifting_market_intervention: {
                title: 'Lifting of Market Intervention Notice',
                fields: [
                    { id: 'region', label: 'Region', placeholder: 'e.g. Visayas' },
                    { id: 'event', label: 'Event', placeholder: 'e.g. System Operator (SO) Initiated Market Intervention' },
                    { id: 'date', label: 'Date', placeholder: 'e.g. 09/23/2026' },
                    { id: 'start', label: 'Start Time', placeholder: 'e.g. 1515H-2155H' },
                    { id: 'duration', label: 'Duration', placeholder: 'e.g. 6hrs and 45mins' },
                    { id: 'cause', label: 'Cause', type: 'textarea', placeholder: 'e.g. Implementation of Manual Load Dropping (MLD)...' },
                    { id: 'marketImpact', label: 'Market Impact', type: 'textarea', placeholder: 'e.g. Administered Pricing (AP) applied to Visayas.' },
                    { id: 'actionTaken', label: 'Action Taken', type: 'textarea', placeholder: 'e.g. AP Flag deleted in COP starting 2155H in DIPC run.' }
                ]
            },
            contingency_congestion: {
                title: 'Contingency Congestion Notice',
                fields: [
                    { id: 'elementHeader', label: 'Header Element Identifier', placeholder: 'e.g. 3DASMA_TR1' },
                    { id: 'marketRun', label: 'Market Run', placeholder: 'e.g. RTD' },
                    { id: 'region', label: 'Region', placeholder: 'e.g. Luzon' },
                    { id: 'event', label: 'Event', placeholder: 'e.g. Contingency Case Congestion' },
                    { id: 'element', label: 'Element', placeholder: 'e.g. 3DASMA_TR1' },
                    { id: 'date', label: 'Date', placeholder: 'e.g. 09/25/2026' },
                    { id: 'interval', label: 'Interval', placeholder: 'e.g. 1140H and 1225H' },
                    { id: 'finding', label: 'Finding', type: 'textarea', placeholder: 'e.g. Reaching capacity to binding limit of 598MW...' },
                    { id: 'status', label: 'Status', type: 'textarea', placeholder: 'e.g. Upon simulation, congestion was not manifested.' }
                ]
            },
            base_case_congestion: {
                title: 'Base Case Congestion Notice',
                fields: [
                    { id: 'elementHeader', label: 'Header Element Identifier', placeholder: 'e.g. 14TACUR_TR4' },
                    { id: 'marketRun', label: 'Market Run', placeholder: 'e.g. RTD' },
                    { id: 'region', label: 'Region', placeholder: 'e.g. Mindanao' },
                    { id: 'event', label: 'Event', placeholder: 'e.g. Base Case Congestion' },
                    { id: 'element', label: 'Element', placeholder: 'e.g. 14TACUR_TR4' },
                    { id: 'date', label: 'Date', placeholder: 'e.g. 09/26/2026' },
                    { id: 'interval', label: 'Interval', placeholder: 'e.g. 0805H - 0900H' },
                    { id: 'finding', label: 'Finding', type: 'textarea', placeholder: 'e.g. Sudden increase of schedule of 14DSA_T2L1...' },
                    { id: 'status', label: 'Status', type: 'textarea', placeholder: 'e.g. At 0905H congestion was resolved.' }
                ]
            },
            load_curtailment: {
                title: 'Load Curtailment Notice',
                fields: [
                    { id: 'marketRun', label: 'Market Run', placeholder: 'e.g. RTD' },
                    { id: 'region', label: 'Region', placeholder: 'e.g. Visayas Grid' },
                    { id: 'event', label: 'Event', placeholder: 'e.g. Intermittent Load Curtailment' },
                    { id: 'magnitude', label: 'Magnitude', placeholder: 'e.g. 10.04-70.38 MW' },
                    { id: 'date', label: 'Date', placeholder: 'e.g. 09/26/2026' },
                    { id: 'intervals', label: 'Intervals Affected', placeholder: 'e.g. 1755H-1840H' },
                    { id: 'finding', label: 'Finding', type: 'textarea', placeholder: 'e.g. Generation deficiency.' },
                    { id: 'impact', label: 'Impact', placeholder: 'e.g. Possible PEN/Market Rerun' },
                    { id: 'status', label: 'Status', type: 'textarea', placeholder: 'e.g. MO on duty already notified CGO as of 1829H.' }
                ]
            }
        };

        let currentNoticeText = '';

        function renderFormFields() {
            const type = document.getElementById('noticeType').value;
            const schema = schemas[type];
            const container = document.getElementById('formFields');
            container.innerHTML = '';

            schema.fields.forEach(field => {
                const group = document.createElement('div');
                group.className = 'form-group';

                const label = document.createElement('label');
                label.innerText = field.label;
                group.appendChild(label);

                if (field.type === 'textarea') {
                    const textarea = document.createElement('textarea');
                    textarea.id = field.id;
                    textarea.placeholder = field.placeholder || '';
                    textarea.value = '';
                    textarea.rows = 2;
                    textarea.oninput = updatePreview;
                    group.appendChild(textarea);
                } else {
                    const input = document.createElement('input');
                    input.type = 'text';
                    input.id = field.id;
                    input.placeholder = field.placeholder || '';
                    input.value = '';
                    input.oninput = updatePreview;
                    group.appendChild(input);
                }

                container.appendChild(group);
            });

            updatePreview();
        }

        function updatePreview() {
            const type = document.getElementById('noticeType').value;
            const schema = schemas[type];
            let output = '';

            const getVal = (id) => {
                const el = document.getElementById(id);
                return el ? el.value.trim() : '';
            };

            if (type === 'contingency_removal') {
                output = `${schema.title}\n\n`;
                if (getVal('marketRun')) output += `▪ Market Run: ${getVal('marketRun')}\n`;
                if (getVal('effective')) output += `▪ Effective: ${getVal('effective')}\n`;
                if (getVal('contingencyEquipment')) output += `▪ Contingency Equipment: ${getVal('contingencyEquipment')}\n`;
                if (getVal('outageRelated')) output += `▪ Outage Related: ${getVal('outageRelated')}\n`;
                if (getVal('outageDate')) output += `▪ Outage Date: ${getVal('outageDate')}\n`;
                if (getVal('actualOnline')) output += `▪ Actual Online: ${getVal('actualOnline')}\n`;

            } else if (type === 'hvdc_limit') {
                output = `${schema.title}\n\n`;
                if (getVal('event')) output += `▪ Event: ${getVal('event')}\n`;
                if (getVal('parameter')) output += `▪ Parameter: ${getVal('parameter')}\n`;
                if (getVal('previousLimit')) output += `▪ Previous Limit: ${getVal('previousLimit')}\n`;
                if (getVal('newLimit')) output += `▪ New Limit: ${getVal('newLimit')}\n`;
                if (getVal('date')) output += `▪ Date: ${getVal('date')}\n`;
                if (getVal('effective')) output += `▪ Effective: ${getVal('effective')}\n`;

            } else if (type === 'market_intervention') {
                output = `${schema.title}\n\n`;
                if (getVal('region')) output += `▪ Region: ${getVal('region')}\n`;
                if (getVal('event')) output += `▪ Event: ${getVal('event')}\n`;
                if (getVal('date')) output += `▪ Date: ${getVal('date')}\n`;
                if (getVal('start')) output += `▪ Start: ${getVal('start')}\n`;
                if (getVal('cause')) output += `▪ Cause: ${getVal('cause')}\n`;
                if (getVal('marketImpact')) output += `▪ Market Impact: ${getVal('marketImpact')}\n`;
                if (getVal('actionTaken')) output += `▪ Action Taken: ${getVal('actionTaken')}\n`;
                output += `\nThank you.`;

            } else if (type === 'lifting_market_intervention') {
                output = `${schema.title}\n\n`;
                if (getVal('region')) output += `▪ Region: ${getVal('region')}\n`;
                if (getVal('event')) output += `▪ Event: ${getVal('event')}\n`;
                if (getVal('date')) output += `▪ Date: ${getVal('date')}\n`;
                if (getVal('start')) output += `▪ Start: ${getVal('start')}\n`;
                if (getVal('duration')) output += `▪ Duration: ${getVal('duration')}\n`;
                if (getVal('cause')) output += `▪ Cause: ${getVal('cause')}\n`;
                if (getVal('marketImpact')) output += `▪ Market Impact: ${getVal('marketImpact')}\n`;
                if (getVal('actionTaken')) output += `▪ Action Taken: ${getVal('actionTaken')}\n`;

            } else if (type === 'contingency_congestion' || type === 'base_case_congestion') {
                const elemHeader = getVal('elementHeader');
                output = elemHeader ? `${schema.title} - ${elemHeader}\n\n` : `${schema.title}\n\n`;
                if (getVal('marketRun')) output += `▪ Market Run: ${getVal('marketRun')}\n`;
                if (getVal('region')) output += `▪ Region: ${getVal('region')}\n`;
                if (getVal('event')) output += `▪ Event: ${getVal('event')}\n`;
                if (getVal('element')) output += `▪ Element: ${getVal('element')}\n`;
                if (getVal('date')) output += `▪ Date: ${getVal('date')}\n`;
                if (getVal('interval')) output += `▪ Interval: ${getVal('interval')}\n`;
                if (getVal('finding')) output += `▪ Finding: ${getVal('finding')}\n`;
                if (getVal('status')) output += `▪ Status: ${getVal('status')}\n`;

            } else if (type === 'load_curtailment') {
                const reg = getVal('region');
                output = reg ? `${reg} Load Curtailment Notice\n\n` : `${schema.title}\n\n`;
                if (getVal('marketRun')) output += `▪ Market Run: ${getVal('marketRun')}\n`;
                if (getVal('region')) output += `▪ Region: ${getVal('region')}\n`;
                if (getVal('event')) output += `▪ Event: ${getVal('event')}\n`;
                if (getVal('magnitude')) output += `▪ Magnitude: ${getVal('magnitude')}\n`;
                if (getVal('date')) output += `▪ Date: ${getVal('date')}\n`;
                if (getVal('intervals')) output += `▪ Intervals affected: ${getVal('intervals')}\n`;
                if (getVal('finding')) output += `▪ Finding: ${getVal('finding')}\n`;
                if (getVal('impact')) output += `▪ Impact: ${getVal('impact')}\n`;
                if (getVal('status')) output += `▪ Status: ${getVal('status')}\n`;
            }

            // Append Signature Line
            const name = document.getElementById('reporterName').value.trim();
            const role = document.getElementById('reporterRole').value.trim();

            if (name) {
                const sig = role ? `\n\n▪ Reported by: ${name} (${role})` : `\n\n▪ Reported by: ${name}`;
                output += sig;
            }

            currentNoticeText = output.trim();
            document.getElementById('previewText').innerText = currentNoticeText || 'Fill in form fields above to view preview...';
        }

        function saveReporterInfo() {
            const name = document.getElementById('reporterName').value;
            const role = document.getElementById('reporterRole').value;
            localStorage.setItem('rto_reporter_name', name);
            localStorage.setItem('rto_reporter_role', role);
        }

        function loadReporterInfo() {
            const savedName = localStorage.getItem('rto_reporter_name');
            const savedRole = localStorage.getItem('rto_reporter_role');
            if (savedName) document.getElementById('reporterName').value = savedName;
            if (savedRole) document.getElementById('reporterRole').value = savedRole;
        }

        function copyAndRedirectViber() {
            const reporterInput = document.getElementById('reporterName');
            if (!reporterInput.value.trim()) {
                reporterInput.classList.add('error-border');
                reporterInput.focus();
                alert('Please enter Dispatcher / Reporter Name before sending.');
                return;
            }
            reporterInput.classList.remove('error-border');

            const executeCopy = () => {
                if (navigator.clipboard && window.isSecureContext) {
                    return navigator.clipboard.writeText(currentNoticeText);
                } else {
                    const textArea = document.createElement("textarea");
                    textArea.value = currentNoticeText;
                    textArea.style.position = "fixed";
                    textArea.style.left = "-999999px";
                    document.body.appendChild(textArea);
                    textArea.focus();
                    textArea.select();
                    return new Promise((resolve, reject) => {
                        document.execCommand('copy') ? resolve() : reject();
                        textArea.remove();
                    });
                }
            };

            executeCopy().then(() => {
                showToast();
                setTimeout(() => {
                    window.location.href = "viber://";
                }, 800);
            }).catch(() => {
                alert('Copying failed. Please copy manually from the preview window.');
            });
        }

        function showToast() {
            const toast = document.getElementById('toast');
            toast.classList.add('show');
            setTimeout(() => {
                toast.classList.remove('show');
            }, 2500);
        }

        window.onload = () => {
            loadReporterInfo();
            renderFormFields();
        };
    </script>
</body>
</html>
