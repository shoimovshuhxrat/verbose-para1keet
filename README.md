
<!DOCTYPE html>
<html lang="uz">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TM Barber Prime</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href='https://unpkg.com/boxicons@2.1.4/css/boxicons.min.css' rel='stylesheet'>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/dayjs/1.11.10/dayjs.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/dayjs/1.11.10/locale/uz.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/framer-motion@10.16.4/dist/framer-motion.min.js"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;500;600;700&display=swap');

        :root {
            --card-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
            --card-border: 1px solid rgba(255, 255, 255, 0.05);
        }

        body {
            font-family: 'Outfit', sans-serif;
            background: #000000;
            background-image: 
                radial-gradient(at 40% 20%, rgba(234, 88, 12, 0.2) 0px, transparent 50%),
                radial-gradient(at 80% 0%, rgba(249, 115, 22, 0.2) 0px, transparent 50%),
                radial-gradient(at 0% 50%, rgba(245, 158, 11, 0.2) 0px, transparent 50%);
            background-attachment: fixed;
        }

        .glass-morphism {
            background: rgba(17, 17, 17, 0.7);
            backdrop-filter: blur(12px);
            border: var(--card-border);
            box-shadow: var(--card-shadow);
        }

        .modal {
            position: fixed;
            bottom: -100%;
            left: 0;
            right: 0;
            background: rgba(17, 17, 17, 0.95);
            backdrop-filter: blur(20px);
            border-top-left-radius: 2rem;
            border-top-right-radius: 2rem;
            transition: all 0.4s cubic-bezier(0.34, 1.56, 0.64, 1);
            max-height: 90vh;
            overflow-y: auto;
            z-index: 50;
            border-top: var(--card-border);
        }

        .modal.show {
            bottom: 0;
        }

        .overlay {
            position: fixed;
            inset: 0;
            background: rgba(0, 0, 0, 0.8);
            backdrop-filter: blur(8px);
            opacity: 0;
            pointer-events: none;
            transition: all 0.3s ease;
            z-index: 40;
        }

        .overlay.show {
            opacity: 1;
            pointer-events: auto;
        }

        .gradient-text {
            background: linear-gradient(135deg, #f59e0b 0%, #ef4444 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .gradient-border {
            position: relative;
            background: rgba(17, 17, 17, 0.7);
            backdrop-filter: blur(12px);
            transition: all 0.3s cubic-bezier(0.34, 1.56, 0.64, 1);
        }

        .gradient-border::before {
            content: '';
            position: absolute;
            inset: -1px;
            border-radius: inherit;
            padding: 1px;
            background: linear-gradient(135deg, #f59e0b 0%, #ef4444 100%);
            -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
            mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
            -webkit-mask-composite: xor;
            mask-composite: exclude;
        }

        .service-card, .specialist-card, .time-slot {
            background: rgba(255, 255, 255, 0.03);
            border: 1px solid rgba(255, 255, 255, 0.05);
            transition: all 0.3s cubic-bezier(0.34, 1.56, 0.64, 1);
        }

        .service-card:hover, .specialist-card:hover, .time-slot:hover {
            background: rgba(255, 255, 255, 0.05);
            border-color: #f59e0b;
            transform: scale(1.02);
        }

        .service-card:active, .specialist-card:active, .time-slot:active {
            transform: scale(0.98);
        }

        .service-card.selected, .specialist-card.selected, .time-slot.selected {
            background: rgba(245, 158, 11, 0.1);
            border-color: #f59e0b;
        }
   
        .user-menu {
            position: absolute;
            top: 100%;
            right: 0;
            margin-top: 0.5rem;
            width: 12rem;
            border-radius: 0.75rem;
            overflow: hidden;
            z-index: 60;
            animation: slideDown 0.3s cubic-bezier(0.34, 1.56, 0.64, 1) forwards;
        }
        
        @keyframes slideDown {
            from {
                opacity: 0;
                transform: translateY(-10px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        
        .user-menu-item {
            display: flex;
            align-items: center;
            padding: 0.75rem 1rem;
            color: white;
            transition: all 0.2s ease;
        }
        
        .user-menu-item:hover {
            background: rgba(255, 255, 255, 0.1);
        }
        
        .user-menu-item i {
            margin-right: 0.75rem;
        }

        .btn-animate {
            transition: all 0.3s cubic-bezier(0.34, 1.56, 0.64, 1);
        }
        
        .btn-animate:hover {
            transform: scale(1.05);
        }
        
        .btn-animate:active {
            transform: scale(0.95);
        }

        .card-animate {
            transition: all 0.3s cubic-bezier(0.34, 1.56, 0.64, 1);
        }
        
        .card-animate:hover {
            transform: translateY(-10px);
            box-shadow: 0 10px 25px -5px rgba(245, 158, 11, 0.1);
        }


        .close-btn {
            transition: all 0.3s cubic-bezier(0.34, 1.56, 0.64, 1);
        }
        
        .close-btn:hover {
            transform: scale(1.1) rotate(90deg);
        }
        
        .close-btn:active {
            transform: scale(0.9);
        }


        .fade-in {
            animation: fadeIn 0.5s ease forwards;
        }
        
        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .stagger-item {
            opacity: 0;
            transform: translateY(20px);
        }

        
        .calendar {
            display: grid;
            grid-template-columns: repeat(7, 1fr);
            gap: 0.5rem;
        }
        
        .calendar-header {
            display: grid;
            grid-template-columns: repeat(7, 1fr);
            gap: 0.5rem;
            margin-bottom: 0.5rem;
        }
        
        .calendar-day {
            text-align: center;
            color: #9ca3af;
            font-size: 0.875rem;
        }
        
        .calendar-date {
            padding: 0.5rem;
            border-radius: 0.5rem;
            text-align: center;
            cursor: pointer;
            transition: all 0.2s ease;
        }
        
        .calendar-date:hover:not(.disabled) {
            background-color: rgba(255, 255, 255, 0.1);
        }
        
        .calendar-date.today {
            position: relative;
            background: rgba(17, 17, 17, 0.7);
        }
        
        .calendar-date.today::before {
            content: '';
            position: absolute;
            inset: -1px;
            border-radius: inherit;
            padding: 1px;
            background: linear-gradient(135deg, #f59e0b 0%, #ef4444 100%);
            -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
            mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
            -webkit-mask-composite: xor;
            mask-composite: exclude;
        }
        
        .calendar-date.selected {
            background: rgba(245, 158, 11, 0.1);
            border: 1px solid #f59e0b;
        }
        
        .calendar-date.disabled {
            opacity: 0.5;
            cursor: not-allowed;
            color: #6b7280;
        }
    </style>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        primary: '#f59e0b',
                        secondary: '#ef4444',
                    }
                }
            }
        }
    </script>
</head>
<body class="min-h-screen text-white">

    <header class="fixed top-0 left-0 right-0 glass-morphism z-50">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-4">
            <div class="flex justify-between items-center">
                <div class="flex items-center space-x-4">
                    <div class="w-12 h-12 rounded-xl gradient-border flex items-center justify-center btn-animate">
                        <span class="text-xl font-bold gradient-text">TM</span>
                    </div>
                    <h1 class="text-xl font-bold gradient-text">BARBER PRIME</h1>
                </div>
                <div class="relative">
                    <button id="authButton" class="border-2 border-[#f59e0b] px-6 py-2 rounded-xl gradient-border btn-animate relative">
                        <span id="authButtonText">Kirish</span>
                    </button>
                </div>
            </div>
        </div>
    </header>

    <main class="pt-24 px-4 sm:px-6 lg:px-8 max-w-7xl mx-auto">
        <div id="booking-summary" class="rounded-3xl glass-morphism p-6 mb-8 hidden fade-in">
            <div class="flex justify-between items-center mb-4">
                <h3 class="text-2xl font-bold gradient-text">Sizning buyurtmangiz</h3>
                <button id="cancel-booking" class="w-10 h-10 rounded-xl gradient-border flex items-center justify-center close-btn">
                    <i class='bx bx-x text-xl'></i>
                </button>
            </div>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                <div class="space-y-2">
                    <p id="summary-specialist" class="flex justify-between"><span class="text-gray-400">Mutaxassis:</span> <span class="font-medium"></span></p>
                    <p id="summary-datetime" class="flex justify-between"><span class="text-gray-400">Sana va vaqt:</span> <span class="font-medium"></span></p>
                </div>
                <div class="space-y-2">
                    <p id="summary-services" class="flex justify-between"><span class="text-gray-400">Xizmatlar:</span> <span class="font-medium"></span></p>
                    <p id="summary-total" class="flex justify-between"><span class="text-gray-400">Jami:</span> <span class="font-medium"></span></p>
                </div>
            </div>
        </div>

        <section class="relative rounded-3xl overflow-hidden mb-12 glass-morphism h-[240px] fade-in">
            <div class="relative z-10 p-8 sm:p-12">
                <h2 class="text-4xl sm:text-5xl lg:text-6xl font-bold mb-4 gradient-text">
                    TM BARBER PRIME
                </h2>
                <p class="text-xl text-gray-300 mb-8">Abdulla Qodiriy ko'chasi, 1</p>
            </div>
        </section>

        <section class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6 mb-12">
            <div class="glass-morphism rounded-2xl p-6 card-animate stagger-item">
                <div class="w-12 h-12 rounded-xl gradient-border flex items-center justify-center mb-4">
                    <i class='bx bx-user text-2xl'></i>
                </div>
                <h3 class="text-xl font-semibold mb-2">Mutaxassisni tanlash</h3>
                <p class="text-gray-400 mb-4">Professional sartaroshlarimizdan birini tanlang</p>
                <button onclick="showSection('specialists')" 
                    class="w-full px-4 py-2 rounded-xl gradient-border btn-animate">
                    Tanlash
                </button>
            </div>

            <div class="glass-morphism rounded-2xl p-6 card-animate stagger-item">
                <div class="w-12 h-12 rounded-xl gradient-border flex items-center justify-center mb-4">
                    <i class='bx bx-calendar text-2xl'></i>
                </div>
                <h3 class="text-xl font-semibold mb-2">Vaqtni tanlash</h3>
                <p class="text-gray-400 mb-4">O'zingizga qulay vaqtni tanlang</p>
                <button onclick="showSection('datetime')" 
                    class="w-full px-4 py-2 rounded-xl gradient-border btn-animate">
                    Tanlash
                </button>
            </div>

            <div class="glass-morphism rounded-2xl p-6 card-animate stagger-item">
                <div class="w-12 h-12 rounded-xl gradient-border flex items-center justify-center mb-4">
                    <i class='bx bx-menu text-2xl'></i>
                </div>
                <h3 class="text-xl font-semibold mb-2">Xizmatlarni tanlash</h3>
                <p class="text-gray-400 mb-4">Kerakli xizmatlarni tanlang</p>
                <button onclick="showSection('services')" 
                    class="w-full px-4 py-2 rounded-xl gradient-border btn-animate">
                    Tanlash
                </button>
            </div>
        </section>
    </main>

    <div id="specialists-modal" class="modal">
        <div class="p-6">
            <div class="flex items-center justify-between mb-8">
                <h2 class="text-2xl font-bold">Mutaxassisni tanlash</h2>
                <button onclick="hideModal('specialists-modal')" class="w-10 h-10 rounded-xl gradient-border flex items-center justify-center close-btn">
                    <i class='bx bx-x text-2xl'></i>
                </button>
            </div>
            <div id="specialists-container" class="space-y-4">
            </div>
            <button id="specialists-next" onclick="showSection('datetime')" 
                class="w-full mt-6 px-6 py-3 rounded-xl gradient-border btn-animate hidden">
                Davom etish
            </button>
        </div>
    </div>

    <div id="datetime-modal" class="modal">
        <div class="p-6">
            <div class="flex items-center justify-between mb-8">
                <h2 class="text-2xl font-bold">Vaqtni tanlash</h2>
                <button onclick="hideModal('datetime-modal')" class="w-10 h-10 rounded-xl gradient-border flex items-center justify-center close-btn">
                    <i class='bx bx-x text-2xl'></i>
                </button>
            </div>
            <div id="calendar" class="glass-morphism rounded-xl p-4 mb-6 fade-in">
            </div>
            <div id="time-slots" class="grid grid-cols-3 sm:grid-cols-4 gap-4">
            </div>
            <button id="datetime-next" onclick="showSection('services')" 
                class="w-full mt-6 px-6 py-3 rounded-xl gradient-border btn-animate hidden">
                Davom etish
            </button>
        </div>
    </div>


    <div id="services-modal" class="modal">
        <div class="p-6 pb-24">
            <div class="flex items-center justify-between mb-8">
                <h2 class="text-2xl font-bold">Xizmatlarni tanlash</h2>
                <button onclick="hideModal('services-modal')" class="w-10 h-10 rounded-xl gradient-border flex items-center justify-center close-btn">
                    <i class='bx bx-x text-2xl'></i>
                </button>
            </div>
            <div class="relative mb-6 fade-in">
                <i class='bx bx-search absolute left-4 top-1/2 -translate-y-1/2 text-gray-400'></i>
                <input type="text" id="serviceSearch" placeholder="Xizmatni qidirish" 
                    class="w-full pl-12 pr-4 py-3 rounded-xl glass-morphism">
            </div>
            <div id="services-container" class="space-y-4">
            </div>
            <div id="total-price-container" class=" bottom-0 left-0 right-0 glass-morphism p-6 hidden">
                <div class="flex justify-between items-center mb-4">
                    <span class="text-lg">Jami:</span>
                    <span id="total-price" class="text-2xl font-bold">0 so'm</span>
                </div>
                <button id="confirmServices" class="w-full py-3 rounded-xl gradient-border btn-animate font-medium">
                    Tasdiqlash
                </button>
            </div>
        </div>
    </div>

    <div id="auth-modal" class="modal">
        <div class="p-6">
            <div class="flex items-center justify-between mb-8">
                <h2 class="text-2xl font-bold">Ro'yxatdan o'tish</h2>
                <button onclick="hideModal('auth-modal')" class="w-10 h-10 rounded-xl gradient-border flex items-center justify-center close-btn">
                    <i class='bx bx-x text-2xl'></i>
                </button>
            </div>
            <form id="auth-form" class="space-y-6">
                <div>
                    <label for="firstName" class="block text-sm font-medium mb-2">Ism</label>
                    <input type="text" id="firstName" required class="w-full px-4 py-3 rounded-xl glass-morphism">
                </div>
                <div>
                    <label for="lastName" class="block text-sm font-medium mb-2">Familiya</label>
                    <input type="text" id="lastName" required class="w-full px-4 py-3 rounded-xl glass-morphism">
                </div>
                <div>
                    <label for="phone" class="block text-sm font-medium mb-2">Telefon</label>
                    <input type="tel" id="phone" required pattern="^\+998[0-9]{9}$" placeholder="+998" 
                        class="w-full px-4 py-3 rounded-xl glass-morphism">
                </div>
                <div class="flex items-center gap-2">
                    <input type="checkbox" id="terms" required class="w-4 h-4 rounded glass-morphism">
                    <label for="terms" class="text-sm text-gray-400">
                        Shaxsiy ma'lumotlarni qayta ishlashga rozilik bildiraman
                    </label>
                </div>
                <button type="submit" class="w-full py-3 rounded-xl gradient-border btn-animate font-medium">
                    Ro'yxatdan o'tish
                </button>
            </form>
        </div>
    </div>

    <div id="cancel-confirmation-modal" class="modal">
        <div class="p-6">
            <div class="flex items-center justify-between mb-8">
                <h2 class="text-2xl font-bold">Buyurtmani bekor qilish</h2>
                <button onclick="hideModal('cancel-confirmation-modal')" class="w-10 h-10 rounded-xl gradient-border flex items-center justify-center close-btn">
                    <i class='bx bx-x text-2xl'></i>
                </button>
            </div>
            <p class="text-lg mb-8">Siz haqiqatan ham buyurtmani bekor qilmoqchimisiz?</p>
            <div class="flex gap-4">
                <button onclick="hideModal('cancel-confirmation-modal')" 
                    class="flex-1 py-3 rounded-xl glass-morphism hover:bg-white/10 transition-colors">
                    Yo'q
                </button>
                <button onclick="confirmCancellation()" 
                    class="flex-1 py-3 rounded-xl gradient-border btn-animate">
                    Ha
                </button>
            </div>
        </div>
    </div>

    <div id="logout-confirmation-modal" class="modal">
        <div class="p-6">
            <div class="flex items-center justify-between mb-8">
                <h2 class="text-2xl font-bold">Hisobdan chiqish</h2>
                <button onclick="hideModal('logout-confirmation-modal')" class="w-10 h-10 rounded-xl gradient-border flex items-center justify-center close-btn">
                    <i class='bx bx-x text-2xl'></i>
                </button>
            </div>
            <p class="text-lg mb-8">Siz haqiqatan ham hisobingizdan chiqmoqchimisiz?</p>
            <div class="flex gap-4">
                <button onclick="hideModal('logout-confirmation-modal')" 
                    class="flex-1 py-3 rounded-xl glass-morphism hover:bg-white/10 transition-colors">
                    Yo'q
                </button>
                <button onclick="confirmLogout()" 
                    class="flex-1 py-3 rounded-xl gradient-border btn-animate">
                    Ha
                </button>
            </div>
        </div>
    </div>

    <div id="overlay" class="overlay"></div>

    <script>
        let currentStep = 1;
        let selectedSpecialist = '';
        let selectedDate = '';
        let selectedTime = '';
        let selectedServices = [];
        let isAuthenticated = false;
        let userData = null;
        let bookingConfirmed = false;
        let userMenuVisible = false;

        // Animate staggered items on load
        document.addEventListener('DOMContentLoaded', function() {
            // Animate staggered items
            const staggerItems = document.querySelectorAll('.stagger-item');
            staggerItems.forEach((item, index) => {
                setTimeout(() => {
                    item.style.animation = `fadeIn 0.5s ease forwards ${0.2 + (index * 0.1)}s`;
                }, 100);
            });

            // Load user data
            const storedUserData = localStorage.getItem('userData');
            if (storedUserData) {
                userData = JSON.parse(storedUserData);
                isAuthenticated = true;
            }
            updateAuthButton();
            
            // Load booking data
            const storedBooking = localStorage.getItem('confirmedBooking');
            if (storedBooking) {
                const booking = JSON.parse(storedBooking);
                selectedSpecialist = booking.specialist;
                selectedDate = booking.date;
                selectedTime = booking.time;
                selectedServices = booking.services;
                bookingConfirmed = true;
                updateBookingSummary();
            }

            // Render specialists and services
            renderSpecialists();
            renderServices();
        });

        function showSection(section) {
            if (!isAuthenticated) {
                showModal('auth-modal');
                return;
            }
            showModal(`${section}-modal`);
        }

        function showModal(modalId) {
            const modal = document.getElementById(modalId);
            const overlay = document.getElementById('overlay');
            
            modal.style.display = 'block';
            overlay.classList.add('show');
            
            setTimeout(() => {
                modal.classList.add('show');
            }, 10);

            if (modalId === 'datetime-modal') {
                renderCalendar();
            }
        }

        function hideModal(modalId) {
            const modal = document.getElementById(modalId);
            const overlay = document.getElementById('overlay');
            
            modal.classList.remove('show');
            overlay.classList.remove('show');
            
            setTimeout(() => {
                modal.style.display = 'none';
            }, 300);
        }

        function selectSpecialist(element, name) {
            document.querySelectorAll('.specialist-card').forEach(card => {
                card.classList.remove('selected');
            });
            element.classList.add('selected');
            selectedSpecialist = name;
            document.getElementById('specialists-next').classList.remove('hidden');
        }

        function renderCalendar() {
            const calendar = document.getElementById('calendar');
            const today = dayjs();
            dayjs.locale('uz');
            
            let calendarHTML = `
                <div class="calendar-header">
                    ${['Du', 'Se', 'Ch', 'Pa', 'Ju', 'Sh', 'Ya'].map(day => 
                        `<div class="calendar-day">${day}</div>`
                    ).join('')}
                </div>
                <div class="calendar">
            `;

            const startOfMonth = today.startOf('month');
            const endOfMonth = today.endOf('month');
            const daysInPreviousMonth = startOfMonth.day();

            for (let i = 0; i < daysInPreviousMonth; i++) {
                calendarHTML += '<div></div>';
            }

            for (let date = startOfMonth; date.isBefore(endOfMonth.add(1, 'day')); date = date.add(1, 'day')) {
                const isToday = date.isSame(today, 'day');
                const isPast = date.isBefore(today, 'day'); 
                const isSelected = date.format('YYYY-MM-DD') === selectedDate;
                
                calendarHTML += `
                    <button 
                        onclick="${isPast ? '' : `selectDate(this, '${date.format('YYYY-MM-DD')}')`}"
                        class="calendar-date ${
                            isPast ? 'disabled' : 
                            isToday ? 'today' : 
                            isSelected ? 'selected' : ''
                        }"
                        ${isPast ? 'disabled' : ''}
                    >
                        ${date.date()}
                    </button>
                `;
            }

            calendarHTML += '</div>';
            calendar.innerHTML = calendarHTML;

            if (selectedDate) {
                renderTimeSlots();
            }
        }

        function selectDate(element, date) {
            document.querySelectorAll('.calendar-date').forEach(btn => {
                btn.classList.remove('selected');
                btn.classList.remove('today');
            });
            element.classList.add('selected');
            selectedDate = date;
            renderTimeSlots();
        }

        function renderTimeSlots() {
            const timeSlots = [
                '10:00', '10:30', '11:00', '11:30', '12:00', '12:30',
                '13:00', '13:30', '14:00', '14:30', '15:00', '15:30',
                '16:00', '16:30', '17:00', '17:30', '18:00', '18:30'
            ];
            
            const container = document.getElementById('time-slots');
            container.innerHTML = '';
            
            timeSlots.forEach((time, index) => {
                const isSelected = time === selectedTime;
                const button = document.createElement('button');
                button.className = `time-slot p-3 rounded-lg text-center ${isSelected ? 'selected' : ''}`;
                button.onclick = () => selectTime(button, time);
                button.textContent = time;
         
                button.style.opacity = '0';
                button.style.transform = 'scale(0.9)';
                
                setTimeout(() => {
                    button.style.transition = 'all 0.3s cubic-bezier(0.34, 1.56, 0.64, 1)';
                    button.style.opacity = '1';
                    button.style.transform = 'scale(1)';
                }, 100 + (index * 20));
                
                container.appendChild(button);
            });
            
            if (selectedTime) {
                document.getElementById('datetime-next').classList.remove('hidden');
            }
        }

        function selectTime(element, time) {
            document.querySelectorAll('.time-slot').forEach(slot => {
                slot.classList.remove('selected');
            });
            element.classList.add('selected');
            selectedTime = time;
            document.getElementById('datetime-next').classList.remove('hidden');
        }

        function selectService(element, name, price) {
            element.classList.toggle('selected');
            
            if (element.classList.contains('selected')) {
                selectedServices.push({ name, price });
            } else {
                selectedServices = selectedServices.filter(service => service.name !== name);
            }
            
            updateTotalPrice();
        }

        function updateTotalPrice() {
            const total = selectedServices.reduce((sum, service) => sum + service.price, 0);
            const totalContainer = document.getElementById('total-price-container');
            const totalElement = document.getElementById('total-price');
            
            if (selectedServices.length > 0) {
                totalContainer.classList.remove('hidden');
                totalElement.textContent = `${total.toLocaleString()} so'm`;
            } else {
                totalContainer.classList.add('hidden');
            }
        }

        document.getElementById('auth-form').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const firstName = document.getElementById('firstName').value;
            const lastName = document.getElementById('lastName').value;
            const phone = document.getElementById('phone').value;

            userData = { firstName, lastName, phone };
            isAuthenticated = true;
            
            localStorage.setItem('userData', JSON.stringify(userData));
            
            updateAuthButton();
            
            hideModal('auth-modal');
            showModal('specialists-modal');
        });

        function updateAuthButton() {
            const authButton = document.getElementById('authButton');
            const authButtonText = document.getElementById('authButtonText');
            
            if (isAuthenticated && userData) {
                authButtonText.textContent = `${userData.firstName} ${userData.lastName}`;
                authButton.classList.add('gradient-border');
                authButton.onclick = showUserMenu;
            } else {
                authButtonText.textContent = 'Kirish';
                authButton.classList.remove('gradient-border');
                authButton.onclick = () => showModal('auth-modal');
            }
        }

        function showUserMenu() {
            const existingMenu = document.querySelector('.user-menu');
            if (existingMenu) {
                existingMenu.remove();
                return;
            }
         
            const userMenu = document.createElement('div');
            userMenu.className = 'user-menu glass-morphism';
            userMenu.innerHTML = `
                <div class="p-4 border-b border-white/10">
                    <div class="flex items-center gap-3">
                        <div class="w-10 h-10 rounded-full gradient-border flex items-center justify-center">
                            <i class='bx bx-user text-xl'></i>
                        </div>
                        <div>
                            <p class="font-medium">${userData.firstName} ${userData.lastName}</p>
                            <p class="text-sm text-gray-400">${userData.phone}</p>
                        </div>
                    </div>
                </div>
                <div class="py-2">
                    <a href="#" class="user-menu-item" onclick="showLogoutConfirmation(); return false;">
                        <i class='bx bx-log-out text-xl'></i>
                        <span>Chiqish</span>
                    </a>
                </div>
            `;
            
            const authButton = document.getElementById('authButton');
            authButton.appendChild(userMenu);

            setTimeout(() => {
                document.addEventListener('click', function closeMenu(e) {
                    if (!userMenu.contains(e.target) && e.target !== authButton) {
                        userMenu.remove();
                        document.removeEventListener('click', closeMenu);
                    }
                });
            }, 10);
        }

        function showLogoutConfirmation() {
            const existingMenu = document.querySelector('.user-menu');
            if (existingMenu) {
                existingMenu.remove();
            }
            showModal('logout-confirmation-modal');
        }

        function confirmLogout() {
            logout();
            hideModal('logout-confirmation-modal');
        }

        function logout() {
            isAuthenticated = false;
            userData = null;
            localStorage.removeItem('userData');
            updateAuthButton();
            resetBooking();
        }

        const specialists = [
            { name: 'Элеонора', role: 'Мастер ногтевого сервиса', rating: 4.8, reviews: 127 },
            { name: 'Хаким', role: 'Барбер', rating: 4.9, reviews: 93 },
            { name: 'Азиза', role: 'Стилист', rating: 4.7, reviews: 156 }
        ];

        function renderSpecialists() {
            const container = document.getElementById('specialists-container');
            container.innerHTML = '';
            
            specialists.forEach((specialist, index) => {
                const div = document.createElement('div');
                div.className = `specialist-card glass-morphism p-6 rounded-xl cursor-pointer ${selectedSpecialist === specialist.name ? 'selected' : ''}`;
                div.onclick = () => selectSpecialist(div, specialist.name);
                
                div.innerHTML = `
                    <div class="flex items-center gap-4">
                        <div class="w-16 h-16 rounded-xl gradient-border flex items-center justify-center">
                            <i class='bx bx-user text-2xl'></i>
                        </div>
                        <div>
                            <h3 class="text-lg font-semibold">${specialist.name}</h3>
                            <p class="text-sm text-gray-400">${specialist.role}</p>
                            <div class="flex items-center gap-2 mt-1">
                                <i class='bx bxs-star text-yellow-400'></i>
                                <span class="text-sm">${specialist.rating}</span>
                                <span class="text-sm text-gray-400">(${specialist.reviews} отзывов)</span>
                            </div>
                        </div>
                    </div>
                `;
                
                div.style.opacity = '0';
                div.style.transform = 'translateY(20px)';
                
                setTimeout(() => {
                    div.style.transition = 'all 0.3s cubic-bezier(0.34, 1.56, 0.64, 1)';
                    div.style.opacity = '1';
                    div.style.transform = 'translateY(0)';
                }, 100 + (index * 100));
                
                container.appendChild(div);
            });
            
            if (selectedSpecialist) {
                document.getElementById('specialists-next').classList.remove('hidden');
            }
        }

        const services = [
            { name: 'Мужская стрижка', duration: '1 час', price: 150000 },
            { name: 'Бритье бороды', duration: '30 минут', price: 100000 },
            { name: 'Укладка волос', duration: '45 минут', price: 80000 },
            { name: 'Детская стрижка', duration: '45 минут', price: 120000 },
            { name: 'Окрашивание', duration: '2 часа', price: 250000 }
        ];

        function renderServices() {
            const container = document.getElementById('services-container');
            container.innerHTML = '';
            
            const searchTerm = document.getElementById('serviceSearch')?.value?.toLowerCase() || '';
            const filteredServices = services.filter(service => 
                service.name.toLowerCase().includes(searchTerm)
            );
            
            filteredServices.forEach((service, index) => {
                const div = document.createElement('div');
                div.className = `service-card p-6 rounded-xl cursor-pointer ${selectedServices.some(s => s.name === service.name) ? 'selected' : ''}`;
                div.onclick = () => selectService(div, service.name, service.price);
                
                div.innerHTML = `
                    <div class="flex justify-between items-center">
                        <div>
                            <h3 class="text-lg font-semibold">${service.name}</h3>
                            <p class="text-sm text-gray-400">${service.duration}</p>
                        </div>
                        <div class="text-right">
                            <p class="font-bold">${service.price.toLocaleString()} so'm</p>
                        </div>
                    </div>
                `;
                
                // Add animation with delay based on index
                div.style.opacity = '0';
                div.style.transform = 'translateY(20px)';
                
                setTimeout(() => {
                    div.style.transition = 'all 0.3s cubic-bezier(0.34, 1.56, 0.64, 1)';
                    div.style.opacity = '1';
                    div.style.transform = 'translateY(0)';
                }, 100 + (index * 100));
                
                container.appendChild(div);
            });
            
            updateTotalPrice();
        }

        document.getElementById('serviceSearch')?.addEventListener('input', renderServices);

        document.getElementById('confirmServices')?.addEventListener('click', function() {
            if (!selectedSpecialist || !selectedDate || !selectedTime || selectedServices.length === 0) {
                alert('Iltimos, barcha maydonlarni to\'ldiring');
                return;
            }

            const totalPrice = selectedServices.reduce((sum, service) => sum + service.price, 0);
            
            const message = `
🆕 *Yangi buyurtma*

👤 *Mijoz ma'lumotlari:*
- Ism-familiya: ${userData.firstName} ${userData.lastName}
- Telefon: ${userData.phone}

💈 *Buyurtma ma'lumotlari:*
- Sartarosh: ${selectedSpecialist}
- Sana: ${selectedDate}
- Vaqt: ${selectedTime}

✂️ *Tanlangan xizmatlar:*
${selectedServices.map(service => `- ${service.name} - ${service.price.toLocaleString()} so'm`).join('\n')}

💰 *Umumiy narx:* ${totalPrice.toLocaleString()} so'm`;

            const botToken = '7758261570:AAGG1bZeHVsey-xRZqACn8ZKYquYQ6UxaOA';
            const chatId = '7675613595';

            fetch(`https://api.telegram.org/bot${botToken}/sendMessage`, {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                },
                body: JSON.stringify({
                    chat_id: chatId,
                    text: message,
                    parse_mode: 'Markdown'
                })
            })
            .then(response => response.json())
            .then(data => {
                if (data.ok) {
                    bookingConfirmed = true;
                    
                    const booking = {
                        specialist: selectedSpecialist,
                        date: selectedDate,
                        time: selectedTime,
                        services: selectedServices
                    };
                    localStorage.setItem('confirmedBooking', JSON.stringify(booking));
                    
                    updateBookingSummary();
                    resetModals();
                } else {
                    alert('Xatolik yuz berdi. Iltimos, qayta urinib ko\'ring.');
                }
            })
            .catch(error => {
                console.error('Error:', error);
                alert('Xatolik yuz berdi. Iltimos, qayta urinib ko\'ring.');
            });
        });

        function updateBookingSummary() {
            if (!bookingConfirmed) return;
            
            const summaryElement = document.getElementById('booking-summary');
            const specialistElement = document.getElementById('summary-specialist');
            const datetimeElement = document.getElementById('summary-datetime');
            const servicesElement = document.getElementById('summary-services');
            const totalElement = document.getElementById('summary-total');
            
            specialistElement.querySelector('span.font-medium').textContent = selectedSpecialist;
            datetimeElement.querySelector('span.font-medium').textContent = `${selectedDate}, ${selectedTime}`;
            
            const serviceNames = selectedServices.map(service => service.name).join(', ');
            servicesElement.querySelector('span.font-medium').textContent = serviceNames;
            
            const totalPrice = selectedServices.reduce((sum, service) => sum + service.price, 0);
            totalElement.querySelector('span.font-medium').textContent = `${totalPrice.toLocaleString()} so'm`;
            
            summaryElement.classList.remove('hidden');
            
            // Add animation
            summaryElement.style.animation = 'fadeIn 0.5s ease forwards';
        }

        document.getElementById('cancel-booking')?.addEventListener('click', function() {
            showModal('cancel-confirmation-modal');
        });

        function confirmCancellation() {
            if (!bookingConfirmed) return;
            const botToken = '7758261570:AAGG1bZeHVsey-xRZqACn8ZKYquYQ6UxaOA';
            const chatId = '7675613595';
            
            const totalPrice = selectedServices.reduce((sum, service) => sum + service.price, 0);
            
            const message = `
❌ *Buyurtma bekor qilindi*

👤 *Mijoz ma'lumotlari:*
- Ism-familiya: ${userData.firstName} ${userData.lastName}
- Telefon: ${userData.phone}

💈 *Bekor qilingan buyurtma ma'lumotlari:*
- Sartarosh: ${selectedSpecialist}
- Sana: ${selectedDate}
- Vaqt: ${selectedTime}

✂️ *Tanlangan xizmatlar:*
${selectedServices.map(service => `- ${service.name} - ${service.price.toLocaleString()} so'm`).join('\n')}

💰 *Umumiy narx:* ${totalPrice.toLocaleString()} so'm`;

            fetch(`https://api.telegram.org/bot${botToken}/sendMessage`, {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                },
                body: JSON.stringify({
                    chat_id: chatId,
                    text: message,
                    parse_mode: 'Markdown'
                })
            })
            .then(response => response.json())
            .then(data => {
                if (data.ok) {
                    resetBooking();
                    hideModal('cancel-confirmation-modal');
                } else {    
                    alert('Xatolik yuz berdi. Iltimos, qayta urinib ko\'ring.');
                }
            })
            .catch(error => {
                console.error('Error:', error);
                alert('Xatolik yuz berdi. Iltimos, qayta urinib ko\'ring.');
            });
        }

        function resetModals() {
            document.querySelectorAll('.modal').forEach(modal => {
                modal.classList.remove('show');
                setTimeout(() => {
                    modal.style.display = 'none';
                }, 300);
            });
            
            document.getElementById('overlay').classList.remove('show');
        }

        function resetBooking() {
            selectedSpecialist = '';
            selectedDate = '';
            selectedTime = '';
            selectedServices = [];
            bookingConfirmed = false;
            
            localStorage.removeItem('confirmedBooking');
            
            document.getElementById('booking-summary').classList.add('hidden');
            
            document.querySelectorAll('.selected').forEach(el => el.classList.remove('selected'));
            document.querySelectorAll('.gradient-border').forEach(el => {
                if (!el.id.includes('authButton')) {
                    el.classList.remove('gradient-border');
                }
            });
            
            document.getElementById('specialists-next').classList.add('hidden');
            document.getElementById('datetime-next').classList.add('hidden');
            document.getElementById('total-price-container').classList.add('hidden');
            
            resetModals();
        }
    </script>
</body>
</html>              m  m  
