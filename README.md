<!DOCTYPE html>
<html lang="en" id="html">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>LERS - The Future Currency</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- GSAP CDN للتأثيرات المتحركة -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/gsap.min.js"></script>
    <!-- Three.js CDN لتأثيرات الخلفية ثلاثية الأبعاد -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <!-- Font Awesome للأيقونات -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.2/css/all.min.css">
    <style>
        body {
            font-family: 'Cairo', sans-serif;
            background: linear-gradient(135deg, #1e3a8a, #3b82f6);
            color: white;
            overflow-x: hidden;
            margin: 0;
        }
        #canvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            opacity: 0.6;
        }
        .hero-section {
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            position: relative;
            z-index: 1;
        }
        .hero-section::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: radial-gradient(circle, rgba(255,255,255,0.1), transparent);
            z-index: 0;
        }
        .btn-reserve {
            background: linear-gradient(90deg, #f59e0b, #f97316);
            transition: transform 0.3s, box-shadow 0.3s;
            border: 2px solid #f97316;
        }
        .btn-reserve:hover {
            transform: scale(1.05);
            box-shadow: 0 0 30px rgba(249, 115, 22, 0.7);
        }
        .menu-btn {
            background: linear-gradient(90deg, #3b82f6, #1e40af);
            transition: all 0.3s;
            border: 2px solid #3b82f6;
            opacity: 1 !important; /* لضمان الظهور */
        }
        .menu-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 20px rgba(59, 130, 246, 0.7);
        }
        .social-icon {
            transition: transform 0.3s;
        }
        .social-icon:hover {
            transform: scale(1.2);
        }
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.8);
            justify-content: center;
            align-items: center;
            z-index: 1000;
        }
        .modal-content {
            background: #1e3a8a;
            padding: 2rem;
            border-radius: 15px;
            text-align: center;
            max-width: 400px;
            width: 90%;
            border: 2px solid #3b82f6;
            box-shadow: 0 0 20px rgba(59, 130, 246, 0.5);
        }
        .language-selector {
            background: rgba(255, 255, 255, 0.1);
            border-radius: 8px;
            padding: 0.5rem;
            border: 1px solid #3b82f6;
        }
        .language-selector select {
            background: transparent;
            color: white;
            border: none;
            font-size: 1rem;
            outline: none;
            cursor: pointer;
        }
        .language-selector select option {
            background: #1e3a8a;
            color: white;
        }
        .section-title {
            text-shadow: 0 0 10px rgba(255, 255, 255, 0.5);
        }
        .glow-effect {
            animation: glow 2s ease-in-out infinite alternate;
        }
        @keyframes glow {
            from {
                text-shadow: 0 0 10px #fff, 0 0 20px #f59e0b;
            }
            to {
                text-shadow: 0 0 20px #fff, 0 0 30px #f97316;
            }
        }
        /* تحسين تخطيط قسم اكتشف المزيد */
        .discover-section {
            position: relative;
            z-index: 10;
            padding: 4rem 1rem;
        }
        .discover-section .menu-btn {
            display: block;
            width: 100%;
            max-width: 400px;
            margin: 0 auto 1.5rem;
        }
    </style>
</head>
<body>
    <!-- قماش الخلفية ثلاثي الأبعاد -->
    <canvas id="canvas"></canvas>

    <!-- القسم الرئيسي -->
    <section class="hero-section">
        <div class="relative z-10">
            <h1 class="text-6xl md:text-8xl font-bold mb-6 animate-text glow-effect" id="main-title">LERS</h1>
            <p class="text-xl md:text-2xl mb-8 max-w-2xl mx-auto" id="main-description">
                The Future Currency in the Testnet World - Join the Digital Revolution!
            </p>
            <button class="btn-reserve text-white font-semibold py-4 px-8 rounded-full text-lg" id="reserve-btn" onclick="reserveSeat()">
                Reserve Your Seat Now
            </button>
        </div>
    </section>

    <!-- قسم التواصل الاجتماعي -->
    <section class="py-12 text-center">
        <h2 class="text-3xl font-bold mb-6 section-title" id="follow-us">Follow Us</h2>
        <div class="flex justify-center gap-6">
            <a href="https://t.me/your_telegram" target="_blank" class="social-icon">
                <i class="fab fa-telegram-plane text-4xl text-blue-400"></i>
            </a>
            <a href="https://twitter.com/your_twitter" target="_blank" class="social-icon">
                <i class="fab fa-twitter text-4xl text-blue-300"></i>
            </a>
        </div>
    </section>

    <!-- قسم القائمة -->
    <section class="discover-section">
        <h2 class="text-4xl font-bold text-center mb-12 section-title" id="discover-more">Discover More</h2>
        <div class="max-w-md mx-auto space-y-6">
            <button class="menu-btn text-white font-semibold py-4 rounded-lg text-lg" id="beta-points-btn" onclick="goToBetaBot()">
                Collect Beta Points
            </button>
            <button class="menu-btn text-white font-semibold py-4 rounded-lg text-lg" id="coming-soon-btn" onclick="showComingSoon()">
                Coming Soon
            </button>
            <button class="menu-btn text-white font-semibold py-4 rounded-lg text-lg" id="about-btn" onclick="showAbout()">
                About
            </button>
        </div>
    </section>

    <!-- قسم اختيار اللغة -->
    <section class="py-8 text-center">
        <div class="language-selector">
            <select id="language-select" onchange="changeLanguage()">
                <option value="en" selected>English</option>
                <option value="ar">العربية</option>
                <option value="ru">Русский</option>
            </select>
        </div>
    </section>

    <!-- نافذة منبثقة -->
    <div id="modal" class="modal">
        <div class="modal-content">
            <h3 id="modal-title" class="text-2xl font-bold mb-4"></h3>
            <p id="modal-message" class="mb-6"></p>
            <button class="bg-blue-600 text-white py-2 px-6 rounded-lg" id="modal-close-btn" onclick="closeModal()">Close</button>
        </div>
    </div>

    <script>
        // بيانات الترجمة
        const translations = {
            en: {
                main_title: "LERS",
                main_description: "The Future Currency in the Testnet World - Join the Digital Revolution!",
                reserve_btn: "Reserve Your Seat Now",
                follow_us: "Follow Us",
                discover_more: "Discover More",
                beta_points_btn: "Collect Beta Points",
                coming_soon_btn: "Coming Soon",
                about_btn: "About",
                modal_close_btn: "Close",
                reserve_modal_title: "Reserve Your Seat",
                reserve_modal_message: "Your seat has been successfully reserved! You will receive LERS tokens upon listing.",
                coming_soon_modal_title: "Coming Soon",
                coming_soon_modal_message: "This feature will be available soon!",
                about_modal_title: "About LERS",
                about_modal_message: "LERS is the future currency in the Testnet world, aiming to revolutionize the digital economy through decentralization and transparency. Join us to be part of this change!"
            },
            ar: {
                main_title: "LERS",
                main_description: "العملة المستقبلية في عالم Testnet - انضم إلى الثورة الرقمية!",
                reserve_btn: "احجز الآن مقعدك",
                follow_us: "تابعنا",
                discover_more: "اكتشف المزيد",
                beta_points_btn: "جمع نقاط بيتا",
                coming_soon_btn: "قريباً",
                about_btn: "حول",
                modal_close_btn: "إغلاق",
                reserve_modal_title: "حجز مقعدك",
                reserve_modal_message: "تم حجز مقعدك بنجاح! ستتلقى عملات LERS عند الإدراج.",
                coming_soon_modal_title: "قريباً",
                coming_soon_modal_message: "هذه الميزة ستكون متاحة قريباً!",
                about_modal_title: "حول LERS",
                about_modal_message: "LERS هي العملة المستقبلية في عالم Testnet، تهدف إلى إحداث ثورة في الاقتصاد الرقمي من خلال اللامركزية والشفافية. انضم إلينا لتكون جزءاً من هذا التغيير!"
            },
            ru: {
                main_title: "LERS",
                main_description: "Будущая валюта в мире Testnet - присоединяйтесь к цифровой революции!",
                reserve_btn: "Забронируйте свое место сейчас",
                follow_us: "Следите за нами",
                discover_more: "Узнайте больше",
                beta_points_btn: "Собирать бета-очки",
                coming_soon_btn: "Скоро",
                about_btn: "О нас",
                modal_close_btn: "Закрыть",
                reserve_modal_title: "Забронировать место",
                reserve_modal_message: "Ваше место успешно забронировано! Вы получите токены LERS при листинге.",
                coming_soon_modal_title: "Скоро",
                coming_soon_modal_message: "Эта функция скоро будет доступна!",
                about_modal_title: "О LERS",
                about_modal_message: "LERS - это будущая валюта в мире Testnet, стремящаяся революционизировать цифровую экономику через децентрализацию и прозрачность. Присоединяйтесь к нам, чтобы стать частью этих изменений!"
            }
        };

        // وظيفة تغيير اللغة
        function changeLanguage() {
            const lang = document.getElementById("language-select").value;
            const html = document.getElementById("html");
            
            // تغيير النصوص
            document.getElementById("main-title").textContent = translations[lang].main_title;
            document.getElementById("main-description").textContent = translations[lang].main_description;
            document.getElementById("reserve-btn").textContent = translations[lang].reserve_btn;
            document.getElementById("follow-us").textContent = translations[lang].follow_us;
            document.getElementById("discover-more").textContent = translations[lang].discover_more;
            document.getElementById("beta-points-btn").textContent = translations[lang].beta_points_btn;
            document.getElementById("coming-soon-btn").textContent = translations[lang].coming_soon_btn;
            document.getElementById("about-btn").textContent = translations[lang].about_btn;
            document.getElementById("modal-close-btn").textContent = translations[lang].modal_close_btn;

            // تغيير الاتجاه بناءً على اللغة
            if (lang === "ar") {
                html.setAttribute("dir", "rtl");
                html.setAttribute("lang", "ar");
            } else {
                html.setAttribute("dir", "ltr");
                html.setAttribute("lang", lang);
            }
        }

        // تأثيرات GSAP
        gsap.from(".animate-text", { opacity: 0, y: 50, duration: 1.5, ease: "power3.out" });
        gsap.from(".btn-reserve", { opacity: 0, scale: 0.8, delay: 0.5, duration: 1, ease: "elastic.out(1, 0.3)" });
        gsap.from(".social-icon", { opacity: 0, y: 20, delay: 1, duration: 1, stagger: 0.2 });
        gsap.from(".menu-btn", { opacity: 0, y: 20, delay: 1.2, duration: 1, stagger: 0.2 });

        // إعداد Three.js لتأثير الجزيئات ثلاثية الأبعاد
        const scene = new THREE.Scene();
        const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
        const renderer = new THREE.WebGLRenderer({ canvas: document.getElementById("canvas"), alpha: true });
        renderer.setSize(window.innerWidth, window.innerHeight);
        camera.position.z = 30;

        const particlesGeometry = new THREE.BufferGeometry();
        const particlesCount = 5000;
        const posArray = new Float32Array(particlesCount * 3);
        for (let i = 0; i < particlesCount * 3; i++) {
            posArray[i] = (Math.random() - 0.5) * 100;
        }
        particlesGeometry.setAttribute("position", new THREE.BufferAttribute(posArray, 3));
        const particlesMaterial = new THREE.PointsMaterial({
            size: 0.1,
            color: 0xffffff,
            transparent: true,
            opacity: 0.8,
            blending: THREE.AdditiveBlending
        });
        const particlesMesh = new THREE.Points(particlesGeometry, particlesMaterial);
        scene.add(particlesMesh);

        function animateParticles() {
            requestAnimationFrame(animateParticles);
            particlesMesh.rotation.y += 0.001;
            particlesMesh.rotation.x += 0.0005;
            renderer.render(scene, camera);
        }
        animateParticles();

        // ضبط حجم القماش عند تغيير حجم النافذة
        window.addEventListener("resize", () => {
            camera.aspect = window.innerWidth / window.innerHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(window.innerWidth, window.innerHeight);
        });

        // وظائف الأزرار
        function reserveSeat() {
            const lang = document.getElementById("language-select").value;
            showModal(translations[lang].reserve_modal_title, translations[lang].reserve_modal_message);
        }

        function goToBetaBot() {
            window.open("https://t.me/your_beta_bot", "_blank");
        }

        function showComingSoon() {
            const lang = document.getElementById("language-select").value;
            showModal(translations[lang].coming_soon_modal_title, translations[lang].coming_soon_modal_message);
        }

        function showAbout() {
            const lang = document.getElementById("language-select").value;
            showModal(translations[lang].about_modal_title, translations[lang].about_modal_message);
        }

        // إدارة النافذة المنبثقة
        function showModal(title, message) {
            document.getElementById("modal-title").textContent = title;
            document.getElementById("modal-message").textContent = message;
            document.getElementById("modal").style.display = "flex";
        }

        function closeModal() {
            document.getElementById("modal").style.display = "none";
        }

        // تهيئة اللغة الافتراضية (الإنجليزية)
        document.addEventListener("DOMContentLoaded", () => {
            changeLanguage();
        });
    </script>
</body>
</html>
