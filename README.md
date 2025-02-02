<!DOCTYPE html>
<html lang="fa">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>شرکت برادران استوی</title>
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css">
    <style>
        body {
            direction: rtl;
            text-align: right;
            padding: 20px;
        }
        table {
            width: 100%;
            border-collapse: collapse;
        }
        table, th, td {
            border: 1px solid black;
        }
        th, td {
            padding: 10px;
            text-align: center;
        }
    </style>
</head>
<body>
    <h1 class="text-center">شرکت برادران استوی</h1>
    <form id="workerForm">
        <div class="form-group">
            <label for="name">نام:</label>
            <input type="text" class="form-control" id="name" required>
        </div>
        <div class="form-group">
            <label for="hours">ساعات کار:</label>
            <input type="number" class="form-control" id="hours" required>
        </div>
        <div class="form-group">
            <label for="description">شرح کار:</label>
            <input type="text" class="form-control" id="description" required>
        </div>
        <button type="submit" class="btn btn-primary">افزودن</button>
    </form>
    <table id="workersTable" class="table mt-4">
        <thead>
            <tr>
                <th>نام</th>
                <th>ساعات کار</th>
                <th>تاریخ</th>
                <th>شرح کار</th>
                <th>دستمزد</th>
            </tr>
        </thead>
        <tbody>
        </tbody>
    </table>
    <h2>کل دستمزد کارگران: <span id="totalWage">0</span> تومان</h2>

    <script src="https://code.jquery.com/jquery-3.5.1.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/moment.js/2.29.1/moment.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/moment-jalaali/0.9.2/moment-jalaali.js"></script>
    <script>
        const hourlyRate = 100000;

        $(document).ready(function() {
            $('#workerForm').on('submit', function(e) {
                e.preventDefault();

                const name = $('#name').val();
                const hours = parseInt($('#hours').val(), 10);
                const description = $('#description').val();
                const date = moment().format('jYYYY/jMM/jDD');
                const wage = hours * hourlyRate;

                const newRow = `<tr>
                    <td>${name}</td>
                    <td>${hours}</td>
                    <td>${date}</td>
                    <td>${description}</td>
                    <td class="wage">${wage}</td>
                </tr>`;

                $('#workersTable tbody').append(newRow);

                updateTotalWage();
                $('#workerForm')[0].reset();
            });

            function updateTotalWage() {
                let totalWage = 0;
                $('#workersTable tbody tr').each(function() {
                    totalWage += parseInt($(this).find('.wage').text(), 10);
                });
                $('#totalWage').text(totalWage);
            }
        });
    </script>
</body>
</html>
