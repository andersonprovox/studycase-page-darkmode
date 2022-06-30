# Construindo uma página com dark mode

## Estruturando o HTML

Primeiramente vamos estrutura o HTML.

- Importar os arquivos de CSS e JS em suas respectivas pastas
- quando importar o arquivo JS use o atributo *defer*, para que o carregamento seja antes da página.
- Nesse projeto vai ser usado o *Bootstrap Icons*.

Segue a estrutura da página em HTML:

```html
<!DOCTYPE html>
<html lang="pt-br">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Página DarkMode</title>
        <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.8.3/font/bootstrap-icons.css">
        <link rel="stylesheet" href="css/styles.css">
        <script src="js/scripts.js" defer></script>
    </head>
    <body class="dark">
        <header>
            <h2>Light and Dark</h2>
            <div>
                <input type="checkbox" name="change-theme" id="change-theme">
                <label for="change-theme">
                    <i class="bi bi-sun"></i>
                    <i class="bi bi-moon"></i>
                </label>
            </div>
        </header>
        <main>
            <div class="card">
                <div class="card-image">
                    <span>Nike</span>
                    <img src="img/tenis.png" alt="Tênis Nike">
                </div>
                <div class="card-details">
                    <h2>Tênis Nike</h2>
                    <p class="subtitle">Excelente para corridas</p>
                    <p class="description">Lorem ipsum dolor sit amet consectetur adipisicing elit. Pariatur ipsa repellendus quia velit ratione amet consequatur ipsum animi, quo, eligendi ex dignissimos quidem voluptatibus veritatis rem odio est, molestias aliquid.</p>
                    <div class="price-container">
                        <span class="price">R$499,99</span>
                        <button class="btn">Comprar</button>
                    </div>
                </div>
            </div>
        </main>
    </body>
</html>
```

## Criando a lógica da página

Com o JavaScript vamos criar o acionamento da troca entre os temas claro e escuro, manipulando a classe do CSS.

Primeiramente vamos selecionar o checkbox "change-theme".

```javascript
const changeThemeBtn = document.querySelector("#change-theme");
```

Será definido um `addEventListener()` para que cada mudança no *input* faça com que ative a função que atribui a classe *dark* do tema escuto ao *body* da página.

Também está sendo salvo no *localStorage* as alterações do usuário, para que quando ele volte para a página a sua configuração esteja salva e se ele escolheu o tema *dark*, numa próxima apresentação a página continuará com o mesmo tema escolhido.

- Observando com um evento as alterações ao clicar no input(1):
- Atribuindo a função `toggleDarkMode();`(2)
- Atribuindo o tema do dark mode com o `localStorage()` (3)

```javascript
changeThemeBtn.addEventListener("change", function() {//(1)
    toggleDarkMode();//(2)

    // Save or remove dark mode

    localStorage.removeItem("dark");

    if(document.body.classList.contains("dark")) {
        localStorage.setItem("dark", 1);//(3)
    }
})
```

Para o próximo carregamento da página já vamos puxar o que foi salvo pelo usuário para a exibição da página:

```javascript
function loadTheme() {
    const darkMode = localStorage.getItem("dark");

    if(darkMode) {
        toggleDarkMode();
    }
}

loadTheme();
```

Vendo o resultado final do código:
```Javascript

const changeThemeBtn = document.querySelector("#change-theme");


function toggleDarkMode() {
    document.body.classList.toggle("dark");
}

// Load light or dark mode

function loadTheme() {
    const darkMode = localStorage.getItem("dark");

    if(darkMode) {
        toggleDarkMode();
    }
}

loadTheme();

changeThemeBtn.addEventListener("change", function() {
    toggleDarkMode();

    // Save or remove dark mode

    localStorage.removeItem("dark");

    if(document.body.classList.contains("dark")) {
        localStorage.setItem("dark", 1);
    }
})
```
## Estilizando a página

Imagem de apresentação da página.

![imagem do modo light mode](/img/lightMode.jpg)

1. *Header* da página com espaçamento e conceito de *flexbox* para dimensionar o título e o *input* de *dark mode*.

   ```css
   header {
       display: flex;
       justify-content: space-between;
       align-items: center;
       background-color: #eceff1;
       box-shadow: .5px .5px 10px .5px #000;
       padding: 1rem 2rem;
       position: relative;
   }
   ```

   

2. Este botão está sendo gerido por um toggle que vai trocar a imagem 

```css
.dark .bi-sun {
    display: none;
}

.dark .bi-moon {
    display: block;
}
```

3. Dimensionamento da caixa de informações

```css
.card {
    margin-top: 4rem;
    display: flex;
    width: 60%;
    background-color: #fff;
    box-shadow: 5px 5px 5px 0px rgba(0, 0, 0, 0.3);
}

.card-image,
.card-details {
    padding: 2rem;
    width: 50%;
}
.card-image {
    position: relative;
    background-color: #eff7fc;
}

.card-image span {
    font-size: 6rem;
    font-weight: 900;
}

.card img {
    width: 130%;
    transform: rotate(-25deg);
    position: absolute;
    right: -1rem;
    top: 10rem;
}

.card-details h2 {
    font-size: 3rem;
    margin-bottom: 1rem;
}

.subtitle {
    color: #444;
    text-transform: uppercase;
    font-weight: bold;
    margin-bottom: 1rem;
}

.description {
    line-height: 1.6rem;
    margin-bottom: 2rem;
}

.price-container {
    display: flex;
    justify-content: space-between;
}

.price {
    font-weight: 900;
    font-size: 2rem;
}

.btn {
    background-color: #444;
    width: 7rem;
    height: 3rem;
    border: none;
    border-radius: 3rem;
    color: #fff;
    text-transform:uppercase;
    cursor:pointer
}
```

4. A imagem foi dimensionada e sofreu inclinação através do CSS para dar o efeito saindo da caixa de informação:

```css
.card img {
    width: 130%;
    transform: rotate(-25deg);
    position: absolute;
    right: -1rem;
    top: 10rem;
}
```

5. estilização do botão para ter a aparência curvada

```css
.btn {
    background-color: #444;
    width: 7rem;
    height: 3rem;
    border: none;
    border-radius: 3rem;
    color: #fff;
    text-transform:uppercase;
    cursor:pointer
}
```

Este efeito foi obtido ao dar o mesmo tamanho do `border-radius` para a altura `height`.

### Atribuindo tema escuro

![imagem dark mode](/img/darkMode.jpg)



Para o momento no qual através do JavaScript será atribuído o modo escuro, o CSS com a classe responsável por essa alteração:

```css
.dark,
.dark header {
    background-color: #263238;
    color: #fff;
}

.dark .bi-sun {
    display: none;
}

.dark .bi-moon {
    display: block;
}

.dark .card {
    background-color: #37474f;
}

.dark .card-image {
    background-color: #273035;
}

.dark .subtitle {
    color: #67b4f3;
}

.dark .description {
    color:#2196f3;
}

.dark .btn {
    background-color: #67b4f3;
}
```

