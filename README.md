<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="الحاج منصور المشرقي للتفصيل - أفضل خدمة تفصيل وخياطة في الإسكندرية">
    <title>ترزي السلام</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #e1f5fe, #b3e5fc);
            margin: 0;
            padding: 0;
            display: flex;
            flex-direction: column;
            align-items: center;
            animation: waveBackground 10s infinite;
            color: #333;
        }

        @keyframes waveBackground {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        header {
            background-color: #29b6f6;
            color: white;
            padding: 20px;
            width: 100%;
            text-align: center;
            border-bottom: 5px solid #0288d1;
        }

        .container {
            width: 90%;
            max-width: 600px;
            background-color: #ffffff;
            padding: 20px;
            margin-top: 20px;
            border-radius: 12px;
            box-shadow: 0 8px 16px rgba(0, 0, 0, 0.1);
        }

        .search-section, .add-section, .login-section {
            margin-bottom: 20px;
        }

        .search-section input, .add-section input, .login-section input {
            width: calc(100% - 120px);
            padding: 12px;
            margin-right: 10px;
            border: 1px solid #b3e5fc;
            border-radius: 8px;
            font-size: 1rem;
        }

        .search-section button, .add-section button, .login-section button {
            padding: 12px;
            background-color: #29b6f6;
            color: white;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-size: 1rem;
            transition: background-color 0.3s;
        }

        .search-section button:hover, .add-section button:hover, .login-section button:hover {
            background-color: #0288d1;
        }

        .result {
            padding: 12px;
            border-radius: 8px;
            margin-top: 10px;
            font-size: 1.1rem;
        }

        .result.done {
            background-color: #c8e6c9;
            color: #2e7d32;
        }

        .result.not-done {
            background-color: #ffcdd2;
            color: #c62828;
        }

        .name-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-top: 10px;
        }

        .name-item button {
            padding: 8px;
            background-color: #29b6f6;
            color: white;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-size: 0.9rem;
            transition: background-color 0.3s;
        }

        .name-item button.done {
            background-color: #4caf50;
        }

        .name-item button.not-done {
            background-color: #f44336;
        }

        .name-item button.delete {
            background-color: #d32f2f;
            margin-left: 10px;
        }

        footer {
            margin-top: 20px;
            padding: 20px;
            width: 100%;
            text-align: center;
            background-color: #29b6f6;
            color: white;
            border-top: 5px solid #0288d1;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        footer a {
            color: white;
            text-decoration: none;
            font-size: 1.2rem;
        }

        .phone-icon {
            width: 40px;
            height: 40px;
            background-color: #0288d1;
            color: white;
            display: flex;
            justify-content: center;
            align-items: center;
            border-radius: 50%;
            font-size: 1.5rem;
            cursor: pointer;
            transition: background-color 0.3s;
        }

        .phone-icon:hover {
            background-color: #01579b;
        }

        .owner-tools {
            display: none;
        }
    </style>
</head>
<body>

<header>
    <h1>ترزي السلام</h1>
</header>

<div class="container">
    <!-- قسم تسجيل الدخول للمالك -->
    <div class="login-section">
        <input type="password" id="passwordInput" placeholder="أدخل كلمة المرور">
        <button onclick="login()">تسجيل دخول</button>
    </div>

    <!-- قسم البحث -->
    <div class="search-section">
        <input type="text" id="searchInput" placeholder="أدخل الاسم أو رقم الصفحة">
        <button onclick="searchName()">بحث</button>
        <div id="searchResult" class="result"></div>
    </div>

    <!-- قسم إضافة الأسماء -->
    <div class="add-section owner-tools">
        <input type="text" id="newName" placeholder="أدخل الاسم">
        <input type="text" id="newPageNumber" placeholder="أدخل رقم الصفحة">
        <button onclick="addName()">إضافة اسم</button>
    </div>

    <!-- قائمة الأسماء للمالك -->
    <div id="ownerNamesList" class="owner-tools">
        <h3>قائمة الأسماء</h3>
    </div>
</div>

<footer>
    <div class="phone-icon" onclick="window.location.href='tel:034480090'">
        &#9742;
    </div>
    <div>
        <a href="tel:034480090">اتصل بنا: 034480090</a>
        <p>الإسكندرية - العامرية - سوق المغاربة</p>
        <p>مواعيد العمل: من 10 صباحًا إلى بعد المغرب</p>
    </div>
</footer>

<script>
    // قاعدة بيانات الأسماء الافتراضية
    let names = [
        { name: 'أحمد محمد', pageNumber: '1', done: false },
        { name: 'علي حسن', pageNumber: '2', done: true },
        { name: 'سارة عبد الله', pageNumber: '3', done: false }
    ];

    // أسماء المالك التي تم إضافتها
    let ownerAddedNames = [];

    // كلمة مرور المالك (يمكن تغييرها حسب الرغبة)
    const ownerPassword = '1234';

    // تسجيل الدخول للمالك
    function login() {
        const passwordInput = document.getElementById('passwordInput').value;
        if (passwordInput === ownerPassword) {
            document.querySelectorAll('.owner-tools').forEach(el => el.style.display = 'block');
            document.querySelector('.login-section').style.display = 'none';
        } else {
            alert('كلمة المرور غير صحيحة.');
        }
    }

    // عرض قائمة الأسماء للمالك
    function displayOwnerNames() {
        const ownerNamesList = document.getElementById('ownerNamesList');
        ownerNamesList.innerHTML = '<h3>قائمة الأسماء</h3>';
        ownerAddedNames.forEach((nameObj, index) => {
            const nameDiv = document.createElement('div');
            nameDiv.className = 'name-item';
            nameDiv.innerHTML = `
                ${nameObj.name} - صفحة: ${nameObj.pageNumber}
                <button onclick="toggleDone(${index})" class="${nameObj.done ? 'done' : 'not-done'}">
                    ${nameObj.done ? 'تم الانتهاء' : 'لم يتم الانتهاء'}
                </button>
                <button onclick="deleteName(${index})" class="delete">حذف</button>
            `;
            ownerNamesList.appendChild(nameDiv);
        });
    }

    // البحث عن اسم
    function searchName() {
        const searchInput = document.getElementById('searchInput').value.toLowerCase();
        const searchResult = document.getElementById('searchResult');
        let found = names.filter(nameObj => nameObj.name.toLowerCase().includes(searchInput));

        if (found.length > 0) {
            searchResult.innerHTML = '';
            found.forEach(nameObj => {
                const resultDiv = document.createElement('div');
                resultDiv.className = 'result ' + (nameObj.done ? 'done' : 'not-done');
                resultDiv.innerHTML = `${nameObj.name} - ${nameObj.done ? 'تم الانتهاء' : 'لم يتم الانتهاء'}`;
                searchResult.appendChild(resultDiv);
            });
        } else {
            searchResult.innerHTML = 'لا يوجد اسم مطابق.';
        }
    }

    // إضافة اسم جديد
    function addName() {
        const newNameInput = document.getElementById('newName').value.trim();
        const newPageNumberInput = document.getElementById('newPageNumber').value.trim();
        if (newNameInput && newPageNumberInput) {
            ownerAddedNames.push({ name: newNameInput, pageNumber: newPageNumberInput, done: false });
            names.push({ name: newNameInput, pageNumber: newPageNumberInput, done: false }); // إضافة الاسم لقائمة البحث
            displayOwnerNames();
            document.getElementById('newName').value = '';
            document.getElementById('newPageNumber').value = '';
        } else {
            alert('يرجى إدخال الاسم ورقم الصفحة.');
        }
    }

    // تغيير حالة الانتهاء (خاص بالأسماء المضافة فقط من المالك)
    function toggleDone(index) {
        ownerAddedNames[index].done = !ownerAddedNames[index].done;
        displayOwnerNames();
    }

    // حذف اسم من القائمة
    function deleteName(index) {
        ownerAddedNames.splice(index, 1);
        displayOwnerNames();
    }

    // عرض الأسماء عند تحميل الصفحة
    displayOwnerNames();
</script>

</body>
</html>
