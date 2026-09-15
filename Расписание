<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Расписание</title>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css">
</head>
<body class="bg-light p-4">
    <div class="container bg-white p-4 rounded shadow-sm">
        <h1 class="mb-4 text-center">Расписание занятий</h1>
        
        <input type="text" id="searchInput" class="form-control mb-3" placeholder="Поиск по предмету, группе или преподавателю...">
        
        <div class="table-responsive">
            <table class="table table-bordered table-striped" id="scheduleTable">
                <thead class="table-dark" id="tableHead"></thead>
                <tbody id="tableBody"></tbody>
            </table>
        </div>
    </div>

    <script>
        async function loadSchedule() {
            const response = await fetch('schedule.json');
            const data = await response.json();
            
            if (data.length === 0) return;

            const headers = Object.keys(data[0]);
            const thead = document.getElementById('tableHead');
            const tbody = document.getElementById('tableBody');

            // Генерация заголовков таблицы
            let headRow = '<tr>';
            headers.forEach(h => headRow += `<th>${h}</th>`);
            headRow += '</tr>';
            thead.innerHTML = headRow;

            // Генерация строк
            function renderRows(items) {
                tbody.innerHTML = '';
                items.forEach(row => {
                    let tr = '<tr>';
                    headers.forEach(h => tr += `<td>${row[h] ?? ''}</td>`);
                    tr += '</tr>';
                    tbody.innerHTML += tr;
                });
            }

            renderRows(data);

            // Фильтрация/поиск
            document.getElementById('searchInput').addEventListener('input', (e) => {
                const term = e.target.value.toLowerCase();
                const filtered = data.filter(row => 
                    Object.values(row).some(val => String(val).toLowerCase().includes(term))
                );
                renderRows(filtered);
            });
        }

        loadSchedule();
    </script>
</body>
</html>
