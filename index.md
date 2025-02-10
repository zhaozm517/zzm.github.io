<!DOCTYPE html>
<html lang="zh">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>zzm</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: -apple-system, BlinkMacSystemFont, "SF Pro Text", "Helvetica Neue", Arial, sans-serif;
        }

        body {
            background-color: #f5f5f7;
            color: #1d1d1f;
            line-height: 1.6;
        }

        header {
            background-color: rgba(255, 255, 255, 0.8);
            backdrop-filter: blur(10px);
            position: fixed;
            width: 100%;
            top: 0;
            z-index: 100;
            box-shadow: 0 1px 3px rgba(0,0,0,0.1);
        }

        nav {
            max-width: 980px;
            margin: 0 auto;
            padding: 1rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo {
            font-size: 1.5rem;
            font-weight: 600;
            color: #1d1d1f;
            text-decoration: none;
        }

        .nav-links a {
            color: #1d1d1f;
            text-decoration: none;
            margin-left: 2rem;
            font-size: 0.9rem;
            transition: color 0.3s ease;
        }

        .nav-links a:hover {
            color: #06c;
        }

        main {
            max-width: 980px;
            margin: 6rem auto 2rem;
            padding: 0 1rem;
        }

        .hero {
            text-align: center;
            margin-bottom: 4rem;
        }

        .hero h1 {
            font-size: 3rem;
            font-weight: 700;
            margin-bottom: 1rem;
        }

        .hero p {
            font-size: 1.5rem;
            color: #86868b;
            margin-bottom: 2rem;
        }

        .posts {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 2rem;
        }

        .post-card {
            background: white;
            border-radius: 18px;
            overflow: hidden;
            transition: transform 0.3s ease;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
            cursor: pointer;
        }

        .post-card:hover {
            transform: translateY(-8px) scale(1.02);
            box-shadow: 0 8px 16px rgba(0,0,0,0.1);
        }

        .post-image {
            width: 100%;
            height: 200px;
            object-fit: cover;
            transition: transform 0.5s ease;
        }

        .post-card:hover .post-image {
            transform: scale(1.1);
        }

        .post-content {
            padding: 1.5rem;
        }

        .post-title {
            font-size: 1.25rem;
            margin-bottom: 0.5rem;
            font-weight: 600;
        }

        .post-excerpt {
            color: #86868b;
            font-size: 0.9rem;
            margin-bottom: 1rem;
        }

        .post-date {
            color: #86868b;
            font-size: 0.8rem;
        }

        footer {
            text-align: center;
            padding: 2rem;
            color: #86868b;
            font-size: 0.9rem;
        }

        @media (max-width: 768px) {
            .hero h1 {
                font-size: 2rem;
            }
            
            .hero p {
                font-size: 1.2rem;
            }

            .nav-links a {
                margin-left: 1rem;
            }
        }

        .about, .contact {
            background: white;
            border-radius: 18px;
            padding: 2rem;
            margin: 2rem 0;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }

        .about h2, .contact h2 {
            font-size: 2rem;
            margin-bottom: 1rem;
            color: #1d1d1f;
        }

        .about p, .contact p {
            color: #86868b;
            margin-bottom: 1rem;
            font-size: 1.1rem;
        }

        .blog-detail {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.5);
            z-index: 1000;
            overflow-y: auto;
            transition: opacity 0.3s ease;
            opacity: 0;
            pointer-events: none;
        }

        .blog-detail.active {
            opacity: 1;
            pointer-events: auto;
        }

        .blog-detail-content {
            background: white;
            max-width: 800px;
            margin: 100px auto 40px;
            padding: 2rem;
            border-radius: 18px;
            position: relative;
            transform: translateY(30px);
            transition: transform 0.3s ease;
        }

        .blog-detail.active .blog-detail-content {
            transform: translateY(0);
        }

        .close-button {
            position: absolute;
            top: 20px;
            right: 20px;
            font-size: 24px;
            cursor: pointer;
            color: #86868b;
            background: none;
            border: none;
            padding: 5px 10px;
        }

        .blog-detail img {
            width: 100%;
            max-height: 400px;
            object-fit: cover;
            border-radius: 12px;
            margin-bottom: 2rem;
        }

        .blog-detail h1 {
            font-size: 2.5rem;
            margin-bottom: 1rem;
        }

        .blog-detail .meta {
            color: #86868b;
            margin-bottom: 2rem;
        }

        .blog-content {
            line-height: 1.8;
            color: #1d1d1f;
        }

        body.modal-open {
            overflow: hidden;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        @keyframes slideIn {
            from { transform: translateX(-100%); }
            to { transform: translateX(0); }
        }

        .hero {
            animation: fadeIn 1s ease-out;
        }

        .post-card {
            animation: fadeIn 0.8s ease-out;
            animation-fill-mode: both;
        }

        .post-card:nth-child(1) { animation-delay: 0.1s; }
        .post-card:nth-child(2) { animation-delay: 0.2s; }
        .post-card:nth-child(3) { animation-delay: 0.3s; }
        .post-card:nth-child(4) { animation-delay: 0.4s; }
        .post-card:nth-child(5) { animation-delay: 0.5s; }
        .post-card:nth-child(6) { animation-delay: 0.6s; }

        .nav-links a {
            position: relative;
        }

        .nav-links a::after {
            content: '';
            position: absolute;
            width: 0;
            height: 2px;
            bottom: -4px;
            left: 0;
            background-color: #06c;
            transition: width 0.3s ease;
        }

        .nav-links a:hover::after {
            width: 100%;
        }

        .progress-bar {
            position: fixed;
            top: 0;
            left: 0;
            width: 0;
            height: 3px;
            background: linear-gradient(to right, #06c, #0091ff);
            z-index: 1001;
            transition: width 0.2s ease;
        }

        pre code {
            background: #f8f9fa;
            border-radius: 8px;
            padding: 1.5rem;
            font-family: 'SF Mono', Consolas, Monaco, monospace;
            font-size: 0.9rem;
            overflow-x: auto;
            display: block;
            border: 1px solid #eee;
        }

        .post-tags {
            display: flex;
            gap: 0.5rem;
            margin-top: 0.5rem;
        }

        .tag {
            background: #f5f5f7;
            padding: 0.2rem 0.8rem;
            border-radius: 12px;
            font-size: 0.8rem;
            color: #86868b;
            transition: all 0.3s ease;
        }

        .tag:hover {
            background: #06c;
            color: white;
        }

        /* 添加粒子背景和新的动态效果样式 */
        #particles-js {
            position: fixed;
            width: 100%;
            height: 100%;
            top: 0;
            left: 0;
            z-index: -1;
            background: linear-gradient(45deg, #1a1a1a, #2a2a2a);
        }

        .hero {
            position: relative;
            padding: 4rem 0;
            color: white;
            text-shadow: 0 2px 4px rgba(0,0,0,0.3);
            overflow: hidden;
        }

        .hero::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(45deg, #06c, #0091ff);
            opacity: 0.9;
            z-index: -1;
            transform: skewY(-6deg);
            transform-origin: top left;
        }

        .hero h1 {
            font-size: 4rem;
            background: linear-gradient(45deg, #fff, #f0f0f0);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            animation: gradientText 3s ease infinite;
        }

        @keyframes gradientText {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        .post-card {
            backdrop-filter: blur(10px);
            background: rgba(255, 255, 255, 0.9);
            border: 1px solid rgba(255, 255, 255, 0.2);
            transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .post-card:hover {
            transform: translateY(-12px) rotate(2deg);
            box-shadow: 0 12px 24px rgba(0,0,0,0.2);
        }

        .tag {
            position: relative;
            overflow: hidden;
        }

        .tag::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.2), transparent);
            transition: 0.5s;
        }

        .tag:hover::before {
            left: 100%;
        }

        .floating {
            animation: floating 3s ease-in-out infinite;
        }

        @keyframes floating {
            0% { transform: translateY(0px); }
            50% { transform: translateY(-10px); }
            100% { transform: translateY(0px); }
        }

        .glow {
            animation: glow 2s ease-in-out infinite alternate;
        }

        @keyframes glow {
            from { text-shadow: 0 0 5px #fff, 0 0 10px #fff, 0 0 15px #0073e6, 0 0 20px #0073e6; }
            to { text-shadow: 0 0 10px #fff, 0 0 20px #fff, 0 0 30px #0073e6, 0 0 40px #0073e6; }
        }

        .nav-links a {
            position: relative;
            color: white;
        }

        .nav-links a::before {
            content: '';
            position: absolute;
            width: 100%;
            height: 2px;
            bottom: -5px;
            left: 0;
            background-color: white;
            transform: scaleX(0);
            transition: transform 0.3s ease;
        }

        .nav-links a:hover::before {
            transform: scaleX(1);
        }

        header {
            background: rgba(26, 26, 26, 0.8);
        }

        .logo {
            color: white;
        }

        body {
            background: #1a1a1a;
        }
    </style>
</head>
<body>
    <div id="particles-js"></div>

    <header>
        <nav>
            <a href="#" class="logo">Blog</a>
            <div class="nav-links">
                <a href="#home" onclick="scrollToSection('hero')">首页</a>
                <a href="#posts" onclick="scrollToSection('posts')">文章</a>
                <a href="#about" onclick="scrollToSection('about')">关于</a>
                <a href="#contact" onclick="scrollToSection('contact')">联系</a>
            </div>
        </nav>
    </header>

    <main>
        <section class="hero" id="home">
            <h1>欢迎来到我的博客</h1>
            <p>分享技术、生活和创意</p>
        </section>

        <section class="posts" id="posts">
            <article class="post-card">
                <img src="https://picsum.photos/600/400" alt="文章配图" class="post-image">
                <div class="post-content">
                    <h2 class="post-title">深入理解JavaScript异步编程</h2>
                    <p class="post-excerpt">探索JavaScript中的异步编程模式，包括Promise、async/await的实践应用...</p>
                    <p class="post-date">2024年3月20日</p>
                    <div class="post-tags">
                        <span class="tag">JavaScript</span>
                        <span class="tag">异步编程</span>
                        <span class="tag">Promise</span>
                    </div>
                </div>
            </article>

            <article class="post-card">
                <img src="https://picsum.photos/600/401" alt="文章配图" class="post-image">
                <div class="post-content">
                    <h2 class="post-title">现代前端框架对比分析</h2>
                    <p class="post-excerpt">深入对比React、Vue和Angular的优势与特点，帮助开发者选择适合的框架...</p>
                    <p class="post-date">2024年3月18日</p>
                    <div class="post-tags">
                        <span class="tag">前端框架</span>
                        <span class="tag">React</span>
                        <span class="tag">Vue</span>
                        <span class="tag">Angular</span>
                    </div>
                </div>
            </article>

            <article class="post-card">
                <img src="https://picsum.photos/600/402" alt="文章配图" class="post-image">
                <div class="post-content">
                    <h2 class="post-title">Web性能优化实战指南</h2>
                    <p class="post-excerpt">分享一些实用的Web性能优化技巧，从加载速度到运行时性能的全方位提升...</p>
                    <p class="post-date">2024年3月15日</p>
                    <div class="post-tags">
                        <span class="tag">Web性能优化</span>
                        <span class="tag">加载速度</span>
                        <span class="tag">运行时性能</span>
                    </div>
                </div>
            </article>

            <article class="post-card">
                <img src="https://picsum.photos/600/403" alt="文章配图" class="post-image">
                <div class="post-content">
                    <h2 class="post-title">CSS Grid布局完全指南</h2>
                    <p class="post-excerpt">详细介绍CSS Grid布局系统，从基础概念到高级应用的全面教程...</p>
                    <p class="post-date">2024年3月12日</p>
                    <div class="post-tags">
                        <span class="tag">CSS</span>
                        <span class="tag">CSS Grid</span>
                        <span class="tag">布局系统</span>
                    </div>
                </div>
            </article>

            <article class="post-card">
                <img src="https://picsum.photos/600/404" alt="文章配图" class="post-image">
                <div class="post-content">
                    <h2 class="post-title">Docker容器化实践</h2>
                    <p class="post-excerpt">学习如何使用Docker进行应用容器化，包括最佳实践和常见问题解决方案...</p>
                    <p class="post-date">2024年3月10日</p>
                    <div class="post-tags">
                        <span class="tag">Docker</span>
                        <span class="tag">容器化</span>
                        <span class="tag">最佳实践</span>
                    </div>
                </div>
            </article>

            <article class="post-card">
                <img src="https://picsum.photos/600/405" alt="文章配图" class="post-image">
                <div class="post-content">
                    <h2 class="post-title">TypeScript入门到进阶</h2>
                    <p class="post-excerpt">从零开始学习TypeScript，掌握类型系统和高级特性...</p>
                    <p class="post-date">2024年3月8日</p>
                    <div class="post-tags">
                        <span class="tag">TypeScript</span>
                        <span class="tag">入门</span>
                        <span class="tag">进阶</span>
                    </div>
                </div>
            </article>
        </section>

        <section class="about" id="about">
            <h2>关于我</h2>
            <p>你好！我是一名热爱技术和写作的博主。通过这个博客，我希望能够分享我的经验和见解。</p>
        </section>

        <section class="contact" id="contact">
            <h2>联系方式</h2>
            <p>邮箱：zzm51704@gmail.com</p>
            <p>微信：AHsea0</p>
        </section>
    </main>

    <footer>
        <p>&copy; 2024 个人博客. 保留所有权利.</p>
    </footer>

    <div class="blog-detail" id="blogDetail">
        <div class="blog-detail-content">
            <button class="close-button" onclick="closeBlogDetail()">&times;</button>
            <img id="detailImage" src="" alt="文章详细配图">
            <h1 id="detailTitle"></h1>
            <div class="meta">
                <span id="detailDate"></span>
            </div>
            <div class="blog-content" id="detailContent">
            </div>
        </div>
    </div>

    <div class="progress-bar" id="progressBar"></div>

    <script src="https://cdn.jsdelivr.net/particles.js/2.0.0/particles.min.js"></script>
    <script>
        // 初始化粒子效果
        particlesJS('particles-js',
        {
            "particles": {
                "number": {
                    "value": 80,
                    "density": {
                        "enable": true,
                        "value_area": 800
                    }
                },
                "color": {
                    "value": "#ffffff"
                },
                "shape": {
                    "type": "circle"
                },
                "opacity": {
                    "value": 0.5,
                    "random": false
                },
                "size": {
                    "value": 3,
                    "random": true
                },
                "line_linked": {
                    "enable": true,
                    "distance": 150,
                    "color": "#ffffff",
                    "opacity": 0.4,
                    "width": 1
                },
                "move": {
                    "enable": true,
                    "speed": 6,
                    "direction": "none",
                    "random": false,
                    "straight": false,
                    "out_mode": "out",
                    "bounce": false
                }
            },
            "interactivity": {
                "detect_on": "canvas",
                "events": {
                    "onhover": {
                        "enable": true,
                        "mode": "repulse"
                    },
                    "onclick": {
                        "enable": true,
                        "mode": "push"
                    },
                    "resize": true
                }
            },
            "retina_detect": true
        });

        // 添加鼠标跟随效果
        document.addEventListener('mousemove', (e) => {
            const cursor = document.createElement('div');
            cursor.className = 'cursor-trail';
            cursor.style.left = e.pageX + 'px';
            cursor.style.top = e.pageY + 'px';
            document.body.appendChild(cursor);

            setTimeout(() => {
                cursor.remove();
            }, 1000);
        });

        // 添加滚动动画
        const observerOptions = {
            threshold: 0.1
        };

        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.classList.add('animate-in');
                }
            });
        }, observerOptions);

        document.querySelectorAll('.post-card, .about, .contact').forEach((el) => {
            observer.observe(el);
        });

        // 添加打字机效果
        function typeWriter(element, text, speed = 100) {
            let i = 0;
            element.innerHTML = '';
            function type() {
                if (i < text.length) {
                    element.innerHTML += text.charAt(i);
                    i++;
                    setTimeout(type, speed);
                }
            }
            type();
        }

        // 页面加载完成后的动画
        window.addEventListener('load', () => {
            const heroTitle = document.querySelector('.hero h1');
            const originalText = heroTitle.textContent;
            typeWriter(heroTitle, originalText);
        });

        // 添加3D卡片效果
        document.querySelectorAll('.post-card').forEach(card => {
            card.addEventListener('mousemove', (e) => {
                const rect = card.getBoundingClientRect();
                const x = e.clientX - rect.left;
                const y = e.clientY - rect.top;
                
                const centerX = rect.width / 2;
                const centerY = rect.height / 2;
                
                const rotateX = (y - centerY) / 10;
                const rotateY = -(x - centerX) / 10;
                
                card.style.transform = `perspective(1000px) rotateX(${rotateX}deg) rotateY(${rotateY}deg)`;
            });

            card.addEventListener('mouseleave', () => {
                card.style.transform = 'perspective(1000px) rotateX(0) rotateY(0)';
            });
        });

        function scrollToSection(sectionId) {
            const element = document.getElementById(sectionId);
            if (element) {
                const headerOffset = 80;
                const elementPosition = element.getBoundingClientRect().top;
                const offsetPosition = elementPosition + window.pageYOffset - headerOffset;

                window.scrollTo({
                    top: offsetPosition,
                    behavior: 'smooth'
                });
            }
        }

        const blogPosts = [
            {
                id: 1,
                title: "深入理解JavaScript异步编程",
                date: "2024年3月20日",
                image: "https://picsum.photos/600/400",
                content: `
                    <p>在现代Web开发中，异步编程已经成为一个不可或缺的概念。本文将深入探讨JavaScript中的异步编程模式。</p>
                    
                    <h2>什么是异步编程？</h2>
                    <p>异步编程允许程序在执行长时间运行的任务时不会被阻塞。在JavaScript中，这对于处理网络请求、文件操作等操作特别重要。</p>
                    
                    <h2>Promise详解</h2>
                    <p>Promise是现代JavaScript中处理异步操作的基础。一个Promise代表一个异步操作的最终完成或失败。</p>
                    
                    <pre><code>
const promise = new Promise((resolve, reject) => {
    // 异步操作
    setTimeout(() => {
        resolve('操作成功');
    }, 1000);
});

promise.then(result => {
    console.log(result);
}).catch(error => {
    console.error(error);
});
                    </code></pre>

                    <h2>Async/Await语法</h2>
                    <p>Async/Await是构建在Promise之上的语法糖，让异步代码更容易编写和理解。</p>
                    
                    <pre><code>
async function fetchData() {
    try {
        const response = await fetch('https://api.example.com/data');
        const data = await response.json();
        return data;
    } catch (error) {
        console.error('获取数据失败:', error);
    }
}
                    </code></pre>

                    <h2>实践建议</h2>
                    <ul>
                        <li>总是使用try/catch处理异步操作中的错误</li>
                        <li>避免回调地狱，优先使用Promise链或async/await</li>
                        <li>合理使用Promise.all()处理并行操作</li>
                    </ul>

                    <h2>总结</h2>
                    <p>掌握异步编程对于现代JavaScript开发至关重要。通过合理使用Promise和async/await，我们可以编写更清晰、可维护的代码。</p>
                `
            },
            {
                id: 2,
                title: "现代前端框架对比分析",
                date: "2024年3月18日",
                image: "https://picsum.photos/600/401",
                content: `
                    <p>在当前前端开发领域，React、Vue和Angular是三大主流框架。本文将对它们进行深入对比分析。</p>

                    <h2>React特点</h2>
                    <ul>
                        <li>使用JSX语法</li>
                        <li>单向数据流</li>
                        <li>虚拟DOM</li>
                        <li>强大的生态系统</li>
                    </ul>

                    <h2>Vue优势</h2>
                    <ul>
                        <li>温和的学习曲线</li>
                        <li>双向数据绑定</li>
                        <li>优秀的性能</li>
                        <li>灵活的API设计</li>
                    </ul>

                    <h2>框架对比</h2>
                    <table>
                        <tr>
                            <th>特性</th>
                            <th>React</th>
                            <th>Vue</th>
                            <th>Angular</th>
                        </tr>
                        <tr>
                            <td>学习曲线</td>
                            <td>中等</td>
                            <td>低</td>
                            <td>高</td>
                        </tr>
                        <tr>
                            <td>性能</td>
                            <td>优秀</td>
                            <td>优秀</td>
                            <td>良好</td>
                        </tr>
                    </table>

                    <h2>选择建议</h2>
                    <p>框架选择应该基于项目需求、团队经验和长期维护考虑。没有最好的框架，只有最适合的框架。</p>

                    <h2>未来展望</h2>
                    <p>随着Web Components的发展，前端框架可能会向更标准化的方向发展。持续关注新技术的演进对于前端开发者来说非常重要。</p>
                `
            },
            {
                id: 3,
                title: "Web性能优化实战指南",
                date: "2024年3月15日",
                image: "https://picsum.photos/600/402",
                content: `
                    <p>网站性能直接影响用户体验和转化率。本文将分享一些实用的Web性能优化技巧。</p>

                    <h2>加载性能优化</h2>
                    <ul>
                        <li>资源压缩与合并</li>
                        <li>图片优化</li>
                        <li>懒加载策略</li>
                        <li>CDN加速</li>
                    </ul>

                    <h2>代码层面优化</h2>
                    <pre><code>
// 图片懒加载示例
const images = document.querySelectorAll('img[data-src]');
const imageObserver = new IntersectionObserver((entries, observer) => {
    entries.forEach(entry => {
        if (entry.isIntersecting) {
            const img = entry.target;
            img.src = img.dataset.src;
            observer.unobserve(img);
        }
    });
});

images.forEach(img => imageObserver.observe(img));
                    </code></pre>

                    <h2>缓存策略</h2>
                    <p>合理利用浏览器缓存机制：</p>
                    <ul>
                        <li>强缓存（Cache-Control, Expires）</li>
                        <li>协商缓存（ETag, Last-Modified）</li>
                        <li>Service Worker缓存</li>
                    </ul>

                    <h2>性能监控</h2>
                    <p>使用性能监控工具：</p>
                    <ul>
                        <li>Lighthouse</li>
                        <li>Chrome DevTools</li>
                        <li>Web Vitals</li>
                    </ul>
                `
            },
            {
                id: 4,
                title: "CSS Grid布局完全指南",
                date: "2024年3月12日",
                image: "https://picsum.photos/600/403",
                content: `
                    <p>CSS Grid是一个强大的二维布局系统，让我们深入了解如何使用它创建复杂的布局。</p>

                    <h2>基础概念</h2>
                    <p>Grid布局的核心概念：</p>
                    <ul>
                        <li>Grid Container</li>
                        <li>Grid Items</li>
                        <li>Grid Lines</li>
                        <li>Grid Tracks</li>
                    </ul>

                    <h2>常用属性</h2>
                    <pre><code>
.grid-container {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-template-rows: auto;
    gap: 20px;
}

.grid-item {
    grid-column: span 2;
    grid-row: 1 / 3;
}
                    </code></pre>

                    <h2>响应式布局</h2>
                    <p>使用Grid创建响应式布局：</p>
                    <pre><code>
.responsive-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 1rem;
}
                    </code></pre>

                    <h2>实践案例</h2>
                    <p>一些常见的Grid布局模式：</p>
                    <ul>
                        <li>圣杯布局</li>
                        <li>画廊布局</li>
                        <li>仪表板布局</li>
                    </ul>
                `
            },
            {
                id: 5,
                title: "Docker容器化实践",
                date: "2024年3月10日",
                image: "https://picsum.photos/600/404",
                content: `
                    <p>Docker已经成为现代应用部署的标准。本文将介绍Docker的核心概念和最佳实践。</p>

                    <h2>Docker基础</h2>
                    <ul>
                        <li>镜像（Image）</li>
                        <li>容器（Container）</li>
                        <li>仓库（Repository）</li>
                    </ul>

                    <h2>Dockerfile最佳实践</h2>
                    <pre><code>
# 使用多阶段构建
FROM node:alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

FROM nginx:alpine
COPY --from=builder /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
                    </code></pre>

                    <h2>容器编排</h2>
                    <p>使用Docker Compose管理多容器应用：</p>
                    <pre><code>
version: '3'
services:
  web:
    build: .
    ports:
      - "80:80"
  db:
    image: postgres
    environment:
      POSTGRES_PASSWORD: example
                    </code></pre>

                    <h2>安全最佳实践</h2>
                    <ul>
                        <li>使用官方镜像</li>
                        <li>定期更新基础镜像</li>
                        <li>使用非root用户运行应用</li>
                        <li>扫描镜像漏洞</li>
                    </ul>
                `
            },
            {
                id: 6,
                title: "TypeScript入门到进阶",
                date: "2024年3月8日",
                image: "https://picsum.photos/600/405",
                content: `
                    <p>TypeScript作为JavaScript的超集，为我们提供了类型安全和更好的开发体验。</p>

                    <h2>基础类型</h2>
                    <pre><code>
// 基础类型示例
let isDone: boolean = false;
let decimal: number = 6;
let color: string = "blue";
let list: number[] = [1, 2, 3];
let tuple: [string, number] = ["hello", 10];
                    </code></pre>

                    <h2>接口和类型</h2>
                    <pre><code>
interface User {
    id: number;
    name: string;
    email?: string;
}

type Point = {
    x: number;
    y: number;
};

class Employee implements User {
    constructor(
        public id: number,
        public name: string,
        public email?: string
    ) {}
}
                    </code></pre>

                    <h2>泛型</h2>
                    <p>使用泛型创建可重用的组件：</p>
                    <pre><code>
function identity<T>(arg: T): T {
    return arg;
}

class GenericNumber<T> {
    zeroValue: T;
    add: (x: T, y: T) => T;
}
                    </code></pre>

                    <h2>高级特性</h2>
                    <ul>
                        <li>装饰器</li>
                        <li>类型守卫</li>
                        <li>映射类型</li>
                        <li>条件类型</li>
                    </ul>
                `
            }
        ];

        function showBlogDetail(postId) {
            const post = blogPosts.find(p => p.id === postId);
            if (!post) return;

            document.getElementById('detailImage').src = post.image;
            document.getElementById('detailTitle').textContent = post.title;
            document.getElementById('detailDate').textContent = post.date;
            document.getElementById('detailContent').innerHTML = post.content;
            
            const blogDetail = document.getElementById('blogDetail');
            blogDetail.style.display = 'block';
            setTimeout(() => {
                blogDetail.classList.add('active');
            }, 10);
            document.body.classList.add('modal-open');
        }

        function closeBlogDetail() {
            const blogDetail = document.getElementById('blogDetail');
            blogDetail.classList.remove('active');
            setTimeout(() => {
                blogDetail.style.display = 'none';
                document.body.classList.remove('modal-open');
            }, 300);
        }

        document.querySelectorAll('.post-card').forEach((card, index) => {
            card.onclick = () => showBlogDetail(index + 1);
        });

        window.addEventListener('scroll', () => {
            const winScroll = document.body.scrollTop || document.documentElement.scrollTop;
            const height = document.documentElement.scrollHeight - document.documentElement.clientHeight;
            const scrolled = (winScroll / height) * 100;
            document.getElementById('progressBar').style.width = scrolled + '%';
        });

        document.getElementById('blogDetail').addEventListener('click', (e) => {
            if (e.target.id === 'blogDetail') {
                closeBlogDetail();
            }
        });

        document.addEventListener('keydown', (e) => {
            if (e.key === 'Escape') {
                closeBlogDetail();
            }
        });
    </script>

    <style>
        .cursor-trail {
            position: fixed;
            width: 10px;
            height: 10px;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.5);
            pointer-events: none;
            animation: cursorTrail 1s linear forwards;
        }

        @keyframes cursorTrail {
            0% {
                opacity: 0.8;
                transform: scale(1);
            }
            100% {
                opacity: 0;
                transform: scale(0);
            }
        }

        .animate-in {
            animation: fadeInUp 0.6s ease forwards;
        }

        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
    </style>
</body>
</html>
