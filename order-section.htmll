<style>
    /* --- BASE OVERLAY & CONTAINER --- */
    #menu-book-overlay {
        display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%;
        background: rgba(0,0,0,0.85); z-index: 10000; backdrop-filter: blur(12px);
        align-items: center; justify-content: center; font-family: 'Poppins', sans-serif;
        box-sizing: border-box; padding: 20px; overflow-y: auto;
    }

    .book-interface-container {
        display: flex; align-items: center; justify-content: center;
        width: 100%; max-width: 960px; gap: 20px; position: relative; margin: auto;
        flex-wrap: nowrap;
    }

    /* --- BOOK WRAPPER --- */
    .book-wrapper {
        width: 650px; height: 420px;
        position: relative; perspective: 2000px; flex-shrink: 0;
        background: transparent; order: 3;
    }

    .page {
        position: absolute; width: 50%; height: 100%; right: 0; top: 0;
        transform-origin: left center; transform-style: preserve-3d; user-select: none;
        transition: transform 0.8s cubic-bezier(0.645, 0.045, 0.355, 1);
    }

    .page.flipped { transform: rotateY(-180deg); }

    #p1 { z-index: 5; } 
    #p2 { z-index: 4; } 
    #p3 { z-index: 3; } 
    #p4 { z-index: 2; } 
    #p5 { z-index: 1; }

    .page-front, .page-back {
        position: absolute; width: 100%; height: 100%; top: 0; left: 0;
        backface-visibility: hidden; padding: 15px; box-sizing: border-box;
        display: flex; flex-direction: column; overflow-y: auto; border: 1px solid #d4a373;
    }

    .page-front { background: #fdfaf7; border-radius: 0 8px 8px 0; }
    .page-back { transform: rotateY(180deg); background: #fdfaf7; border-radius: 8px 0 0 8px; }

    .page-title { 
        font-family: 'Playfair Display', serif; color: #800000; font-size: 1.05rem;
        border-bottom: 2px solid #d4a373; margin-bottom: 10px; padding-bottom: 5px; 
        display: flex; align-items: center; gap: 8px;
    }

    /* --- SIDEBAR --- */
    .selected-menus-sidebar {
        width: 260px; background: #fff; border-radius: 10px; border: 1px solid #d4a373;
        box-shadow: 0 8px 25px rgba(0,0,0,0.3); display: flex; flex-direction: column;
        height: 420px; transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
        position: relative; z-index: 10015; flex-shrink: 0; overflow: hidden;
        order: 1; box-sizing: border-box;
    }

    .selected-menus-sidebar.collapsed { width: 45px; }

    .sidebar-toggle-btn {
        position: absolute; top: 10px; right: 10px; background: #800000; color: #fff;
        border: none; width: 24px; height: 24px; border-radius: 50%; cursor: pointer;
        display: flex; align-items: center; justify-content: center; z-index: 5;
        transition: transform 0.3s ease; font-size: 0.7rem;
    }

    .selected-menus-sidebar.collapsed .sidebar-toggle-btn { right: 10px; }

    .sidebar-content {
        padding: 12px; height: 100%; display: flex; flex-direction: column;
        box-sizing: border-box; transition: opacity 0.3s ease;
    }

    .selected-menus-sidebar.collapsed .sidebar-content { opacity: 0; pointer-events: none; }

    .sidebar-collapsed-label {
        position: absolute; top: 50px; left: 50%; transform: translateX(-50%) rotate(-90deg);
        color: #800000; font-weight: bold; font-size: 0.7rem; white-space: nowrap;
        display: none; cursor: pointer; letter-spacing: 1px;
    }

    .selected-menus-sidebar.collapsed .sidebar-collapsed-label { display: block; }

    .selected-list-container {
        flex-grow: 1; overflow-y: auto; margin-top: 6px; margin-bottom: 6px;
        border-top: 1px solid #eee; border-bottom: 1px solid #eee; padding: 6px 0;
    }

    .selected-item-row {
        display: flex; justify-content: space-between; align-items: center;
        background: #fdfaf7; padding: 5px 8px; border-radius: 6px; margin-bottom: 5px;
        border: 1px solid #e2e8f0; font-size: 0.7rem;
    }

    .selected-item-row button {
        background: none; border: none; color: #e53e3e; cursor: pointer; font-size: 0.75rem;
    }

    .sidebar-total-section {
        background: #fdfaf7; padding: 8px 10px; border-radius: 6px; border: 1px solid #d4a373;
        margin-bottom: 8px; display: flex; justify-content: space-between; align-items: center;
        font-size: 0.75rem; font-weight: bold; color: #800000; flex-shrink: 0;
    }

    /* --- MENU ITEM CARD --- */
    .menu-item-card {
        background: #fff; border: 1px solid #e2e8f0; border-radius: 6px;
        padding: 6px; display: flex; align-items: center; justify-content: space-between;
        gap: 6px; margin-bottom: 6px; box-shadow: 0 2px 4px rgba(0,0,0,0.04);
    }

    .menu-item-info { display: flex; align-items: center; gap: 6px; flex-grow: 1; min-width: 0; }
    .menu-item-img { width: 35px; height: 35px; border-radius: 4px; object-fit: cover; flex-shrink: 0; }
    .menu-item-details { min-width: 0; }
    .menu-item-details h4 { font-size: 0.75rem; margin: 0; color: #333; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
    .menu-item-details span { font-size: 0.65rem; color: #800000; font-weight: bold; }

    .btn-select-menu {
        background: #fdfaf7; color: #800000; border: 1px solid #800000;
        padding: 3px 6px; border-radius: 4px; font-size: 0.65rem; font-weight: bold;
        cursor: pointer; transition: all 0.3s ease; white-space: nowrap; flex-shrink: 0;
    }

    .btn-select-menu:hover, .btn-select-menu.selected {
        background: #800000; color: #fff;
    }

    /* --- NAVIGATION BUTTONS --- */
    .book-nav-btn {
        width: 35px; height: 35px; border-radius: 50%; border: 1px solid #cbd5e0;
        background: linear-gradient(135deg, #fff 0%, #e2e8f0 100%); color: #800000;
        cursor: pointer; z-index: 10010; transition: all 0.4s ease;
        box-shadow: 0 4px 10px rgba(0,0,0,0.3); display: flex; align-items: center; justify-content: center; font-weight: bold;
        flex-shrink: 0;
    }

    .book-nav-btn:hover:not(:disabled) { transform: scale(1.1); background: #800000; color: #fff; }
    .book-nav-btn.auto-hide-arrow { opacity: 0; visibility: hidden; pointer-events: none; }

    /* --- MECHANICAL LOCK SYSTEM --- */
    .book-3d-mechanical-lock {
        position: absolute; top: 45%; right: -15px; width: 30px; height: 45px;
        z-index: 10050; cursor: pointer; transition: all 0.6s cubic-bezier(0.4, 0, 0.2, 1);
    }
    .lock-metal-clasp {
        width: 100%; height: 100%; background: linear-gradient(135deg, #f3d06c, #aa841c);
        border-radius: 4px 8px 8px 4px; display: flex; align-items: center; justify-content: center;
    }
    .is-unlocked { transform: rotateY(-110deg); opacity: 0.6; }
    .is-locked-at-end { right: auto; left: -15px; transform-origin: right; }

    /* --- RESPONSIVE MEDIA QUERY --- */
    @media (max-width: 1024px) {
        .book-interface-container {
            transform: scale(0.9);
            transform-origin: center;
        }
    }

    @media (max-width: 800px) {
        #menu-book-overlay { align-items: flex-start; padding: 10px; overflow-y: auto; }
        .book-interface-container { flex-direction: column; align-items: center; gap: 12px; transform: none; width: 100%; }
        
        .selected-menus-sidebar { width: 100%; max-width: 350px; height: auto; max-height: 160px; order: 1; }
        .selected-menus-sidebar.collapsed { width: 100%; max-width: 350px; height: 35px; }
        .sidebar-collapsed-label { transform: none; top: 8px; left: 12px; }
        
        .book-wrapper { order: 3; width: 100%; max-width: 350px; height: 320px; perspective: 1000px; background: transparent; }
        .page { width: 100%; right: 0; }
        .page-back { transform: none; position: absolute; width: 100%; height: 100%; top: 0; left: 0; background: #fdfaf7; border-radius: 0 8px 8px 0; display: none; }
        .btn-position-holder { display: flex; gap: 8px; margin-top: 3px; }
    }
</style>

<!-- button onclick="openMenuBook()" style="background: #800000; color: #fff; padding: 12px 24px; border: none; border-radius: 8px; font-family: 'Poppins', sans-serif; font-weight: bold; cursor: pointer; font-size: 1rem; box-shadow: 0 4px 12px rgba(0,0,0,0.15);">
    📖 Buksan ang Menu Book
</button -->

<div id="menu-book-overlay" onclick="closeOnOutsideClick(event)">
    <div style="position: absolute; top: 15px; right: 20px; color: white; cursor: pointer; font-size: 30px; z-index: 10020;" onclick="closeMenuBook()">&times;</div>
    
    <div class="book-interface-container">
        
        <!-- LEFT SIDE: SIDEBAR -->
        <div class="selected-menus-sidebar" id="selectedMenusSidebar">
            <button class="sidebar-toggle-btn" onclick="toggleSidebar()" title="Toggle Selected Menus">
                <i class="fas fa-chevron-left" id="sidebarToggleIcon"></i>
            </button>
            <span class="sidebar-collapsed-label" onclick="toggleSidebar()">📂 Selected Menus (<span id="collapsedCount">0</span>)</span>
            
            <div class="sidebar-content">
                <h3 style="font-family:'Playfair Display'; color: #800000; font-size: 0.85rem; margin: 0 0 2px 0;">Selected Menus</h3>
                <p style="font-size: 0.6rem; color: #666; margin: 0;">Mga pagkaing napili mo.</p>
                
                <div class="selected-list-container" id="selectedListContainer">
                    <p style="font-size: 0.65rem; color: #aaa; text-align: center; margin-top: 10px;">Wala pang napipiling menu.</p>
                </div>

                <div class="sidebar-total-section">
                    <span>Total Amount:</span>
                    <span id="sidebarTotalAmount">₱0.00</span>
                </div>

                <button style="width: 100%; padding: 6px; background: #800000; color: #fff; border: none; border-radius: 6px; font-weight: bold; cursor: pointer; font-size: 0.7rem;" onclick="proceedToCheckout()">
                    Confirm Order
                </button>
            </div>
        </div>

        <!-- LEFT ARROW (Pang-balik ng pahina sa kaliwa ng 3D Book) -->
        <div class="btn-position-holder" style="order: 2;">
            <button class="book-nav-btn" id="prevBookPageBtn" onclick="turnToPrevPage()" disabled>
                <i class="fas fa-chevron-left"></i>
            </button>
        </div>

        <!-- CENTER/RIGHT SIDE: 3D BOOK -->
        <div class="book-wrapper" style="order: 3;">
            <div class="book-3d-mechanical-lock" id="bookMechanical3DLock" onclick="turnToNextPage()">
                <div class="lock-metal-clasp"></div>
            </div>
            
            <!-- PAGE 1: COVER & BEEF CATEGORY -->
            <div class="page" id="p1">
                <div class="page-front" style="background: #800000; color: white; text-align: center; justify-content: center; border: 2px solid #d4a373; border-left: 8px solid #5a0000; box-shadow: 10px 5px 20px rgba(0,0,0,0.4);">
                    <h1 style="font-family:'Playfair Display'; color: white; font-size: 1.5rem; margin:0;">THELMA'S</h1>
                    <p style="letter-spacing: 2px; font-size: 0.65rem; color: #d4a373; text-transform: uppercase; font-weight: bold; margin-top: 5px;">Menu Book</p>
                    <div style="margin-top: 20px; border-top: 1px solid rgba(212, 163, 115, 0.5); width: 60%; align-self: center; padding-top: 10px; font-style: italic; font-size: 0.65rem; color: #d4a373;">
                        I-click ang Lock o Next Button para buksan
                    </div>
                </div>
                <div class="page-back">
                    <h2 class="page-title">🥩 Beef Menu</h2>
                    <div class="menu-item-card">
                        <div class="menu-item-info">
                            <img src="https://images.unsplash.com/photo-1555244162-803834f70033?w=100" class="menu-item-img">
                            <div class="menu-item-details">
                                <h4>Special Beef Caldereta</h4>
                                <span>₱350.00</span>
                            </div>
                        </div>
                        <button class="btn-select-menu" onclick="toggleSelectMenu(event, this, 'Special Beef Caldereta', 350)">Select</button>
                    </div>
                    <div class="menu-item-card">
                        <div class="menu-item-info">
                            <img src="https://images.unsplash.com/photo-1544025162-d76694265947?w=100" class="menu-item-img">
                            <div class="menu-item-details">
                                <h4>Beef Mechado</h4>
                                <span>₱340.00</span>
                            </div>
                        </div>
                        <button class="btn-select-menu" onclick="toggleSelectMenu(event, this, 'Beef Mechado', 340)">Select</button>
                    </div>
                </div>
            </div>

            <!-- PAGE 2: PORK CATEGORY -->
            <div class="page" id="p2">
                <div class="page-front">
                    <h2 class="page-title">🐖 Pork Menu</h2>
                    <div class="menu-item-card">
                        <div class="menu-item-info">
                            <img src="https://images.unsplash.com/photo-1544025162-d76694265947?w=100" class="menu-item-img">
                            <div class="menu-item-details">
                                <h4>Crispy Pata Deluxe</h4>
                                <span>₱650.00</span>
                            </div>
                        </div>
                        <button class="btn-select-menu" onclick="toggleSelectMenu(event, this, 'Crispy Pata Deluxe', 650)">Select</button>
                    </div>
                    <div class="menu-item-card">
                        <div class="menu-item-info">
                            <img src="https://images.unsplash.com/photo-1555244162-803834f70033?w=100" class="menu-item-img">
                            <div class="menu-item-details">
                                <h4>Pork Sisig Special</h4>
                                <span>₱280.00</span>
                            </div>
                        </div>
                        <button class="btn-select-menu" onclick="toggleSelectMenu(event, this, 'Pork Sisig Special', 280)">Select</button>
                    </div>
                </div>
                <div class="page-back">
                    <h2 class="page-title">🍗 Chicken Menu</h2>
                    <div class="menu-item-card">
                        <div class="menu-item-info">
                            <img src="https://images.unsplash.com/photo-1563379091339-03b21ab4a4f8?w=100" class="menu-item-img">
                            <div class="menu-item-details">
                                <h4>Chicken Cordon Bleu</h4>
                                <span>₱320.00</span>
                            </div>
                        </div>
                        <button class="btn-select-menu" onclick="toggleSelectMenu(event, this, 'Chicken Cordon Bleu', 320)">Select</button>
                    </div>
                    <div class="menu-item-card">
                        <div class="menu-item-info">
                            <img src="https://images.unsplash.com/photo-1555244162-803834f70033?w=100" class="menu-item-img">
                            <div class="menu-item-details">
                                <h4>Garlic Butter Chicken</h4>
                                <span>₱300.00</span>
                            </div>
                        </div>
                        <button class="btn-select-menu" onclick="toggleSelectMenu(event, this, 'Garlic Butter Chicken', 300)">Select</button>
                    </div>
                </div>
            </div>

            <!-- PAGE 3: SEAFOOD CATEGORY -->
            <div class="page" id="p3">
                <div class="page-front">
                    <h2 class="page-title">🦐 Seafood Menu</h2>
                    <div class="menu-item-card">
                        <div class="menu-item-info">
                            <img src="https://images.unsplash.com/photo-1563379091339-03b21ab4a4f8?w=100" class="menu-item-img">
                            <div class="menu-item-details">
                                <h4>Butter Garlic Shrimp</h4>
                                <span>₱380.00</span>
                            </div>
                        </div>
                        <button class="btn-select-menu" onclick="toggleSelectMenu(event, this, 'Butter Garlic Shrimp', 380)">Select</button>
                    </div>
                </div>
                <div class="page-back">
                    <h2 class="page-title">🍝 Pasta & Noodles</h2>
                    <div class="menu-item-card">
                        <div class="menu-item-info">
                            <img src="https://images.unsplash.com/photo-1563379091339-03b21ab4a4f8?w=100" class="menu-item-img">
                            <div class="menu-item-details">
                                <h4>Pancit Bihon Tray</h4>
                                <span>₱850.00</span>
                            </div>
                        </div>
                        <button class="btn-select-menu" onclick="toggleSelectMenu(event, this, 'Pancit Bihon Tray', 850)">Select</button>
                    </div>
                </div>
            </div>
        
            <!-- PAGE 4: DESSERTS & DRINKS CATEGORY -->
            <div class="page" id="p4">
                <div class="page-front">
                    <h2 class="page-title">🍨 Desserts</h2>
                    <div class="menu-item-card">
                        <div class="menu-item-info">
                            <img src="https://images.unsplash.com/photo-1563379091339-03b21ab4a4f8?w=100" class="menu-item-img">
                            <div class="menu-item-details">
                                <h4>Leche Flan Special</h4>
                                <span>₱150.00</span>
                            </div>
                        </div>
                        <button class="btn-select-menu" onclick="toggleSelectMenu(event, this, 'Leche Flan Special', 150)">Select</button>
                    </div>
                </div>
                <div class="page-back">
                    <h2 class="page-title">🍹 Drinks</h2>
                    <div class="menu-item-card">
                        <div class="menu-item-info">
                            <img src="https://images.unsplash.com/photo-1563379091339-03b21ab4a4f8?w=100" class="menu-item-img">
                            <div class="menu-item-details">
                                <h4>Fresh Iced Tea (Pitcher)</h4>
                                <span>₱120.00</span>
                            </div>
                        </div>
                        <button class="btn-select-menu" onclick="toggleSelectMenu(event, this, 'Fresh Iced Tea (Pitcher)', 120)">Select</button>
                    </div>
                </div>
            </div>

            <!-- PAGE 5: EXTRA MENU & BACK COVER -->
            <div class="page" id="p5">
                <div class="page-front">
                    <h2 class="page-title">🍲 Soup & Appetizer</h2>
                    <div class="menu-item-card">
                        <div class="menu-item-info">
                            <img src="https://images.unsplash.com/photo-1563379091339-03b21ab4a4f8?w=100" class="menu-item-img">
                            <div class="menu-item-details">
                                <h4>Cream of Mushroom Soup</h4>
                                <span>₱180.00</span>
                            </div>
                        </div>
                        <button class="btn-select-menu" onclick="toggleSelectMenu(event, this, 'Cream of Mushroom Soup', 180)">Select</button>
                    </div>
                </div>
                <div class="page-back" style="background: #800000; color: white; text-align: center; justify-content: center;">
                    <h2 style="font-family:'Playfair Display'; color: white; font-size: 1.3rem;">END OF MENU</h2>
                    <p style="font-size: 0.65rem; color: #d4a373; margin-top: 8px;">I-check ang sidebar sa kaliwa para sa mga napili mo.</p>
                </div>
            </div>
        </div>

        <!-- RIGHT ARROW (Pang-next ng pahina sa kanan ng 3D Book) -->
        <div class="btn-position-holder" style="order: 4;">
            <button class="book-nav-btn" id="nextBookPageBtn" onclick="turnToNextPage()">
                <i class="fas fa-chevron-right"></i>
            </button>
        </div>

    </div>
</div>

<script>
    let currentOpenPagePointer = 0; 
    const maxTotalBookPages = 5; 
    let selectedMenusArray = [];

    function openMenuBook() { 
        document.getElementById('menu-book-overlay').style.display = 'flex'; 
        currentOpenPagePointer = 0;
        
        for(let i = 1; i <= maxTotalBookPages; i++) {
            const pageElem = document.getElementById(`p${i}`);
            pageElem.classList.remove('flipped');
            pageElem.style.zIndex = maxTotalBookPages - i + 1;
        }
        
        updateNavButtonsState();
    }

    function closeMenuBook() {
        document.getElementById('menu-book-overlay').style.display = 'none';
        currentOpenPagePointer = 0;
        updateNavButtonsState();
    }

    function closeOnOutsideClick(event) {
        if (event.target === document.getElementById('menu-book-overlay')) { closeMenuBook(); }
    }

    function toggleSidebar() {
        const sidebar = document.getElementById('selectedMenusSidebar');
        const icon = document.getElementById('sidebarToggleIcon');
        sidebar.classList.toggle('collapsed');
        if(sidebar.classList.contains('collapsed')) {
            icon.classList.remove('fa-chevron-left');
            icon.classList.add('fa-chevron-right');
        } else {
            icon.classList.remove('fa-chevron-right');
            icon.classList.add('fa-chevron-left');
        }
    }

    function toggleSelectMenu(event, buttonElem, menuName, menuPrice) {
        event.stopPropagation();
        const existingIndex = selectedMenusArray.findIndex(item => item.name === menuName);

        if (existingIndex > -1) {
            selectedMenusArray.splice(existingIndex, 1);
            buttonElem.classList.remove('selected');
            buttonElem.innerText = 'Select';
        } else {
            selectedMenusArray.push({ name: menuName, price: menuPrice });
            buttonElem.classList.add('selected');
            buttonElem.innerText = 'Selected ✓';
        }
        renderSelectedMenusList();
    }

    function renderSelectedMenusList() {
        const container = document.getElementById('selectedListContainer');
        const countBadge = document.getElementById('collapsedCount');
        const totalAmountElem = document.getElementById('sidebarTotalAmount');
        countBadge.innerText = selectedMenusArray.length;

        if (selectedMenusArray.length === 0) {
            container.innerHTML = `<p style="font-size: 0.65rem; color: #aaa; text-align: center; margin-top: 10px;">Wala pang napipiling menu.</p>`;
            totalAmountElem.innerText = '₱0.00';
            return;
        }

        let html = '';
        let grandTotal = 0;
        
        selectedMenusArray.forEach((item) => {
            grandTotal += item.price;
            html += `
                <div class="selected-item-row">
                    <div>
                        <strong style="display:block; color:#333;">${item.name}</strong>
                        <span style="color:#800000;">₱${item.price}.00</span>
                    </div>
                    <button onclick="removeSelectedItem('${item.name}')"><i class="fas fa-trash-alt"></i></button>
                </div>
            `;
        });
        
        container.innerHTML = html;
        totalAmountElem.innerText = `₱${grandTotal}.00`;
    }

    function removeSelectedItem(menuName) {
        selectedMenusArray = selectedMenusArray.filter(item => item.name !== menuName);
        
        document.querySelectorAll('.menu-item-card').forEach(card => {
            const title = card.querySelector('h4').innerText;
            if (title === menuName) {
                const btn = card.querySelector('.btn-select-menu');
                btn.classList.remove('selected');
                btn.innerText = 'Select';
            }
        });

        renderSelectedMenusList();
    }

    function proceedToCheckout() {
        if(selectedMenusArray.length === 0) {
            alert('Mangyaring pumili muna ng kahit isang menu.');
            return;
        }
        alert('Order confirmed! Total items: ' + selectedMenusArray.length);
    }

    function turnToNextPage() {
        if (currentOpenPagePointer < maxTotalBookPages) {
            const lockElement = document.getElementById('bookMechanical3DLock');
            if (currentOpenPagePointer === 0 && lockElement) {
                lockElement.classList.add('is-unlocked');
            }
            currentOpenPagePointer++;
            const targetPage = document.getElementById(`p${currentOpenPagePointer}`);
            targetPage.classList.add('flipped');
            setTimeout(() => { targetPage.style.zIndex = currentOpenPagePointer; }, 300);
            updateNavButtonsState();
        }
    }

    function turnToPrevPage() {
        if (currentOpenPagePointer > 0) {
            const targetPage = document.getElementById(`p${currentOpenPagePointer}`);
            targetPage.classList.remove('flipped');
            const pageNum = currentOpenPagePointer;
            setTimeout(() => { 
                if(pageNum >= 1 && pageNum <= 5) targetPage.style.zIndex = 6 - pageNum;
            }, 300);
            currentOpenPagePointer--;
            updateNavButtonsState();
        }
    }

    function updateNavButtonsState() {
        const prevBtn = document.getElementById('prevBookPageBtn');
        const nextBtn = document.getElementById('nextBookPageBtn');
        const lockElement = document.getElementById('bookMechanical3DLock');
        
        prevBtn.disabled = (currentOpenPagePointer === 0);
        nextBtn.disabled = (currentOpenPagePointer === maxTotalBookPages);
        
        if (lockElement) {
            if (currentOpenPagePointer === 0) lockElement.className = "book-3d-mechanical-lock";
            else if (currentOpenPagePointer === maxTotalBookPages) lockElement.className = "book-3d-mechanical-lock is-locked-at-end";
            else lockElement.className = "book-3d-mechanical-lock is-unlocked";
        }
        
        prevBtn.classList.toggle('auto-hide-arrow', currentOpenPagePointer === 0);
        nextBtn.classList.toggle('auto-hide-arrow', currentOpenPagePointer === maxTotalBookPages);
    }
</script>
