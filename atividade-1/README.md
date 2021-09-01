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
