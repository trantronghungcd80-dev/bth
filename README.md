<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chức Năng Tìm Kiếm và Lọc Dữ Liệu</title>
    <!-- Tải Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f7f7f9;
        }
        .status-badge {
            padding: 4px 8px;
            border-radius: 9999px;
            font-size: 0.75rem;
            font-weight: 600;
        }
        .status-con-hang {
            background-color: #d1fae5;
            color: #065f46;
        }
        .status-het-hang {
            background-color: #fee2e2;
            color: #991b1b;
        }
        .status-dang-ve {
            background-color: #fef3c7;
            color: #92400e;
        }
        .clickable-row {
            cursor: pointer;
            transition: background-color 0.15s;
        }
        .clickable-row:hover {
            background-color: #f3f4f6;
        }
    </style>
</head>
<body class="p-4 sm:p-8">

    <div class="max-w-6xl mx-auto bg-white shadow-xl rounded-2xl p-6 md:p-10">

        <!-- Header -->
        <h1 class="text-3xl font-bold text-gray-800 mb-2">Quản Lý Dữ Liệu Sản Phẩm</h1>
        <p class="text-gray-500 mb-6">Click vào bất kỳ hàng nào để xem chi tiết sản phẩm.</p>

        <!-- Control Panel: Search & Filter -->
        <div class="flex flex-col sm:flex-row space-y-4 sm:space-y-0 sm:space-x-4 mb-6">
            
            <!-- Input Tìm kiếm -->
            <div class="relative flex-grow">
                <input 
                    type="text" 
                    id="searchInput" 
                    placeholder="Tìm kiếm theo Tên hoặc Mã sản phẩm..."
                    class="w-full p-3 pl-10 border border-gray-300 rounded-lg focus:ring-blue-500 focus:border-blue-500 transition duration-150"
                >
                <!-- Icon Kính lúp -->
                <svg class="absolute left-3 top-1/2 transform -translate-y-1/2 w-5 h-5 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"></path></svg>
            </div>

            <!-- Dropdown Lọc -->
            <select 
                id="statusFilter" 
                class="sm:w-1/3 p-3 border border-gray-300 rounded-lg bg-white focus:ring-blue-500 focus:border-blue-500 transition duration-150 shadow-sm"
                onchange="updateTable()"
            >
                <option value="Tất cả">Lọc theo Tình trạng (Tất cả)</option>
                <option value="Còn hàng">Còn hàng</option>
                <option value="Hết hàng">Hết hàng</option>
                <option value="Đang về">Đang về</option>
            </select>
        </div>

        <!-- Data Table -->
        <div class="overflow-x-auto rounded-lg shadow-md border border-gray-200">
            <table class="min-w-full divide-y divide-gray-200">
                <thead class="bg-gray-50">
                    <tr>
                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Tên Sản Phẩm</th>
                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Mã Sản Phẩm</th>
                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Giá Bán</th>
                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Tình Trạng</th>
                    </tr>
                </thead>
                <tbody id="productTableBody" class="bg-white divide-y divide-gray-200">
                    <!-- Data rows populated by JS or static HTML -->
                    <tr class="clickable-row" data-name="Laptop ASUS Zenbook" data-code="LPT001" data-status="Còn hàng" data-description="Laptop cao cấp, mỏng nhẹ, hiệu năng vượt trội cho công việc đồ họa." data-quantity="50" onclick="showProductDetails(this)">
                        <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-blue-600 hover:text-blue-800 underline cursor-pointer">Laptop ASUS Zenbook</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">LPT001</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">25,000,000₫</td>
                        <td class="px-6 py-4 whitespace-nowrap">
                            <span class="status-badge status-con-hang">Còn hàng</span>
                        </td>
                    </tr>
                    <tr class="clickable-row" data-name="Điện Thoại Samsung Galaxy" data-code="DT005" data-status="Còn hàng" data-description="Điện thoại thông minh Android, màn hình AMOLED, camera 108MP." data-quantity="120" onclick="showProductDetails(this)">
                        <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-blue-600 hover:text-blue-800 underline cursor-pointer">Điện Thoại Samsung Galaxy</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">DT005</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">18,500,000₫</td>
                        <td class="px-6 py-4 whitespace-nowrap">
                            <span class="status-badge status-con-hang">Còn hàng</span>
                        </td>
                    </tr>
                    <tr class="clickable-row" data-name="Bàn Phím Cơ Logitech" data-code="BP012" data-status="Hết hàng" data-description="Bàn phím cơ full-size, switch Brown, thích hợp cho cả gõ văn bản và chơi game." data-quantity="0" onclick="showProductDetails(this)">
                        <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-blue-600 hover:text-blue-800 underline cursor-pointer">Bàn Phím Cơ Logitech</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">BP012</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">1,950,000₫</td>
                        <td class="px-6 py-4 whitespace-nowrap">
                            <span class="status-badge status-het-hang">Hết hàng</span>
                        </td>
                    </tr>
                    <tr class="clickable-row" data-name="Chuột Không Dây Gaming" data-code="CT008" data-status="Đang về" data-description="Chuột không dây chuyên nghiệp, độ phân giải cao, pin 100 giờ." data-quantity="35" onclick="showProductDetails(this)">
                        <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-blue-600 hover:text-blue-800 underline cursor-pointer">Chuột Không Dây Gaming</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">CT008</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">850,000₫</td>
                        <td class="px-6 py-4 whitespace-nowrap">
                            <span class="status-badge status-dang-ve">Đang về</span>
                        </td>
                    </tr>
                    <tr class="clickable-row" data-name="Màn Hình 4K Dell" data-code="MH003" data-status="Còn hàng" data-description="Màn hình 27 inch 4K, tấm nền IPS, màu sắc chuẩn cho thiết kế đồ họa." data-quantity="75" onclick="showProductDetails(this)">
                        <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-blue-600 hover:text-blue-800 underline cursor-pointer">Màn Hình 4K Dell</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">MH003</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">12,500,000₫</td>
                        <td class="px-6 py-4 whitespace-nowrap">
                            <span class="status-badge status-con-hang">Còn hàng</span>
                        </td>
                    </tr>
                     <tr class="clickable-row" data-name="Tai Nghe Chống Ồn" data-code="TN010" data-status="Hết hàng" data-description="Tai nghe chụp tai, công nghệ chống ồn chủ động (ANC) hàng đầu." data-quantity="0" onclick="showProductDetails(this)">
                        <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-blue-600 hover:text-blue-800 underline cursor-pointer">Tai Nghe Chống Ồn</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">TN010</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">3,500,000₫</td>
                        <td class="px-6 py-4 whitespace-nowrap">
                            <span class="status-badge status-het-hang">Hết hàng</span>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
        
        <!-- Footer Info -->
        <p id="resultCount" class="mt-4 text-sm text-gray-600">Hiển thị 6 kết quả.</p>

    </div>
    
    <!-- Modal Hiển Thị Chi Tiết Sản Phẩm -->
    <div id="productModal" class="fixed inset-0 bg-gray-600 bg-opacity-50 hidden items-center justify-center z-50 transition-opacity duration-300">
        <div class="bg-white rounded-xl shadow-2xl w-full max-w-lg mx-4 transform transition-all duration-300 scale-100 p-6 md:p-8">
            <!-- Modal Header -->
            <div class="flex justify-between items-center border-b pb-3 mb-4">
                <h2 id="modalProductName" class="text-2xl font-bold text-gray-800">Chi Tiết Sản Phẩm</h2>
                <button onclick="closeModal()" class="text-gray-400 hover:text-gray-600 transition">
                    <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path></svg>
                </button>
            </div>
            
            <!-- Modal Body (Details) -->
            <div class="space-y-3 text-gray-700">
                <p><strong>Mã Sản Phẩm:</strong> <span id="modalProductCode" class="font-semibold text-gray-900"></span></p>
                <p><strong>Giá Bán:</strong> <span id="modalProductPrice" class="font-semibold text-green-600"></span></p>
                <p><strong>Tình Trạng:</strong> <span id="modalProductStatus" class="font-semibold"></span></p>
                <p><strong>Số Lượng Tồn Kho:</strong> <span id="modalProductQuantity" class="font-semibold"></span></p>
                <div class="pt-2">
                    <p class="font-bold text-gray-800 mb-1">Mô Tả:</p>
                    <p id="modalProductDescription" class="text-sm italic border-l-4 border-blue-400 pl-3 py-1 bg-gray-50 rounded-md"></p>
                </div>
            </div>

            <!-- Modal Footer -->
            <div class="mt-6 pt-4 border-t flex justify-end">
                <button onclick="closeModal()" class="px-6 py-2 bg-blue-500 text-white font-medium rounded-lg hover:bg-blue-600 transition shadow-md">Đóng</button>
            </div>
        </div>
    </div>

    <script>
        
        function updateResultCount(count) {
            const resultCount = document.getElementById('resultCount');
            const totalRows = document.getElementById('productTableBody').getElementsByTagName('tr').length;
            const visibleCount = (typeof count !== 'undefined') ? count : totalRows;

            resultCount.textContent = visibleCount === 0 
                ? "Không tìm thấy kết quả nào." 
                : `Hiển thị ${visibleCount} kết quả.`;
            
            resultCount.classList.toggle('text-red-500', visibleCount === 0);
        }

        const updateTable = () => {
            const keyword = document.getElementById('searchInput').value.trim().toLowerCase();
            const filterStatus = document.getElementById('statusFilter').value;
            const rows = document.getElementById('productTableBody').getElementsByTagName('tr');
            
            let visibleRowCount = 0;

            for (let i = 0; i < rows.length; i++) {
                const row = rows[i];
                
                const name = row.getAttribute('data-name').toLowerCase();
                const code = row.getAttribute('data-code').toLowerCase();
                const status = row.getAttribute('data-status');
                
                // 1. Kiểm tra Tìm kiếm (logic OR)
                const matchesSearch = name.includes(keyword) || code.includes(keyword);

                // 2. Kiểm tra Lọc
                const matchesFilter = filterStatus === 'Tất cả' || status === filterStatus;
                
                // 3. Quyết định hiển thị (logic AND)
                const isVisible = matchesSearch && matchesFilter;
                
                row.style.display = isVisible ? "" : "none";
                
                if (isVisible) visibleRowCount++;
            }
            
            updateResultCount(visibleRowCount);
        };
        
        function showProductDetails(row) {
            const name = row.getAttribute('data-name');
            const code = row.getAttribute('data-code');
            const status = row.getAttribute('data-status');
            const price = row.querySelector('td:nth-child(3)').textContent;
            const description = row.getAttribute('data-description');
            const quantity = row.getAttribute('data-quantity');

            // Cập nhật nội dung Modal
            document.getElementById('modalProductName').textContent = name;
            document.getElementById('modalProductCode').textContent = code;
            document.getElementById('modalProductPrice').textContent = price;
            document.getElementById('modalProductStatus').textContent = status;
            document.getElementById('modalProductQuantity').textContent = quantity;
            document.getElementById('modalProductDescription').textContent = description;

            // Hiển thị Modal
            const modal = document.getElementById('productModal');
            modal.classList.remove('hidden');
            modal.classList.add('flex');
            document.body.style.overflow = 'hidden';
        }

        function closeModal() {
            const modal = document.getElementById('productModal');
            modal.classList.remove('flex');
            modal.classList.add('hidden');
            document.body.style.overflow = '';
        }

        document.addEventListener('DOMContentLoaded', () => {
            document.getElementById('searchInput').addEventListener('input', updateTable);
            document.getElementById('statusFilter').addEventListener('change', updateTable);
            updateResultCount();
        });
        
    </script>
</body>
</html>
