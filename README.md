<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Comparação de Preços - Papelarias</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }
        
        .container {
            max-width: 1400px;
            margin: 0 auto;
            background: white;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
            overflow: hidden;
        }
        
        .header {
            background: linear-gradient(45deg, #2c3e50, #3498db);
            color: white;
            padding: 25px;
            text-align: center;
        }
        
        .header h1 {
            font-size: 2.2em;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }
        
        .header p {
            font-size: 1.1em;
            opacity: 0.9;
        }
        
        .controls {
            background: #f8f9fa;
            padding: 20px;
            border-bottom: 1px solid #e9ecef;
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            align-items: center;
        }
        
        .form-group {
            display: flex;
            flex-direction: column;
            min-width: 150px;
        }
        
        .form-group label {
            font-weight: 600;
            margin-bottom: 5px;
            color: #2c3e50;
            font-size: 0.9em;
        }
        
        .form-group input, .form-group select {
            padding: 8px 12px;
            border: 2px solid #ddd;
            border-radius: 6px;
            font-size: 0.95em;
            transition: border-color 0.3s;
        }
        
        .form-group input:focus, .form-group select:focus {
            outline: none;
            border-color: #3498db;
        }
        
        .btn {
            padding: 10px 20px;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            font-weight: 600;
            transition: all 0.3s;
            font-size: 0.95em;
        }
        
        .btn-primary {
            background: linear-gradient(45deg, #3498db, #2980b9);
            color: white;
        }
        
        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(52, 152, 219, 0.4);
        }
        
        .btn-danger {
            background: linear-gradient(45deg, #e74c3c, #c0392b);
            color: white;
        }
        
        .btn-danger:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(231, 76, 60, 0.4);
        }
        
        .btn-success {
            background: linear-gradient(45deg, #27ae60, #229954);
            color: white;
        }
        
        .btn-success:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(39, 174, 96, 0.4);
        }
        
        .table-container {
            overflow-x: auto;
            padding: 20px;
        }
        
        table {
            width: 100%;
            border-collapse: collapse;
            background: white;
            border-radius: 8px;
            overflow: hidden;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }
        
        th {
            background: linear-gradient(45deg, #34495e, #2c3e50);
            color: white;
            padding: 15px 10px;
            text-align: left;
            font-weight: 600;
            font-size: 0.9em;
            position: sticky;
            top: 0;
            z-index: 10;
        }
        
        td {
            padding: 12px 10px;
            border-bottom: 1px solid #eee;
            font-size: 0.9em;
        }
        
        tr:hover {
            background: #f8f9fa;
        }
        
        .category-filter {
            background: #e8f4f8;
            padding: 15px;
            margin: 10px 20px;
            border-radius: 8px;
            border-left: 4px solid #3498db;
        }
        
        .stats {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            padding: 20px;
            background: #f8f9fa;
        }
        
        .stat-card {
            background: white;
            padding: 20px;
            border-radius: 10px;
            text-align: center;
            box-shadow: 0 3px 10px rgba(0,0,0,0.1);
            border-top: 4px solid #3498db;
        }
        
        .stat-number {
            font-size: 2em;
            font-weight: bold;
            color: #2c3e50;
            margin-bottom: 5px;
        }
        
        .stat-label {
            color: #7f8c8d;
            font-size: 0.9em;
        }
        
        .price {
            font-weight: bold;
            color: #27ae60;
        }
        
        .best-price {
            background: linear-gradient(45deg, #2ecc71, #27ae60);
            color: white;
            padding: 3px 8px;
            border-radius: 15px;
            font-size: 0.8em;
            font-weight: bold;
        }
        
        .export-section {
            padding: 20px;
            background: #f8f9fa;
            border-top: 1px solid #e9ecef;
            text-align: center;
        }
        
        @media (max-width: 768px) {
            .controls {
                flex-direction: column;
                align-items: stretch;
            }
            
            .form-group {
                min-width: 100%;
            }
            
            .stats {
                grid-template-columns: 1fr;
            }
            
            .header h1 {
                font-size: 1.8em;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>📊 Comparação de Preços - Papelarias</h1>
            <p>Sistema de comparação entre: Globo Papelaria • Global Livraria • Americanas • Felícia • Varejão Das Malhas</p>
        </div>
        
        <div class="controls">
            <div class="form-group">
                <label for="productName">Nome do Produto</label>
                <input type="text" id="productName" placeholder="Digite o nome do produto">
            </div>
            
            <div class="form-group">
                <label for="category">Categoria</label>
                <select id="category">
                    <option value="">Selecione a categoria</option>
                    <option value="Balões">Balões</option>
                    <option value="Decoração">Decoração</option>
                    <option value="Doces e Lembrancinhas">Doces e Lembrancinhas</option>
                    <option value="Itens necessários">Itens necessários</option>
                    <option value="Outros produtos">Outros produtos</option>
                </select>
            </div>
            
            <div class="form-group">
                <label for="globoPrice">Globo Papelaria (R$)</label>
                <input type="number" id="globoPrice" step="0.01" placeholder="0,00">
            </div>
            
            <div class="form-group">
                <label for="globalPrice">Global Livraria (R$)</label>
                <input type="number" id="globalPrice" step="0.01" placeholder="0,00">
            </div>
            
            <div class="form-group">
                <label for="americanasPrice">Americanas (R$)</label>
                <input type="number" id="americanasPrice" step="0.01" placeholder="0,00">
            </div>
            
            <div class="form-group">
                <label for="feliciaPrice">Felícia (R$)</label>
                <input type="number" id="feliciaPrice" step="0.01" placeholder="0,00">
            </div>
            
            <div class="form-group">
                <label for="varejaoPrice">Varejão Das Malhas (R$)</label>
                <input type="number" id="varejaoPrice" step="0.01" placeholder="0,00">
            </div>
            
            <button class="btn btn-primary" onclick="addProduct()">+ Adicionar Produto</button>
            <button class="btn btn-danger" onclick="clearForm()">🗑️ Limpar</button>
        </div>
        
        <div class="category-filter">
            <strong>Filtrar por categoria:</strong>
            <select id="filterCategory" onchange="filterByCategory()" style="margin-left: 10px; padding: 5px;">
                <option value="">Todas as categorias</option>
                <option value="Balões">Balões</option>
                <option value="Decoração">Decoração</option>
                <option value="Doces e Lembrancinhas">Doces e Lembrancinhas</option>
                <option value="Itens necessários">Itens necessários</option>
                <option value="Outros produtos">Outros produtos</option>
            </select>
        </div>
        
        <div class="stats" id="statsContainer">
            <div class="stat-card">
                <div class="stat-number" id="totalProducts">0</div>
                <div class="stat-label">Total de Produtos</div>
            </div>
            <div class="stat-card">
                <div class="stat-number" id="avgGlobo">R$ 0,00</div>
                <div class="stat-label">Média Globo</div>
            </div>
            <div class="stat-card">
                <div class="stat-number" id="avgGlobal">R$ 0,00</div>
                <div class="stat-label">Média Global</div>
            </div>
            <div class="stat-card">
                <div class="stat-number" id="avgAmericanas">R$ 0,00</div>
                <div class="stat-label">Média Americanas</div>
            </div>
            <div class="stat-card">
                <div class="stat-number" id="avgFelicia">R$ 0,00</div>
                <div class="stat-label">Média Felícia</div>
            </div>
            <div class="stat-card">
                <div class="stat-number" id="avgVarejao">R$ 0,00</div>
                <div class="stat-label">Média Varejão</div>
            </div>
        </div>
        
        <div class="table-container">
            <table id="productsTable">
                <thead>
                    <tr>
                        <th>#</th>
                        <th>Produto</th>
                        <th>Categoria</th>
                        <th>Globo Papelaria</th>
                        <th>Global Livraria</th>
                        <th>Americanas</th>
                        <th>Felícia</th>
                        <th>Varejão Das Malhas</th>
                        <th>Melhor Preço</th>
                        <th>Ações</th>
                    </tr>
                </thead>
                <tbody id="productsBody">
                    <!-- Os produtos serão inseridos aqui -->
                </tbody>
            </table>
        </div>
        
        <div class="export-section">
            <button class="btn btn-success" onclick="exportData()">📥 Exportar Dados</button>
            <button class="btn btn-primary" onclick="sortTable()">🔤 Ordenar A-Z</button>
        </div>
    </div>

    <script>
        let products = [];
        let productCounter = 1;

        function addProduct() {
            const name = document.getElementById('productName').value.trim();
            const category = document.getElementById('category').value;
            const globo = parseFloat(document.getElementById('globoPrice').value) || 0;
            const global = parseFloat(document.getElementById('globalPrice').value) || 0;
            const americanas = parseFloat(document.getElementById('americanasPrice').value) || 0;
            const felicia = parseFloat(document.getElementById('feliciaPrice').value) || 0;
            const varejao = parseFloat(document.getElementById('varejaoPrice').value) || 0;

            if (!name || !category) {
                alert('Por favor, preencha o nome do produto e selecione uma categoria.');
                return;
            }

            const product = {
                id: productCounter++,
                name: name,
                category: category,
                prices: {
                    globo: globo,
                    global: global,
                    americanas: americanas,
                    felicia: felicia,
                    varejao: varejao
                }
            };

            products.push(product);
            updateTable();
            updateStats();
            clearForm();
        }

        function updateTable() {
            const tbody = document.getElementById('productsBody');
            tbody.innerHTML = '';

            const filteredProducts = getFilteredProducts();

            filteredProducts.forEach(product => {
                const row = tbody.insertRow();
                
                // Encontrar o melhor preço
                const prices = [
                    {store: 'Globo', price: product.prices.globo},
                    {store: 'Global', price: product.prices.global},
                    {store: 'Americanas', price: product.prices.americanas},
                    {store: 'Felícia', price: product.prices.felicia},
                    {store: 'Varejão', price: product.prices.varejao}
                ].filter(p => p.price > 0);
                
                const bestPrice = prices.length > 0 ? prices.reduce((min, p) => p.price < min.price ? p : min) : null;

                row.innerHTML = `
                    <td><strong>${product.id}</strong></td>
                    <td><strong>${product.name}</strong></td>
                    <td><span style="background: #3498db; color: white; padding: 3px 8px; border-radius: 12px; font-size: 0.8em;">${product.category}</span></td>
                    <td class="price">${formatPrice(product.prices.globo)}</td>
                    <td class="price">${formatPrice(product.prices.global)}</td>
                    <td class="price">${formatPrice(product.prices.americanas)}</td>
                    <td class="price">${formatPrice(product.prices.felicia)}</td>
                    <td class="price">${formatPrice(product.prices.varejao)}</td>
                    <td>${bestPrice ? `<span class="best-price">${bestPrice.store} - ${formatPrice(bestPrice.price)}</span>` : '-'}</td>
                    <td><button class="btn btn-danger" onclick="removeProduct(${product.id})" style="padding: 5px 10px; font-size: 0.8em;">❌</button></td>
                `;
            });
        }

        function getFilteredProducts() {
            const filterCategory = document.getElementById('filterCategory').value;
            if (!filterCategory) return products;
            return products.filter(p => p.category === filterCategory);
        }

        function filterByCategory() {
            updateTable();
        }

        function removeProduct(id) {
            if (confirm('Tem certeza que deseja remover este produto?')) {
                products = products.filter(p => p.id !== id);
                updateTable();
                updateStats();
            }
        }

        function formatPrice(price) {
            if (price === 0) return '-';
            return `R$ ${price.toFixed(2).replace('.', ',')}`;
        }

        function updateStats() {
            document.getElementById('totalProducts').textContent = products.length;
            
            const stores = ['globo', 'global', 'americanas', 'felicia', 'varejao'];
            const storeNames = ['avgGlobo', 'avgGlobal', 'avgAmericanas', 'avgFelicia', 'avgVarejao'];
            
            stores.forEach((store, index) => {
                const prices = products.map(p => p.prices[store]).filter(p => p > 0);
                const avg = prices.length > 0 ? prices.reduce((a, b) => a + b, 0) / prices.length : 0;
                document.getElementById(storeNames[index]).textContent = formatPrice(avg);
            });
        }

        function clearForm() {
            document.getElementById('productName').value = '';
            document.getElementById('category').value = '';
            document.getElementById('globoPrice').value = '';
            document.getElementById('globalPrice').value = '';
            document.getElementById('americanasPrice').value = '';
            document.getElementById('feliciaPrice').value = '';
            document.getElementById('varejaoPrice').value = '';
            document.getElementById('productName').focus();
        }

        function sortTable() {
            products.sort((a, b) => a.name.localeCompare(b.name));
            updateTable();
        }

        function exportData() {
            let csv = 'Número,Produto,Categoria,Globo Papelaria,Global Livraria,Americanas,Felícia,Varejão Das Malhas\n';
            
            products.forEach(product => {
                csv += `${product.id},"${product.name}","${product.category}",${product.prices.globo},${product.prices.global},${product.prices.americanas},${product.prices.felicia},${product.prices.varejao}\n`;
            });
            
            const blob = new Blob([csv], { type: 'text/csv' });
            const url = window.URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = 'comparacao_precos_papelarias.csv';
            a.click();
        }

        // Permitir adicionar produto com Enter
        document.addEventListener('DOMContentLoaded', function() {
            const inputs = document.querySelectorAll('input');
            inputs.forEach(input => {
                input.addEventListener('keypress', function(e) {
                    if (e.key === 'Enter') {
                        addProduct();
                    }
                });
            });
        });
    </script>
</body>
</html>
