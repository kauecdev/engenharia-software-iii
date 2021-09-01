# Melhorias em códigos antigos

## Função para calcular fatorial de um número

- Código antigo
```js
function fatorial(n) {
  var contador = n;
  var fatorial = 1;

  while (contador > 0) {
    fatorial *= contador;
    contador -= 1;
  }
  
  return fatorial;
}
```
- Código melhorado
```js
const calcularFatorial = (numero) => numero <= 1 ? 1 : calcularFatorial(numero - 1) * numero;
```

## Calcular preço total de uma compra

- Código antigo
```js
function calcularTotal() {
  const valorBase = quantidade * precoItem;
  
  if (valorBase > 400) {
    return valorBase * 0.9;
  } else {
    return valorBase;
  }
}
```

- Código melhorado
```js
function calcularTotal() {

  const valorCompra = calcularValorCompra();

  if (valorCompra > 400) {
    return valorCompra * 0.9;
  }
  
  return valorCompra;
}

function calcularValorCompra() {
  return quantidade * precoItem;
}
```

## Verificar idade  

- Código antigo
```js
function liberarAcesso(idade) {
    
    if (idade >= 0 && idade < 18) {
        console.log("Você ainda é menor, acesso não liberado.");
    } else {
        console.log("Acesso liberado.");
        redirecionarParaHome();
    }
}
```

- Código melhorado
```js
function liberarAcesso(idade) {
    if (ehMenor(idade)) {
        console.log("Você ainda é menor, acesso não liberado.");
        return;
    }

    console.log("Acesso liberado.");
    redirecionarParaHome();
}

function ehMenor(idade) {
    return idade < 18 ? true : false;
}
```
