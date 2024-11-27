# **Documentação do Código HTML de Mapas**
Este documento descreve a estrutura, funcionalidade e elementos principais do código HTML para uma página de mapas e informações sobre linhas de transporte público.

---

## **1. Estrutura Geral**
A página é dividida em três partes principais:
1. **Cabeçalho (`<header>`)**: Contém os títulos principais e o menu.
2. **Corpo (`<body>`)**: Inclui a área de mapas, barra de busca, seções informativas e tabela de horários.
3. **Rodapé (`<footer>`)**: Contém botões adicionais e um fundo decorativo.

---

## **2. Cabeçalho**
O cabeçalho utiliza títulos estilizados para representar informações gerais sobre o conteúdo.
- **Elementos**:
  - `<h1>` e `<h4>`: Representam o título principal ("SP", "EMTU") e o menu.
  - `aria-label`: Fornece descrições acessíveis para leitores de tela.

```html
<header>
    <h1 style="padding: 0 19px;" aria-label="S.P">SP</h1>
    <h1 style="text-align: center;" aria-label="E.M.T.U">EMTU</h1>
    <h4 style="padding: 0 20px;" aria-label="menu">MENU</h4>
</header>
```

---

## **3. Corpo**
O corpo é o conteúdo principal e contém diversas funcionalidades organizadas em seções.

### **3.1. Navegação de Mapas**
Permite navegar entre diferentes mapas por meio de um menu suspenso (`<select>`) e visualizar o mapa escolhido em um `<iframe>`.

- **Elementos**:
  - `<select>`: Lista de mapas disponíveis.
  - `<iframe>`: Mostra o mapa escolhido.
  - **Função JavaScript**:
    - `changeImage()`: Atualiza o mapa exibido no `<iframe>` com base na escolha do usuário.
    - `loadMapFromURL()`: Carrega o mapa apropriado usando o parâmetro da URL.

```html
<select name="linha" id="imageSelector" onchange="changeImage()" style="height: 25px; width: 30%;">
    <option value="URL_DO_MAPA">Mapa Geral</option>
    <!-- Outras opções -->
</select>

<div style="overflow: hidden; position: relative; width: 100%; height: 500px;">
    <iframe id="displayImage" src="URL_PADRÃO" style="border: 0; width: 100%; height: 600px;"></iframe>
</div>
```

---

### **3.2. Barra de Busca**
Inclui um campo de texto para busca e um botão para pesquisar.

- **Elementos**:
  - `<input>`: Campo de texto para digitar termos de pesquisa.
  - `<button>`: Botão para enviar a pesquisa.

```html
<div id="search">
    <input type="text" id="searchBar" placeholder="O que você procura?" aria-label="barra de pesquisa">
    <button aria-label="pesquisar">o</button>
</div>
```

---

### **3.3. Seções Informativas**
Exibe informações sobre categorias de usuários (escolar, especial, idoso e vale-transporte).

- **Elementos**:
  - Cada item é representado como um `<div>` com descrição e estilo consistente.

```html
<div class="pai">
    <div class="child" aria-label="informações sobre o passe escolar">
        <h6>Passe<br>Escolar</h6>
    </div>
    <!-- Outros itens -->
</div>
```

---

### **3.4. Tabela de Horários**
Mostra horários e paradas das linhas de transporte. Atualmente, contém apenas placeholders.

- **Elementos**:
  - `<table>`: Estrutura da tabela.
  - `<thead>`: Cabeçalho com os títulos das colunas.
  - `<tbody>`: Corpo com os dados das linhas (ainda não preenchidos).

```html
<table border="1">
    <thead>
        <tr>
            <th>Número da linha</th>
            <th>Nome da linha</th>
            <th>Horários</th>
            <th>Parada</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>[...]</td>
            <td>[...]</td>
            <td>[...]</td>
            <td>[...]</td>
        </tr>
    </tbody>
</table>
```

---

## **4. Rodapé**
O rodapé contém botões e uma área decorativa.

- **Elementos**:
  - Botões (`<button>`): Podem ser utilizados para navegação ou outras interações.
  - Área de fundo (`<div>`): Decoração com cor sólida e bordas.

```html
<footer>
    <div style="display: flex; justify-content: space-evenly;">
        <button class="footerbtn"></button>
        <button class="footerbtn"></button>
        <button class="footerbtn"></button>
    </div>
    <div style="background-color: rgb(37, 37, 86); height: 170px;">
        <div style="border: 1px solid white; height: 40px;"></div>
    </div>
</footer>
```

---

## **5. JavaScript**
Controla as interações e a troca de mapas dinamicamente.

### **Funções**
1. **`changeImage()`**:
   - Atualiza o `<iframe>` com a URL do mapa selecionado.
   - Atualiza a URL da página sem recarregar (usando `history.pushState`).

2. **`loadMapFromURL()`**:
   - Carrega o mapa selecionado ao acessar a página usando o parâmetro `map` da URL.

```javascript
function changeImage() {
    const selector = document.getElementById('imageSelector');
    const image = document.getElementById('displayImage');
    image.src = selector.value;

    const url = new URL(window.location);
    url.searchParams.set('map', selector.value);
    window.history.pushState({}, '', url);
}

function loadMapFromURL() {
    const urlParams = new URLSearchParams(window.location.search);
    const mapParam = urlParams.get('map');
    
    if (mapParam) {
        const selector = document.getElementById('imageSelector');
        selector.value = mapParam;
        document.getElementById('displayImage').src = mapParam;
    }
}

window.onload = loadMapFromURL;
```

---

## **6. Melhorias Futuras**
1. **Adicionar Dados Reais**:
   - Preencher a tabela de horários com informações úteis.
   - Incluir mapas e rotas adicionais.

2. **Responsividade**:
   - Implementar `media queries` no CSS para melhorar a usabilidade em dispositivos móveis.

3. **Interatividade**:
   - Conectar botões do rodapé a funcionalidades específicas.
   - Adicionar funcionalidade à barra de pesquisa.

---
