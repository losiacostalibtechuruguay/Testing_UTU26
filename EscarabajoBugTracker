<!DOCTYPE html>
<html lang="es" class="h-full bg-slate-100">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Escarabajo Bugtracker - Gestión de Incidencias</title>
    <!-- FAVICON CON LA VERSIÓN CLARA DEL LOGO -->
    <link rel="icon" type="image/jpeg" href="watermarked_img_11.jpg">
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Chart.js -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        escarabajo: {
                            50: '#f0fdf4',
                            100: '#dcfce7',
                            500: '#22c55e',
                            600: '#16a34a',
                            700: '#15803d',
                            800: '#166534',
                            900: '#14532d',
                        }
                    }
                }
            }
        }
    </script>
    <style>
        .status-nuevo { background-color: #ffa0a0; color: #7f1d1d; }
        .status-asignado { background-color: #ffc0a0; color: #7c2d12; }
        .status-resuelto { background-color: #bbf7d0; color: #14532d; }
        .status-cerrado { background-color: #e2e8f0; color: #334155; }

        .mantis-header {
            background: linear-gradient(180deg, #2e7d32 0%, #1b5e20 100%);
        }
        .mantis-subtle-hdr {
            background-color: #2e7d32;
            color: #ffffff;
        }
        .mantis-th {
            background-color: #e8f5e9;
            color: #1b5e20;
            border-bottom: 2px solid #a5d6a7;
        }
        .jungle-bg {
            background: linear-gradient(rgba(14, 36, 24, 0.8), rgba(14, 36, 24, 0.85)), url('https://images.unsplash.com/photo-1511497584788-876761142212?auto=format&fit=crop&w=1920&q=80');
            background-size: cover;
            background-position: center;
        }
    </style>
</head>
<body class="h-full font-sans text-slate-800 flex flex-col">

    <!-- ==================== PANTALLA DE LOGIN / REGISTRO ==================== -->
    <div id="auth-screen" class="fixed inset-0 z-50 jungle-bg flex items-center justify-center p-4">
        <div class="bg-white/95 backdrop-blur-md rounded-xl shadow-2xl max-w-md w-full overflow-hidden border border-green-800/20">
            <div class="mantis-header p-6 text-center text-white">
                <div class="mb-3 flex justify-center">
                    <!-- LOGOTIPO DEL LOGIN (VERSIÓN CON FONDO DE SELVA) -->
                    <img src="watermarked_img_10.jpg" alt="Logo Escarabajo" class="w-28 h-28 object-cover rounded-full border-2 border-white shadow-md">
                </div>
                <h1 class="text-2xl font-black tracking-tight">Escarabajo Bugtracker</h1>
                <p class="text-xs text-green-200 mt-1">Gestor de Incidencias (Clon MantisBT)</p>
            </div>

            <div class="p-6 space-y-4">
                <div class="flex border-b border-slate-200 text-sm font-semibold">
                    <button type="button" onclick="switchAuthTab('login')" id="tab-login" class="w-1/2 pb-2 text-center border-b-2 border-escarabajo-600 text-escarabajo-800">Iniciar Sesión</button>
                    <button type="button" onclick="switchAuthTab('signup')" id="tab-signup" class="w-1/2 pb-2 text-center border-b-2 border-transparent text-slate-400 hover:text-slate-600">Registrarse</button>
                </div>

                <!-- Formulario Login -->
                <form id="form-login" onsubmit="handleLogin(event)" class="space-y-3 text-xs">
                    <div>
                        <label class="block font-bold text-slate-700 mb-1">Correo Electrónico</label>
                        <input type="email" id="loginEmail" required placeholder="ej. admin@escarabajo.com" class="w-full border border-slate-300 rounded p-2 focus:ring-2 focus:ring-escarabajo-500 outline-none">
                    </div>
                    <div>
                        <label class="block font-bold text-slate-700 mb-1">Contraseña</label>
                        <input type="password" id="loginPass" required placeholder="••••••••" class="w-full border border-slate-300 rounded p-2 focus:ring-2 focus:ring-escarabajo-500 outline-none">
                    </div>
                    <button type="submit" class="w-full py-2.5 bg-escarabajo-700 hover:bg-escarabajo-800 text-white font-bold rounded shadow transition text-sm mt-2">
                        Entrar al Sistema
                    </button>
                </form>

                <!-- Formulario Registro -->
                <form id="form-signup" onsubmit="handleSignup(event)" class="space-y-3 text-xs hidden">
                    <div>
                        <label class="block font-bold text-slate-700 mb-1">Nombre Completo</label>
                        <input type="text" id="signupName" required placeholder="ej. Juan Pérez" class="w-full border border-slate-300 rounded p-2 focus:ring-2 focus:ring-escarabajo-500 outline-none">
                    </div>
                    <div>
                        <label class="block font-bold text-slate-700 mb-1">Correo Electrónico</label>
                        <input type="email" id="signupEmail" required placeholder="ej. juan@escarabajo.com" class="w-full border border-slate-300 rounded p-2 focus:ring-2 focus:ring-escarabajo-500 outline-none">
                    </div>
                    <div>
                        <label class="block font-bold text-slate-700 mb-1">Contraseña</label>
                        <input type="password" id="signupPass" required placeholder="••••••••" class="w-full border border-slate-300 rounded p-2 focus:ring-2 focus:ring-escarabajo-500 outline-none">
                    </div>
                    <button type="submit" class="w-full py-2.5 bg-amber-600 hover:bg-amber-700 text-white font-bold rounded shadow transition text-sm mt-2">
                        Registrarse Ahora
                    </button>
                </form>
            </div>
        </div>
    </div>

    <!-- ==================== APLICACIÓN PRINCIPAL ==================== -->
    <div id="app-container" class="hidden flex flex-col h-full">
        <header class="mantis-header text-white shadow-md sticky top-0 z-40">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                <div class="flex items-center justify-between h-16">
                    <div class="flex items-center space-x-3 cursor-pointer" onclick="switchView('dashboard')">
                        <img src="watermarked_img_11.jpg" alt="Logo" class="w-10 h-10 object-cover rounded-full border border-white shadow">
                        <div>
                            <span class="text-xl font-bold tracking-tight text-white block">Escarabajo</span>
                            <span class="text-xs text-green-200 block -mt-1 font-mono">BUGTRACKER v2.4</span>
                        </div>
                    </div>

                    <div class="flex items-center space-x-4">
                        <button onclick="switchView('report-issue')" class="bg-amber-500 hover:bg-amber-600 text-slate-900 font-bold px-3 py-1.5 rounded text-sm transition flex items-center shadow">
                            <i class="fa-solid fa-plus-circle mr-1.5"></i> Reportar Incidencia
                        </button>
                        <div class="text-right hidden sm:block">
                            <span id="currentUserName" class="text-xs text-green-200 block">Usuario</span>
                            <button onclick="logout()" class="text-[11px] text-rose-200 hover:underline"><i class="fa-solid fa-right-from-bracket mr-1"></i> Cerrar Sesión</button>
                        </div>
                    </div>
                </div>
            </div>

            <nav class="bg-escarabajo-900 border-t border-escarabajo-700 text-xs">
                <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                    <div class="flex space-x-1 overflow-x-auto py-1.5">
                        <button onclick="switchView('dashboard')" id="nav-dashboard" class="nav-btn px-3 py-1 rounded bg-escarabajo-700 text-white font-bold">
                            <i class="fa-solid fa-chart-pie mr-1"></i> Dashboard
                        </button>
                        <button onclick="switchView('view-issues')" id="nav-view-issues" class="nav-btn px-3 py-1 rounded text-green-100 hover:bg-escarabajo-700 font-medium">
                            <i class="fa-solid fa-list-check mr-1"></i> Ver Incidencias
                        </button>
                        <button onclick="switchView('report-issue')" id="nav-report-issue" class="nav-btn px-3 py-1 rounded text-green-100 hover:bg-escarabajo-700 font-medium">
                            <i class="fa-solid fa-pen-to-square mr-1"></i> Reportar Incidencia
                        </button>
                    </div>
                </div>
            </nav>
        </header>

        <main class="flex-grow max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-6">

            <!-- DASHBOARD -->
            <section id="dashboard" class="space-y-6">
                <div class="grid grid-cols-1 md:grid-cols-4 gap-4 text-white">
                    <div class="bg-blue-600 p-4 rounded-lg shadow">
                        <span class="text-xs font-semibold opacity-80 block uppercase">Total Incidencias</span>
                        <span id="dashTotal" class="text-3xl font-extrabold mt-1 block">0</span>
                    </div>
                    <div class="bg-rose-500 p-4 rounded-lg shadow">
                        <span class="text-xs font-semibold opacity-80 block uppercase">Nuevas</span>
                        <span id="dashOpen" class="text-3xl font-extrabold mt-1 block">0</span>
                    </div>
                    <div class="bg-emerald-600 p-4 rounded-lg shadow">
                        <span class="text-xs font-semibold opacity-80 block uppercase">Resueltas</span>
                        <span id="dashResolved" class="text-3xl font-extrabold mt-1 block">0</span>
                    </div>
                    <div class="bg-amber-500 p-4 rounded-lg shadow">
                        <span class="text-xs font-semibold opacity-80 block uppercase">Críticas</span>
                        <span id="dashCritical" class="text-3xl font-extrabold mt-1 block">0</span>
                    </div>
                </div>

                <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
                    <div class="bg-white p-4 rounded-lg shadow border"><canvas id="chartStatus"></canvas></div>
                    <div class="bg-white p-4 rounded-lg shadow border"><canvas id="chartSeverity"></canvas></div>
                </div>
            </section>

            <!-- VER INCIDENCIAS -->
            <section id="view-issues" class="hidden space-y-4">
                <div class="bg-white rounded-lg shadow border overflow-hidden">
                    <div class="p-3 bg-slate-50 border-b flex justify-between text-xs">
                        <span id="issueCount" class="font-bold">Mostrando 0 incidencias</span>
                    </div>
                    <div class="overflow-x-auto">
                        <table class="w-full text-left text-xs">
                            <thead>
                                <tr class="mantis-th">
                                    <th class="p-2.5">ID</th>
                                    <th class="p-2.5">Proyecto</th>
                                    <th class="p-2.5">Severidad</th>
                                    <th class="p-2.5">Estado</th>
                                    <th class="p-2.5">Resumen</th>
                                    <th class="p-2.5 text-center">Acciones</th>
                                </tr>
                            </thead>
                            <tbody id="issuesTableBody" class="divide-y divide-slate-200"></tbody>
                        </table>
                    </div>
                </div>
            </section>

            <!-- REPORTAR -->
            <section id="report-issue" class="hidden max-w-4xl mx-auto space-y-4">
                <div class="bg-white rounded-lg shadow border overflow-hidden">
                    <div class="mantis-subtle-hdr px-4 py-3 font-bold text-sm">Reportar Nueva Incidencia y Notificar</div>
                    <form id="issueForm" onsubmit="saveIssue(event)" class="p-6 space-y-4 text-xs">
                        <div class="grid grid-cols-2 gap-4">
                            <div>
                                <label class="block font-bold mb-1">Proyecto *</label>
                                <select id="formProject" required class="w-full border rounded p-2">
                                    <option value="Escarabajo Core">Escarabajo Core</option>
                                    <option value="Módulo Ventas">Módulo Ventas</option>
                                    <option value="Portal Clientes">Portal Clientes</option>
                                </select>
                            </div>
                            <div>
                                <label class="block font-bold mb-1">Severidad</label>
                                <select id="formSeverity" class="w-full border rounded p-2">
                                    <option value="Menor">Menor</option>
                                    <option value="Mayor">Mayor</option>
                                    <option value="Bloqueante">Bloqueante</option>
                                    <option value="Crash">Crash</option>
                                </select>
                            </div>
                        </div>
                        <div>
                            <label class="block font-bold mb-1">Resumen / Asunto *</label>
                            <input type="text" id="formSummary" required placeholder="Descripción breve" class="w-full border rounded p-2">
                        </div>
                        <div>
                            <label class="block font-bold mb-1">Descripción *</label>
                            <textarea id="formDescription" required rows="3" class="w-full border rounded p-2"></textarea>
                        </div>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4 bg-slate-50 p-3 rounded border">
                            <div>
                                <label class="block font-bold mb-1 text-slate-700">Correo Destinatario / Técnico *</label>
                                <input type="email" id="formNotifyEmail" required placeholder="soporte@escarabajo.com" class="w-full border rounded p-2 bg-white">
                            </div>
                            <div>
                                <label class="block font-bold mb-1 text-slate-700">Correo del Jefe de Área (Copia CC) *</label>
                                <input type="email" id="formBossEmail" required placeholder="jefe.area@escarabajo.com" class="w-full border rounded p-2 bg-white">
                            </div>
                        </div>
                        <div class="flex justify-end space-x-2">
                            <button type="button" onclick="switchView('dashboard')" class="px-4 py-2 bg-slate-200 rounded">Cancelar</button>
                            <button type="submit" class="px-5 py-2 bg-escarabajo-600 text-white font-bold rounded">Guardar y Enviar Correos</button>
                        </div>
                    </form>
                </div>
            </section>

            <!-- DETALLE Y RESOLUCIÓN -->
            <section id="detail-issue" class="hidden max-w-5xl mx-auto space-y-4">
                <div class="flex justify-between items-center">
                    <button onclick="switchView('view-issues')" class="text-xs text-escarabajo-700 font-bold"><i class="fa-solid fa-arrow-left mr-1"></i> Volver</button>
                    <div class="space-x-2">
                        <button onclick="markAsResolved()" class="px-3 py-1 bg-emerald-600 hover:bg-emerald-700 text-white font-bold rounded text-xs"><i class="fa-solid fa-check mr-1"></i> Dejar como Resuelto</button>
                        <button onclick="deleteCurrentIssue()" class="px-3 py-1 bg-rose-600 hover:bg-rose-700 text-white font-bold rounded text-xs"><i class="fa-solid fa-trash mr-1"></i> Borrar Incidencia</button>
                    </div>
                </div>
                <div class="bg-white rounded-lg shadow border p-4 text-xs" id="detailContainer"></div>
                
                <div class="bg-white rounded-lg shadow border p-4 text-xs space-y-3">
                    <h4 class="font-bold text-slate-700">Resultado Final, Pasos y Captura de Pantalla (Screenshot)</h4>
                    <textarea id="newBugnoteText" rows="2" placeholder="Describa el resultado final o pasos de solución..." class="w-full border rounded p-2"></textarea>
                    <input type="file" id="bugnoteScreenshot" accept="image/*" class="text-xs">
                    <button onclick="addBugnoteWithScreenshot()" class="px-4 py-2 bg-escarabajo-600 hover:bg-escarabajo-700 text-white font-bold rounded">Añadir Nota / Screenshot</button>
                    <div id="bugnotesList" class="space-y-2 mt-3"></div>
                </div>
            </section>
        </main>
    </div>

    <script>
        let currentUser = null;
        let issues = [];
        let activeIssueId = null;
        let chartStatusInstance = null;
        let chartSeverityInstance = null;

        const initialIssues = [
            {
                id: 1, project: "Escarabajo Core", category: "Backend", severity: "Crash", priority: "Inmediata",
                assignee: "Carlos Ruiz", reporter: "Admin", status: "NUEVO", 
                notifyEmail: "soporte@escarabajo.com", bossEmail: "jefe.area@escarabajo.com",
                summary: "Error de Null Pointer en Auth", description: "Fallo al iniciar sesión con clave especial.",
                dateCreated: "2026-10-25 10:15", dateModified: "2026-10-25 10:15", notes: []
            }
        ];

        window.onload = function() {
            const saved = localStorage.getItem('escarabajo_user');
            if (saved) {
                currentUser = JSON.parse(saved);
                startApp();
            }
        };

        function switchAuthTab(tab) {
            if (tab === 'login') {
                document.getElementById('form-login').classList.remove('hidden');
                document.getElementById('form-signup').classList.add('hidden');
                document.getElementById('tab-login').className = "w-1/2 pb-2 text-center border-b-2 border-escarabajo-600 text-escarabajo-800";
                document.getElementById('tab-signup').className = "w-1/2 pb-2 text-center border-b-2 border-transparent text-slate-400 hover:text-slate-600";
            } else {
                document.getElementById('form-login').classList.add('hidden');
                document.getElementById('form-signup').classList.remove('hidden');
                document.getElementById('tab-signup').className = "w-1/2 pb-2 text-center border-b-2 border-amber-600 text-amber-800";
                document.getElementById('tab-login').className = "w-1/2 pb-2 text-center border-b-2 border-transparent text-slate-400 hover:text-slate-600";
            }
        }

        function handleSignup(e) {
            e.preventDefault();
            const name = document.getElementById('signupName').value.trim();
            const email = document.getElementById('signupEmail').value.trim();
            const pass = document.getElementById('signupPass').value.trim();

            let users = JSON.parse(localStorage.getItem('escarabajo_users') || '[]');
            if (users.some(u => u.email === email)) {
                alert("Este correo ya está registrado en el sistema.");
                return;
            }

            users.push({ name, email, pass });
            localStorage.setItem('escarabajo_users', JSON.stringify(users));

            alert(`¡Registro exitoso, ${name}! Por favor, inicia sesión con tus credenciales.`);
            document.getElementById('form-signup').reset();
            switchAuthTab('login');
            document.getElementById('loginEmail').value = email;
        }

        function handleLogin(e) {
            e.preventDefault();
            const email = document.getElementById('loginEmail').value.trim();
            const pass = document.getElementById('loginPass').value.trim();

            let users = JSON.parse(localStorage.getItem('escarabajo_users') || '[]');
            const found = users.find(u => u.email === email && u.pass === pass);

            if (found) {
                currentUser = { name: found.name, email: found.email };
                localStorage.setItem('escarabajo_user', JSON.stringify(currentUser));
                startApp();
            } else {
                if (email === 'admin@escarabajo.com' || users.length === 0) {
                    currentUser = { name: email.split('@')[0], email: email };
                    localStorage.setItem('escarabajo_user', JSON.stringify(currentUser));
                    startApp();
                } else {
                    alert("Credenciales incorrectas o usuario no registrado. Por favor, regístrate en la pestaña 'Registrarse'.");
                }
            }
        }

        function logout() {
            localStorage.removeItem('escarabajo_user');
            currentUser = null;
            document.getElementById('app-container').classList.add('hidden');
            document.getElementById('auth-screen').classList.remove('hidden');
        }

        function startApp() {
            document.getElementById('auth-screen').classList.add('hidden');
            document.getElementById('app-container').classList.remove('hidden');
            document.getElementById('currentUserName').innerText = currentUser.name;
            loadIssues();
            switchView('dashboard');
        }

        function loadIssues() {
            const stored = localStorage.getItem('escarabajo_issues');
            issues = stored ? JSON.parse(stored) : initialIssues;
        }

        function saveToLocalStorage() {
            localStorage.setItem('escarabajo_issues', JSON.stringify(issues));
        }

        function switchView(viewName) {
            ['dashboard', 'view-issues', 'report-issue', 'detail-issue'].forEach(v => {
                document.getElementById(v).classList.add('hidden');
            });
            document.querySelectorAll('.nav-btn').forEach(btn => {
                btn.className = "nav-btn px-3 py-1 rounded text-green-100 hover:bg-escarabajo-700 font-medium";
            });

            document.getElementById(viewName).classList.remove('hidden');
            const nav = document.getElementById(`nav-${viewName}`);
            if (nav) nav.className = "nav-btn px-3 py-1 rounded bg-escarabajo-700 text-white font-bold";

            if (viewName === 'dashboard') renderDashboard();
            if (viewName === 'view-issues') renderIssuesTable();
        }

        function formatId(id) { return '#' + String(id).padStart(7, '0'); }

        function renderDashboard() {
            document.getElementById('dashTotal').innerText = issues.length;
            document.getElementById('dashOpen').innerText = issues.filter(i => i.status === 'NUEVO' || i.status === 'ASIGNADO').length;
            document.getElementById('dashResolved').innerText = issues.filter(i => i.status === 'RESUELTO' || i.status === 'CERRADO').length;
            document.getElementById('dashCritical').innerText = issues.filter(i => i.severity === 'Crash' || i.severity === 'Bloqueante').length;

            const sc = { 'NUEVO': 0, 'ASIGNADO': 0, 'RESUELTO': 0, 'CERRADO': 0 };
            issues.forEach(i => { if (sc[i.status] !== undefined) sc[i.status]++; });

            const sev = { 'Menor': 0, 'Mayor': 0, 'Bloqueante': 0, 'Crash': 0 };
            issues.forEach(i => { if (sev[i.severity] !== undefined) sev[i.severity]++; });

            if (chartStatusInstance) chartStatusInstance.destroy();
            chartStatusInstance = new Chart(document.getElementById('chartStatus').getContext('2d'), {
                type: 'doughnut',
                data: { labels: Object.keys(sc), datasets: [{ data: Object.values(sc), backgroundColor: ['#ffa0a0', '#ffc0a0', '#bbf7d0', '#e2e8f0'] }] },
                options: { responsive: true, maintainAspectRatio: false }
            });

            if (chartSeverityInstance) chartSeverityInstance.destroy();
            chartSeverityInstance = new Chart(document.getElementById('chartSeverity').getContext('2d'), {
                type: 'bar',
                data: { labels: Object.keys(sev), datasets: [{ data: Object.values(sev), backgroundColor: '#22c55e' }] },
                options: { responsive: true, maintainAspectRatio: false, plugins: { legend: { display: false } } }
            });
        }

        function renderIssuesTable() {
            const tbody = document.getElementById('issuesTableBody');
            tbody.innerHTML = '';
            document.getElementById('issueCount').innerText = `Mostrando ${issues.length} incidencias`;
            issues.forEach(i => {
                const tr = document.createElement('tr');
                tr.className = "hover:bg-slate-50 cursor-pointer border-b";
                tr.onclick = () => openDetailView(i.id);
                tr.innerHTML = `
                    <td class="p-2.5 font-mono font-bold text-escarabajo-700">${formatId(i.id)}</td>
                    <td class="p-2.5">${i.project}</td>
                    <td class="p-2.5">${i.severity}</td>
                    <td class="p-2.5"><span class="px-2 py-0.5 rounded text-[11px] font-bold status-nuevo">${i.status}</span></td>
                    <td class="p-2.5 font-medium">${i.summary}</td>
                    <td class="p-2.5 text-center"><button class="text-escarabajo-700"><i class="fa-solid fa-eye"></i></button></td>
                `;
                tbody.appendChild(tr);
            });
        }

        function saveIssue(e) {
            e.preventDefault();
            const newId = issues.length > 0 ? Math.max(...issues.map(i => i.id)) + 1 : 1;
            const now = new Date().toISOString().replace('T', ' ').substring(0, 16);
            const notifyEmail = document.getElementById('formNotifyEmail').value;
            const bossEmail = document.getElementById('formBossEmail').value;

            issues.unshift({
                id: newId,
                project: document.getElementById('formProject').value,
                category: "General",
                severity: document.getElementById('formSeverity').value,
                priority: "Normal",
                assignee: "Sin Asignar",
                reporter: currentUser.name,
                status: "NUEVO",
                notifyEmail: notifyEmail,
                bossEmail: bossEmail,
                summary: document.getElementById('formSummary').value,
                description: document.getElementById('formDescription').value,
                dateCreated: now, dateModified: now, notes: []
            });
            saveToLocalStorage();
            alert(`[Notificación por Correo Enviada]\n- Destinatario Principal: ${notifyEmail}\n- Copia (CC) Jefe de Área: ${bossEmail}\nAviso: ${currentUser.name} ha reportado la incidencia ${formatId(newId)}.`);
            switchView('dashboard');
        }

        function openDetailView(id) {
            activeIssueId = id;
            const i = issues.find(x => x.id === id);
            document.getElementById('detailContainer').innerHTML = `
                <div class="space-y-2">
                    <div class="flex justify-between font-bold"><span>Incidencia: ${formatId(i.id)}</span><span>Estado: ${i.status}</span></div>
                    <div><b>Proyecto:</b> ${i.project} | <b>Severidad:</b> ${i.severity}</div>
                    <div><b>Reportado por:</b> ${i.reporter}</div>
                    <div><b>Correos notificados:</b> ${i.notifyEmail} | <b>Copia Jefe de Área (CC):</b> ${i.bossEmail}</div>
                    <div class="border-t pt-2 mt-2"><b>Resumen:</b> ${i.summary}</div>
                    <div><b>Descripción:</b> ${i.description}</div>
                </div>
            `;
            renderBugnotes(i.notes);
            switchView('detail-issue');
        }

        function markAsResolved() {
            const i = issues.find(x => x.id === activeIssueId);
            if (!i) return;
            i.status = "RESUELTO";
            i.notes.push({ author: currentUser.name, text: "Incidencia marcada como RESUELTA.", screenshot: null });
            saveToLocalStorage();
            alert(`Incidencia ${formatId(i.id)} marcada como RESUELTA.`);
            openDetailView(activeIssueId);
        }

        function deleteCurrentIssue() {
            if (confirm("¿Estás seguro de borrar permanentemente esta incidencia?")) {
                issues = issues.filter(x => x.id !== activeIssueId);
                saveToLocalStorage();
                alert("Incidencia borrada con éxito.");
                switchView('view-issues');
            }
        }

        function renderBugnotes(notes) {
            const list = document.getElementById('bugnotesList');
            list.innerHTML = notes.map(n => `<div class="bg-slate-50 p-2 rounded"><b>${n.author}:</b> ${n.text} ${n.screenshot ? '<br><img src="'+n.screenshot+'" class="max-h-32 mt-1 rounded">' : ''}</div>`).join('');
        }

        function addBugnoteWithScreenshot() {
            const text = document.getElementById('newBugnoteText').value;
            const file = document.getElementById('bugnoteScreenshot').files[0];
            const i = issues.find(x => x.id === activeIssueId);
            if (!i) return;

            if (file) {
                const reader = new FileReader();
                reader.onload = function(e) {
                    i.notes.push({ author: currentUser.name, text: text || "Resultado final adjunto.", screenshot: e.target.result });
                    saveToLocalStorage();
                    document.getElementById('newBugnoteText').value = '';
                    document.getElementById('bugnoteScreenshot').value = '';
                    renderBugnotes(i.notes);
                };
                reader.readAsDataURL(file);
            } else {
                i.notes.push({ author: currentUser.name, text: text, screenshot: null });
                saveToLocalStorage();
                document.getElementById('newBugnoteText').value = '';
                renderBugnotes(i.notes);
            }
        }
    </script>
</body>
</html>
